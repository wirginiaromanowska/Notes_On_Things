## 1. Pressure
- stiffness 
  - for epheres higher it it the more bouncy the thing is
## 2. Accuracy and artefacts
- increase substeps
## 3. Weld
- stitches for cloth
- if @weld = -1 the stitches are gone
## 4. Vellum post process
- to smooth out
- can add after sim cache to disc
- this is what can transfer low res sim to high res render
## 5. Detangle
- needs pscale attrib
- needs rest pos (old pos) that doesn't intersect with collision geo
  - can just transform out of the way
  - create attrib OlpPos and transfer it to the not transformed geo
## 6. Vellum solver
- can go inside and add pop wind and pop fluid even if this is after vellum configure cloth
## 7. cloth
- in cloth constraints you can pin to animation - just select the verts
- always check the thickness in cloth solver visualize
  - if it's too thick - spheres overlap then sim is going to explode
  - too thin - collision problems
  - spheres - pscale
## 8 Hair
- use draw curve to draw few strokes
- then go to shelf and use hair
## 9. Vellum ballon
- torus and go to vellum shelf
## 10. Soft body
- from shelf
- construcs constraints works on any type f geo - might be better than tetrahydral geo
## 11. Vellum grains
- from shelf
- needs more substeps (at least 5 times more)
## 12. simple cloth tool (flag example in masterclass)
- from shelf
- on sop level
- asks for cloth
- asks for collision
- cloth solver
  - this is where the ground plane is defined (checkbox)
  - forces like wind etc are in there too
 - clothe constraints
  - this is where pin point can be selected
  - use the arow
## 13. Vellum attach
- after cloth constraints
- before cloth solver
- use max distance to attach closest points to collision geometry
- or select a group of points to attach
## 14 cloth_io
- simmilar like dop_io
- saving files to disk
- constraints as packed geo
- saves both geo and constraints (2 files per frame)
- constraints ar enot static, change per frame - updated by the solver
## 15. postprocess
- subdiv
- smoothing
- add thicknes extrude
- visualisation options
- falls color mode
## 16. Friction
- to make things (cloth) more sticky - increatse statick threshold in forces pane in vellum solver to 10 (goes over 1)

  

