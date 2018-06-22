## 1. Control amount of detail with shred microsolver
### a) detail on the edges 
- standard setup
- high cutoff (above density top range)
- control settings: firld - density, inluence - 1, range from 1 to 0 (opposite)
- bindings - default
### b) detail in the core - where fast velocities are
- cutoff - 10 times above top range
- control - vel, influence -1, control range from 1 to 0
- bindings: disturb firld is vector field on, disturb field - vel, threshold field density
- allow editing, in disturb vector field: control field node needs to be type vector, after append lenght node
## 2. Gas particle to field (Wagner)
### a)In SOPs
- create attribute on points/particles etc.
- name it divergence or temperature etc.
- set value to something 0.2

### b) In DOP
- smoke object
- to apply data
- to pyro solver
- sop geo node to second imput of apply data
  - bring the points
  - set to update always
- gas resize fluid dynamic to second imput of smoke solver
- gas particle to field to second imput (merge with the one above)
  - destination field is fuel or temperature or velocity
  - vel goes to vel update in solver (3rd imput)
  - attribute fuel, temp, vel (or v if it's name that way on the geo)
  

- provide sop path
```
`opimputpath("../",0)`
```
### c) After DOP
- Not always need DOP import sop, DOP has Object Merge built in:
  - Object = smokeobject1
  - Data - anything, most often density
  - can bring more fields (+ sign), temperature, vel
## 3. Rules and Advice
- avoid transforms at the object level (for emitters, colliders etc) in case you need to scale whole sim from cm to m later
- when there is error in DOPs
  - right click on node will clear the error
  - you can see what error says only in tree view (right click)
  - vel is non divergent - so will not expand or shrink - this is why it needs to go to vel update input int he pyro solver
  - only vel that can go in pre-solve imput in pyro solver is curl noise
  - how you mix in vel matters
    - try to set it to maximum instead of add
## 4. Fast moving trails
### a) Wagner way
- trail SOP: preserve original, trail lenght 5 (frames)
- add SOP: under poligons by group, by attribute, and attribute is id
- resample with max segments set to what would be max substeps
- point jitter - makes it more noise
- wire this directly to DOPnet
### b) S. K. Way
- in attrib wrangle
```
@P = @P - @TimeInc * @v
```
- go back one time increment (one sim frame) along vel vector and put point there
- merhe this with original points
- add SOP, by group, by attribute, attribute is "id"
- resample SOP to add more points in between
- attr wrangle after original (front) points and multiply pscale by 0.001, to make the lines spear shaped - thinner at the leading point. Resample SOp will interpolate between the two pscales
## 5. Pyro solver parameters
- boyancy lift - takes direction * amount of boyancy * current temperature and adds that to current vel
- gas released = expansion - often animated for explosion (high to lower to zero)
## 6. S. K. Way of setting up pyro sim
- can drag and drop out source volume from the SOP's to the smoke object initial Data Density Sop path
- don't use the shape tab in the pyro solver, add your own micro-solvers
- microsolver go to third input of the pyrosolver (velocity update), especially turbulence
- use merge to have multiple microsolvers applied together
- keyframe turbulence off
- dop import field
  - smokeobject1
  - fields to import add and field is nedsity
## 7. S. K. Sim and Render in the same queue
- make geometry in out context - this is instead of the file cache
  - drag out from dopimport to the SOP path of the geometry node
  - save in $JOB/cache
- connect this to mantra (mantra below) to runt hem together
  - will sim, save to disc and then render the image
- mantra node - click on the purple flag
  - change order to "node by done" - means first cache all sim first and the render frame range.
  - frame by frame means - sim frame, then render frame
## 8. S. K. building source
### a) simple
  - use mountain on sphere and animate it with T
  - contract and shrink size of the source 
    - by noise($T, 0, 0) in uniform scale
    - this noise range is from -0.5 to 0.5 so need to be offset noise($T, 0, 0)+1.0
  - trail SOP and compute velocity
  - fluid source SOP
### b) with debris source
- creates density attrib depending on age on particles
```
f@density = 1.0 - @age / ch("../debrisource1/lifespan");
```
- referencing channel on debris source up the stream of the same geo - ch("../debrisource1/lifespan"
- instead could make lifespan per point attribute -  @ (especially if there is variance) and use that to gen normalized age
- 1.0 - stuff is to invert the range 0-1 to 1-0
- creates pscale attribute after any particle simulation happens (to avoid strange collisions with gorund etc)
```
f@pscale = @density;
```
- Color from density - on points from debris source
```
v@Cd = set(@density, 0, 1.0 - @density);
```
- starts red and becomes blue by the end
### c) collision source
- make sdf volume ahead of time and cache
- could use fluid source (it's iso offset)
  - container settings, change to collision preset
  - makes sdf
  - records velocity
  - calls this vol field collision automatically
  - they're slow
  - buggy
- use vdb volumes
  - vdb from polygons
  - much faster
  - source attribute - point v to vel field, vector type needs to be Velocity
  
  
## 9. S. K. Fluid source SOP
- Houdini volume (stores scalar per vol)
- hollow vs/ filled with density - SDF from Geometry tab
  - Minimum distance (off to make solid vol)
  - Empty interior (off to make solid vol)
- Noise pane
  - noise is animated by default
  - tub noise 0 - 1 values
  - turbulence means levels of detail
- Vlocity pane
  - stamp points - looks how far away to look for points with vel (from the surface) to apply that vel to the density volume (filling the interior). If density volume voxel doesn;t sample far enough to find vel from point it gets 0 velocity.
  - curl noise
## 10. S. K. pyro DOP
- pyrosolver
- smoke object - scale up the box to max bounds
- source volume 
  - to sourcing/post solve/last input of pyro solver
  - point to fluid source in SOPs
  - checks every frame by default
  - Volume operations - ADD VELOCITY, and bring amount down (0.1)
  - masking vel by density (when things are going to fast/crazy)
  - keyframe scale velocity over time
  - source velocity and density in the same source, collision separate source (sdf)
- drag 0.04
- for smoke gravity at -9.8
- ground plane or collide with bottom of the fluid container
- substeps on DOP for increased swirliness and nuance in motion 
  - use more substeps when you can afford
  - add to your take system for HQ settings
- for final sim 600 voxels along if it's box (along max axis)
## 11. Resize Fluid Dynamic
- second imput/presolve of the pyro solver
-  max bounds
  - if you do not clamp to maximum = allow simulation to grow indefinetly
  - initialisation static will grow bounds to the maximum bounds specified by size in main properties of smoke object
  - the value in field cutoff tells it to grow or shrink bounds
  - initialization dynamic - for moving objects like a comet
- tracking object - the bounds are at least as big as the tracking object
  - S. k. is using bound SOP with some padding on the geo (not on fluid source)
## 12. Reseting blue cache simulation
- DOP changes
- not always by referenced in DOP sOP changes
- use button reseet sim on top of DOP network node properties
## 13. Gas Disturbance microsolver
- to the third input in pyro solver
- visualize block size by creating box in geo of the same size
- S. K. modified version
  - in bindings disturb field should disturb vel instead of temperature
  - disturb field is vector field should be on
  - threshold field is density by default, threshold refers to cutoff under disturb settings pane
  - cutoff says - apply disturbance only if there is less than 0.1 density
  - merging 2 - 3 different sizes disturbance 1/3 size difference
  - control settings by default set to density, range 0 - 0.1 (or whatever the cutoff value was)
  - control settings left side of the curve applies disturbance to lowest density - 0 and right side to whatever the max range vaue is
  - make it like \ to apply more disturbance where lower density is to break the mushroom leading edges
- S. K. modified version 2
  - S. K. later changes the control field to be vel so the parts that are moving very fast are more disturbed than areas that move slower
  - control influence set to 1
  - no keframing animation needed
  - control range 0 to 1 and remap ramp like / means speed 0 to 1 (might need a different range?)
  - allow editing of contents
  - go inside and in disturb vector field
  - we want to disturb vel based on vel
  - find control field (lower part of the vop net)
  - change the control field type to vector
  - add lenght after it to calculate speed
  
- time scale = power
## 14. Gass dissipate microsolver
- difusion = blurr 0.05
- evaporation rate = disspation 0.1
## 15. Expansion = Divergence without combustion
- With combustion: fuel + temperature = expansion + fire + smopke + more temperature
- in SOPS 
  - delete (by group) everything but density field
  - adds volume vop after fluid source created for density
- in volume vop create aanoise in simplex mode and multiply its density with original density to create pockets of expansion
- in DOPs 
  - source volume
  - merge with density
  - go to last input of pyro solver
  - preset expand
  - SOP to DOP bindings should be density to divergence
  - keyframe scale source volume only for short time at the start of time
  - can multiply by 100 or 200 if not visible
## 16. Vortex confinement
- for whicpy smoke like cigarette smoke
## 17. DOP import field
- density
- vel to get motion blur
- one of the presets might have the right settings
## 18. Adding temperaure without combustion
- if you want more boyancy
- SOP to DOP bindings density to temperature
## 19. Rest
- Enable in pyro solver in rest field pane
  - Dueal rest fields on
  - Frames between solve 10
  - Frame offset 1
  - Rest advection rate 1
- In smoke object
  - in initial data tab turn on Add Rest Field
- In dopimportfields
  - add rest and rest2 fields to import
## 20. Rendering in mantra
- watch the S. K. tutorial Applied Houdini Dynamics III
## 21. Rendering General
- On the geometry level in shading pane there is Volume Filter setting
  - try gaussian instead of box
  - with 1.5
## 22. In DOP - Collision sourcing
- source volume to collision preset
- if sourcing the col from vdb HAVE TO CHANGE SCALE SOURCE VOLUME TO NEGATIVE 1
- if sourcing from vdb names of volumes are differend, so bindings need to change
  - surface to collision
  - v to collisionvel
  - or change names when creating that vdb in SOPs
 - collision settings in pyro solver under relationship/collisions
  - extrapolate into collisions - gives sense of stickyness
  - Correct collisions - delete density inside collision volumes - turning off helps to keep more volume trail
## 23. Turbulence microsolver
- Time scale says how fast turbulence is moving through
  





  
  
  
  
  

  





