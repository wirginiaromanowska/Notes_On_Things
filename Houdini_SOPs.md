## 1. Add sop - can add point, can move it with transform in viewport
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
  - time wrap to cycle
  - time blen
  - time shift to cycle longer loop
