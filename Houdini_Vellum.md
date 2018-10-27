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
## 5. Detangle
- needs pscale attrib
- needs rest pos (old pos) that doesn't intersect with collision geo
  - can just transform out of the way
  - create attrib OlpPos and transfer it to the not transformed geo
  
