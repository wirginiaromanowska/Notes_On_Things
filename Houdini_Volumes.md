## 1. Types of volumes
### a) vdb
- sdf (signed distance field) - good for collisions etc
  - 0 on the surface
  - negative outside
  - positive inside
  - it's opposite of native Houdini volumes
- fog - cheaper
- vdb from polygons can source v from points to vel volume (Vector type needs to be Velocity)
- can store vector fields
- almost always more memory eficient
- empty voxels inside and outside are not stored
### b) houdini volume (dense), e.g. iso offset
- fog
- sdf (Signed Distance Field)
  - each voxel stores value that means how close it is to the surface
  - surface = 0
  - inside - negative
  - outside - positive valueas
### c) heighfield 
- is dense volume
## 2. VDB
- see vdb volumes fields/groups manipulation here: https://vimeo.com/272793390 at 46 min
- created by VDB from polygons- to create volume source for pyro sim
  - can add surface attributes as new volumes in the same VDB
  - point.v, VDB name vel
  - density is created by default
- blast can delete volume by group e.g. density
- use name sop to rename volume fields (groups)
- can use merge to merge back different fields/groups into one volume
## 3. Creating
- Iso offset - from polys
## 4. Visualizing
- Volume visualisation SOP
  - doesn't change anything, just changes how this looks in viewport
  - Density scale 10
## 5. Operations
- Volume mix
  - when changing "post multiply" you actually change the data stored int he voxels
## 6. Cloud and cloud noise SOPs
- vdb volume
- byaanimating time in advection pane in cloud noise sop you can make animated puff without simulation
- build low res then kick the res to 300
## 7. S. K. Create vel volume
- Bound sop around your geo + some padding
- volume Sop named vel, vector
- volume vop with bind export vel 3 floats (vector)
- aaflow noise

  
  
  
