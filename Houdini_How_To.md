## 1. Slacking wires
- draw cyrve
- attrib wrangle to delete random points except first and last
```
if(@ptnum != 0 && @ptnum != @numpt - 1 && rand(@ptnum) > ch("amount")) removepoint (0, @ptnum);
```
- convert line sop to separate the segments of the line in to separate primitives + also gives restlenght
- for each primitive loop
  - reasmple 4 segments
  - blast middle point (no 2)
  - attrib promote from prim to point restlenght
  - attrib wrangle, affect point grou 1 and 2
  ```
  @P.y -= ch("amount") * @restlenght;
  ```
- resample after the loop
  - swicth off max segment lenght 
  - switch on mas segments 25
  - treat polygons as subdivision curves
- to add randomness
  - in for each begin use create meta import node button
  - that node gives detail attribute for each iteration
  - pipe that node to second imput in the warngle in the loop
  - back in wrangle in the loop
  ```
  int iteration = detail(1, "iteration"); // imports iteration detail attribute from second stream
  
  int seed = chi("seed");
  float random = fit01(rand(iteartion + seed), 1, 3);
  
  @P.y -= ch("amount") * @restlenght * random;
  ```
  ## 2. Apply image color to Cd
  - mesh needs to have some UV's
  - in point vop place uvcoords
  - colormap (connect u and v)
  - colormap to Cd
