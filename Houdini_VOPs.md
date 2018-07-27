- there are cool patterns, not just noises. Search for pattern
## 2. Noisses
- aa flow noise - range from -0.5 to 0.5
- 1D noise for color means it will output float do gray color only, 3D noise will be colorfull
- 4D input
  - before connecting noise you can choose it to have 4D inmput - this is when you wand position and time as input (for aaflow noise for example)
  - use vector to vector 4 to combine pos and time into one vector
- turbulence - adds more detail to noise - subdividing main noise area into smaller fractal areas of noise
- frequency is not the same - this changes overal size of detail.
## 3. Parameter VOP
- create new attributes
## 4. Bind Export
- export attributes
## 5. Compliment
- makes 1-the thing (for example normalized age to feed to pscale if you want particles to get smaller with age)
## 6. Clamp
## 7. Random
- gives rand number from 0 - 1, can based on id for particles or ptnum for meshes
## 8. Power
- use if you want to change distribution (in size for example). Many small particles and only few big ones
## 9. Add const
## 10. Alpha
- bind export Alpha per point will render alpha (transparency)
## 11. Turbulent noise (1d) To have more variation in vel
- multiply with existing vel
- amplitude higher (8)
- frequency higher (more detail)
## 12. dot product
- compares two vectors
- if direction is the same or close you get 1 or close
- if direction is opposite you get -1
- if they are perpedicular you get 0
## 13. cross product
- needs two vectors
- gives vector perpedicualr to the two vectors
## 14. Quaterions
- needs axis (vector) aroun which to rotate
- needs angle - how much to rotate

