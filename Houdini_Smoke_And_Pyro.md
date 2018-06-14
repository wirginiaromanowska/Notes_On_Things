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
## 2. Gas particle to field
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
- trail SOP: preserve original, trail lenght 5 (frames)
- add SOP: under poligons by group, by attribute, and attribute is id
- resample with max segments set to what would be max substeps
- point jitter - makes it more noise
- wire this directly to DOPnet
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
  
  

  





