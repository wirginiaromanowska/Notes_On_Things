## 1. Particles
- points with attributes
  - P
  - v
  - force - vector
  - life - set in the source by life expetancy
  - age - how long it is currently alive, not normalized, still in seconds
  - id (unique)
  - dead - can be set in POP wrangler
## 2. POP network
### a) popobject - particle bucket
- some physical properties
### b) popsolver - moves particles around
### c) POP source
- can source only from selected group of polys
- spawn by attribute
- Impulse Activation 1, then Impulse count means spawn n particles every simulation frame (default every frame)
- Constant Activation 1, then Const Birth Rate means spawn n particles every second
- Life expectancy is particle life in seconds
- Life Variance + or - in seconds
- Inherit attributes from geo from where particles are spawning, like velocity or color
- in Attributes panes can set velocity - that's initial velocity
## 3. Popforce
- can display vecttors in vieport when guide is on
- two popforces - vectors will add
- has noise built in
## 4. Pop location
- birth
- velocity
## 5. Problems
- geo with material/texture on it will spawn black square particles when used in POP. To solve attribute delete, primitive attribute/shop material path on the geometry
- access geometry spreed sheet in the DOP network by going in the spreed sheet/tree view on left side in popobject/geometry
## 6. POP Wrangle
- plugs below particle cource
- @dead = 1; - kills all particles



  
