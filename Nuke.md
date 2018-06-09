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
- shadows
- ao
## 4. To comp beauty pass
- add above planes using PLUS node, then mult shadows and ao on top
## 4. DOF 
- in redshift zdepth values are saved in meters (so everything that's fruther away than 1 meter will show up white)
- [https://vimeo.com/87174825]
- separate from exr using shuffle
- shuffle copy 
  - input 1 - beauty comp/pass
  - input 2 - z plane
  - set top left to rgba and select diagonally first under r, second down under g, third down under b and fourth under a
  - set lower right to be depth and select only top for r
- use ZDefocus node
  - second input
  - depth channel - depth.Z
  - focus plane - where the focus is (can nimate
  - depth of field - how wide is the focus plane (bigger numbers = more stuff will be sharp, smaller numbers = DOF will be very narrow)
  - size - how blurry
  - maximum - max blurr at fruther away distance (background)
 


