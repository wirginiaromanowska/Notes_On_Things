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
- provide sop path
```
`opimputpath("../",0)`
```
## 3. Rules and Advice
- avoid transforms at the object level (for emitters, colliders etc) in case you need to scale whole sim from cm to m later
## 4. Fast moving trails
- trail SOP: preserve original, trail lenght 5 (frames)
- add SOP: under poligons by group, by attribute, and attribute is id
