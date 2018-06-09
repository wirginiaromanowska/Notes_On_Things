## 1. Non-commercial - size limit to 1920 x 1080
## 2. Nodes
- Layer Contact Sheet - to see all image planes at once
- shuffle to separate image planes
## 3. Image Planes
- background
- difusse
- gi
- emission
- refract
- reflect
- spec
## 4. To comp beauty pass
- add above planes using PLUS node
## 4. DOF 
- [https://vimeo.com/87174825]
- separate from exr using shuffle
- shuffle copy 
  - input 1 - beauty comp/pass
  - input 2 - z plane
- use ZDefocus node
  - second input
  - depth channel - depth.Z
  - focus plane - where the focus is (can nimate
  - depth of field - how wide is the focus plane (bigger numbers = more stuff will be sharp, smaller numbers = DOF will be very narrow)
  - size - how blurry
  - maximum - max blurr at fruther away distance (background)


