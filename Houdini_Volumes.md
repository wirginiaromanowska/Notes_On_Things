## 1. Types of volumes
- vdb
  - sdf (signed distance field) - good for collisions etc
  - fog - cheaper
- houdini volume (dense
- heighfield is dense volume
## 2. VDB
- see vdb volumes fields/groups manipulation here: https://vimeo.com/272793390 at 46 min
- created by VDB from polygons- to create volume source for pyro sim
  - can add surface attributes as new volumes in the same VDB
  - point.v, VDB name vel
  - density is created by default
- blast can delete volume by group e.g. density
- use name sop to rename volume fields (groups)
- can use merge to merge back different fields/groups into one volume
  
  
  
