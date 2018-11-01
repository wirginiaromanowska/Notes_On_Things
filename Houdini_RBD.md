## 1. Basics
- objects is grey plug
- data is green plug
## 2. Units
- real world
- edit/preferences/hip file options m and kg
## 3. Physical parms
- rotational stifness - how much object will spin (how much object inherites rotation when hit by another object), 0 - means no rotation
- bounce - how much energy conservation there is when two objects collide, this is multiplication between the two objects (e.g. sphere and the ground)
- friction - how difficult is to move object from rest. 0 - no resistance at all
- dynamic friction - multiplier for objects that are already moving
## 4. S. K. simplest version
- uses shelf tool to create rbd glued object (packed) from voronoi fracture
- uses shelf to create ground plane
- adds initial vel (-30) on rigids source object in DOP net
- DOP import modifications (created by shelf)
  - change import style to fetch unpacked geo from DOP (get smaterials and attribs)
  - Point velocities set to Instantenous Point Velocities
- filecache
## 5. Debis source
- this is simulations - results of next frame depend on previous frame
- it does not rely on any rbd data - it's post process thing
- points automatically inherit velocity from source rbd
- can source volume (stamp points mode)
## 6. H17 Convex decomposition sop
- chair example
- decrease max concavity
## 7. H17 Extract rigid transform
- object
- fractures
- animated the whole thing
- on left side timeshift set to first frame and pack prims below
- on right side extract rigid transform - left input from timeshift, right input from animated geo
- below is transform pieces, left input from packed prims, middle input form extract rigid transform
- below create atrib - active
  - intiger
  - class point
  - value $F >= 75 means it's 0 and then turns 1 after frame 75
  - animate animated attrib the opposite way
## 8. Workflow with constraints
- first assemble to create name attribute and connect inside edges
- second assemble to create packed prims (and nothing else)
## 9. To apply pop forces in RBD in dop
- use rigidbodysolver not bullet solver
- plug pop forces into middle input
## 10. To selectively change non active to active
- set i@active=0 after packed primitives in SOP's
- in dopnet create multiple solver
- connect sop solver
  - in sop solver make group (box) selection of the geometry
  - animate the selection
  - attrib wrangle on the group to change i@active to 1
  
  
