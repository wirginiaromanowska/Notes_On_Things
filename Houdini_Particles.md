## 1. Particles
- points with attributes
  - P
  - v
  - force - vector
  - age
  - id (unique)
## 2. POP network
- popobject - particle bucket
  - some physical properties
- popsolver - moves particles around
- POP source
  - can source only from selected group of polys
  - spawn by attribute
  - Impulse Activation 1, then Impulse count means spawn n particles every simulation frame (default every frame)
  - Constant Activation 1, then Const Birth Rate means spawn n particles every second
  - Life expectancy is particle life in seconds
## 3. Popforce
- can display vecttors in vieport when guide is on
- two popforces - vectors will add
- has noise built in
## 4. Pop location
- birth
- velocity
## 5. Problems
- geo with material/texture on it will spawn black square particles when used in POP. To solve attribute delete, primitive attribute/shop material path on the geometry



  
