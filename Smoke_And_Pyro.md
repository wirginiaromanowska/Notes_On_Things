## 1. Control amount of detail with shred microsolver
### a) detail on the edges 
- standard setup
- high cutoff (above density top range)
- control settings: firld - density, inluence - 1, range from 1 to 0 (opposite)
- bindings - default
### b) detail in the core - where fast velocities are
- cutoff - 10 times above top range
- control - vel, influence -1, control range from 1 to 0
- bindings: disturb firld is vector field on, disturb field - vel, threshold field density
- allow editing, in disturb vector field: control field node needs to be type vector, after append lenght node
## 2. Gas particle to field
### a) In DOP
- smoke object
- to apply data
- to pyro solver
- sop geo node to second imput of apply data
  - bring the points
  - set to update always
- gas resize fluid dynamic to second imput of smoke solver
- gas particle to field to second imput (merge with the one above)
  - destination field is fuel or temperature or velocity
  - vel goes to vel update in solver (3rd imput)
  - attribute fuel, temp, vel (or v if it's name that way on the geo)
  

- provide sop path
```
`opimputpath("../",0)`
```
## 3. Rules and Advice
- avoid transforms at the object level (for emitters, colliders etc) in case you need to scale whole sim from cm to m later
- when there is error in DOPs
  - right click on node will clear the error
  - you can see what error says only in tree view (right click)
  - vel is non divergent - so will not expand or shrink - this is why it needs to go to vel update input int he pyro solver
  - only vel that can go in pre-solve imput in pyro solver is curl noise
  - how you mix in vel matters
    - try to set it to maximum instead of add
## 4. Fast moving trails
- trail SOP: preserve original, trail lenght 5 (frames)
- add SOP: under poligons by group, by attribute, and attribute is id
- resample with max segments set to what would be max substeps
- point jitter - makes it more noise
- wire this directly to DOPnet
## 5. Pyro solver parameters
- boyancy lift - takes direction * amount of boyancy * current temperature and adds that to current vel

