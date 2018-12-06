## 1. Add sop 
- can add point, can move it with transform in viewport
- In particles pane can replace points with particles
## 2. Point jitter (quick noise on curves, trails etc)
## 3. Measure 
- can measure geometry curvature
## 4. Attrb promote
- to find min and max attrb value (e.g. curvature) through all the points
- name of the attrib (curvature)
- promote from point to detail
- promotion method max or min
- change original name to curve_max for example
- don't have to delete original
## 5. Trail sop
- compute velocity
  - Velocity Approximation - Central difference - so you get some vel on first and last frame
- connect as polygons with close rows off - makes splines/trails
## 6. Bound SOP
- creates bounding box (geo) around incoming geo
- can add more padding on all axis and directions
## 7. Convertline
- converts mesh to wireframe primitives
- uses width attrib
## 8. Point Jitter
- use on fused geo after convert line to make the wireframe look electric
## 9. Merge SOP
- Cn bring multiple objests at once - use plus button to add more
## 10. Facet
- when edges on boxes look like normals are smoothed
- have to switch "Unique Points"
## 11. Resample
- for curves use Treat Polygon As Subdivision Curves for smoothing result
## 12. Rest
- adds rest attribute that is the position at the start
- useful when you want to color based on initial position
- can add rest normals from drop down
## 13. Time Warp 
- to cycle run/walk animations
## 14. Time blend
- To make slow mo animation of skinned model (no changing topo)
  - time wrap to cycle, e.g 1-55, 1-55 with cycle at start and end
  - time blend (default settings)
  - time wrap to cycle longer loop e.g. 1 - 55, 1 -110 with extend at start and end
## 15. Peak SOP
- pushes points along direction of the normal
## 16. Ray SOP
- to transfer attributes (like Cd) from points on mesh to poins filling volume inside the mesh along mesh normals
  - mesh (with some color)
  - fill with points from volume
  - need normals on the points inside so need to vdb from polygons and vdb analysis (gradient) and then attrib from volume (points inside to the left, vdb analysys to the right
  - ray SOP - original mesh to the right, attrib from vol to the left, transform points off, and import attrib from hits - Cd
## 17. Poly Reduce
- can use attribute (for example @retention) from painted color to make parts of mesh more or less poly reduced
## 18 Boolean
- to delete interior intersections from the geomjust plug geo in the first input, because therenis resolve self intersect geomcheckbox on by default
## 19. Curves
### a) drawcurve
- inside geo node to draw a curve projected to a plane
### b) convert
- to nurbs to smooth the curve
### c) carve
- can use extract (pane) to exctract only one point at time from the curve using first U animation
## 20. split
- splits points into left aright group based on condition
## 21. Grouping curve points
- goup sop, points
```
@curveuv=1
```
- 0  is first point
- 1 is last point
## 22. Smoothing curve
- convert sop - set to nurbs
## 21 Copy Stamp
- copy to points can't do a lot of things
- based on ptnum change bend angle
- have a color specified in points on right side of copy stamp
- have bend sop on the left side that comes to the copy stamp
- on bend angle use stamp function
   - requires: specy which copy node you are using (name), name of the function, default value
  ```
  stamp("../copy1", "bendname", 30)
  ```
- on copy stamp find stamp pane and turn stamp inputs on
  - put the bendname in variable 1 slot
  - put @ptnum in the value
  - or @ptnum * 2
  - or rand(@ptnum) * 100
  - can use fit functions etc
  
## 22. Fuse sop
- can merge points or unmerge points )separate primitives (unique pane)
## 23. Attrib from map sop
- apply texture to point color
## 24. Polyframe sop
- can generate normals, tangents and bitangets on curves
## 25. Straighten
- select faces that should face down if the thing was standing correctly 
- press enter
- model will be rotated
## 26. Axis Align
- puts the bottom of the bounding box at the origin
## 27. Box, sphere
- they have imput
- if you plug any geo in the input - the box will become a bounding box for the geo, and sphere will become bounding sphere for the input geo
## 28. Point deform sop
- get animated geo
- get t-pose geo
- scatter points on the t-pose model
- use point deform sop to transfer the points (1st input) from t- pose (second input) to animated mesh (3rd input)
- use Maximum points setting in point deform (lower it) to make sure that the point match the animated mesh more tightly
## 29. Blend shape
- two meshes with exactly the same topology/number of verts 
- can blend between pose 1 and pose 2 of riggerd/posed character
## 30. SOP SOLVER
- to create growth "algorithm"
- bunch of points
- group some and make @active attribute=1 on the selected group
- sop solver
- inside sop solver add attribute transfer and connect both inputs to the prev frame
- source group @active=0
- destination group @active=0
- attributes (points) active
- source and destination group types set to points
- distance threshold on atrib transfer will dictate how fast the growth is spreading
- the attributes you want to alter in the solver must be initialized before the solbver, not in yhe solver.
  - solver to change the attrib value based on previous frame must use prev frame - and prev frame takes info from outside the solver
- examples http://www.tokeru.com/cgwiki/index.php?title=The_solver_sop
- if reading animated attributes (animated outside the solver sop) you need to use input1 - this fetches geo every frame, unless pre frame that fetches geao only on the first frame
  - have to fetch geo from first input to check if @active is changing for example
## 31. H17 Point velocity sop
- needs mesh with normals
- creates velocity with various options
## 32. H17 Stroke sop
- can draw multiple curves
## 33. Point Replicate sop
- needs points (at least one)
- adds bunch of points around existing point
## 34. Retime sop
- can retime anything, poly, rbd, characters, pyro, flip etc
- best retime from cached files
- pyro
  - interpolation cubic
  - under volumes - blend mode best is advected
  - on top reduce the speed from 1 to 0.1
## 35 Falloff sop
- use group before to select stuff
- three modes
  - surface falloff - will not bleed to the nearby surface if it's not directly connected
  - edge
  - radius (old)
## 36. Graph color sop
- can pick 4 - 5 colors and color prims so none of the same colors are neighbours.
## 37. Hole sop
- when you have grid and bunch of smaller grids where you want to have holes
## 38. Winding number
- see Jeff's illume webinar on top 10 H17
## 39. Clean sop
- remove unused points checkbox removes points that are floating - not attached to mesh in any way
## 40. Attribute randomize
- can set random pscale with a ramp - few big and bunch of small ones
## 41. Instance sop
- packed prim
- doesn't update orient attrib
## 42. Physics painter
- game tools
- to throw bunch of rocks or twigs around
- scatter then simulate and dry the paint
- see this: https://vimeo.com/298265924 at about 25min in
## 43. Gameres sop
- game dev tools sop
- from hi res scan model to low res plus texture bake
## 44. Reverse sop
- reverses normals
## 45. Draw curve sop
- shows a plane that you can draw curve on - you can adjust it - xy, zx, and move it up etc.
## 46. Scatter sop
- to have differently scattered points use $F in seed 
- to have randomly shown on eor 0 points use rand($F) < 0.5 in force total count - will spawn 1 point 50% of time
