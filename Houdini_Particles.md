## 1. Particles generally
- points with attributes
  - P
  - v
  - force - vector
  - life - set in the source by life expetancy
  - age - how long it is currently alive, not normalized, still in seconds
  - @nage - normalized age - dont have to calculate = @age/@life;
  - id (unique)
  - dead - can be set in POP wrangler
- divide age/life to get 0-1 value
  - sometimes because precision it might go over 1, use clamp VOP
## 2. POP network
### a) popobject - particle bucket
- some physical properties
### b) popsolver 
- moves particles around
- collision behaviour pane + standard ground plane - can get all hit attributes like hittotal
### c) POP source
- can source only from selected group of polys
- emission attribute - for example spawn by Cd (will spawn only ehre whiter is)
- Impulse Activation 1, then Impulse count means spawn n particles every simulation frame (default every frame)
- Constant Activation 1, then Const Birth Rate means spawn n particles every second
- Life expectancy is particle life in seconds
- Life Variance + or - in seconds
- Inherit attributes from geo from where particles are spawning, like velocity or color
- in Attributes panes can set velocity - that's initial velocity
- S. K. for bursts uses 0 - 1 aniamtion on const birth rate over 13 frames
  - to ahve more than one point use Scale Point Count By area in Source tab, start with 0.001. The lower the number the more particles
## 3. Forces
### a) Popforce
- can display vecttors in vieport when guide is on
- two popforces - vectors will add
- has noise built in, layer two forces with different swirl size
- use instead of gravity dop, because gravity dop is slower (not multithreded), while pop force is faster.
### b) Drag 
- goes right under source too
### c) pop wind
- adds air resistance (drag)
- wind
- noise
- use vexpressions, to affect by wind particles only before they land ont he ground
```
amp = (@hittotal==0)
```
- amp - amplitude of the wind
- this will evaluate to 1 if particle didnt hit, so wind will be applied - can use multiplier if you want stronger wind
- this will evaluate to 0 after particle hits, so even if using strenght multiplier - wind will be still 0.
## 4. Pop location
- birth
- velocity
## 5. Problems
- geo with material/texture on it will spawn black square particles when used in POP. To solve attribute delete, primitive attribute/shop material path on the geometry
- access geometry spreed sheet in the DOP network by going in the spreed sheet/tree view on left side in popobject/geometry
## 6. POP Wrangle
- plugs below particle cource
- @dead = 1; - kills all particles
## 7. Particles rendering
- motion blur with shutter offset of negative 1 (-1)
## 8. Pop Advect By Volumes by S. K.
- use vel colume (see in volumes)
- set to update Velocity
- change color and pscale:
```
float speed = length(@v);
speed = fit(speed, chf("min_speed"), chf("max_speed"), 0, 1);
float norm_age = @age/ @life;
float bias = fit(@bias, -0.5, 0.5, 0, 1);
@Cd = set(speed, bias, norm_age);
@pscale = chf("scale") * chramp("size_ramp",  norm_age);
```
- particles will stop moving and be stuck to the edge of puto container, to fix post sim:
  - create box with the same dimentions as the pyro sim container
  - vdb from polys - sdf
  - attrib wrangle, with forst input from particles (post sim), second input from the vdb
  ```
  float bound_scale = fit(volumesample(1, 0, @P), chf("min_dist"), chf("max_dist"), 1, 0);
  @pscale *= bound_scale;
  ```
## 9. In vieport
- press D and go to geo tab and display particles as pixels
## 10. Rest (start) position for coloring etc
- create justborn group in DOPS in source
- append popwrangle to run over justborn group with v@rest = @P;
## 11. Grouping by age
- in popnet create PopGroup POP
- by rule
```
ingroup = @nage > 0.6;
```
## 12. SLow down particles in certain grouop
- in POP network create PopWrangle
```
@v = @v*0.8;
```
- 20% drop in vel for each frame
## 13. Color based on speed
- in POP network create POPColor
- ramp = lenght(@v);
## 14. POP collision detect
- after source
- collision - path to sop (ground)
- behaviour - default is none (change to stop etc)
- om stop they by default miss the collision by a bit, can use move to hit checkbox to align them perfectly
- to record particles that just hit use group name "justHit"
gives bunch of useful atributes to create groups:
- @hittotal=0
- @stopped=1
## 15. Replace points with particles
- Add sop - particles pane - add particles
## 16. To make particles stick to point they are spawned from
- put down a pop wrangle
```
@P = point("op:/obj/MorphGeo/OUT_SOURCE", "P", @id);
```
- id needs to match
## 17. Pop fluid dop
- wire by merging with emitter source, but last, just before going to pop solver
- adds volume to particles (particles have collision pscale)
- replaces pop interact
- projection type - update velocity
- velocity blend 0.8 makes it very viscous
## 18. Orient and w
- for initial orientation use orient
  - attrib randomize on points that particles are emitted from
  - 4 dimentions
  - distribution - inside sphere
- for spin over time use w - angular velocity
  - set random from 5 to 10 - this will spin in one direction
  - and then set another attrib randomize on w as well with multiply as action and set it to be intiger -1 to 1?
## 19. Spawn particles from particles 
- pop replicate
## 20. Forces connecting
- wind or pop drag don;t need imput
- connect directly in the merge with the pop source
- connect on the right of the source if you want the force to affect particles in the source
- comnect on the left if you don't
- order of forces connections matters - executed from left to right
- can use if you want the drag to affect one force but not the other (drag affecting velocity/wind, but not gravity)
## 21. Custom radial attractor/gravity
- in pop wrangle
```
float mass = 10;  
vector origin = {0, 0, 0}; 
float dist = max(distance(v@P, origin), 2.0);  
float gravityStrength = mass / pow(dist, 0.7); 
vector gravity = (origin - v@P) * gravityStrength;  
@force += gravity;
```
## 22. To use vortex force in pops
- make line/curve in sops
- deform with noise or whatever
- vortex force attribs sop 
- point vop if you need to change radius (orbitrad attr) with height (@P.y)
- in pops vortex force and sop geometry with path to sop above
