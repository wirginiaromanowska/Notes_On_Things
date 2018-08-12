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
## 13. Time Warp 
- to cycle run/walk animations
## 14. Time blend
- To make slow mo animation of skinned model (no changing topo)
  - time wrap to cycle, e.g 1-55, 1-55
  - time blend (default settings)
  - time wrap to cycle longer loop e.g. 1 - 55, 1 -110
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
  
