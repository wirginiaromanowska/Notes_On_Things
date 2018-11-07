## 1. Slacking wires
- draw curve
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
  - uv's are vertex attrib where Cd is point attrib
    - either run point vop over verts
    - promote uv to be point attrib (method first match to avoid sims?)
## 3. Cut out bacon shape from bacon texture
- in geo context put down copnet
 - method set to volume slice
 - dive in and put down file
 - file bacon.jpg
- traces op
  - link the above cop in the cop path
  - lower down the trheshold
  - produces outline with few holes
  = Add point texture checkbox on for later
- measure sop after trace sop 
  - to measure and remove tiny holes
  - set type to area
  - adds @area atribute - can see it in spreadsheet - two big areas (bacon) and bunch of tiny (holes)
- blast
  - group type primitive
  - @area>0.1
  - delete non-selected
- resample to have less points
- planar patch from curve
  - resample curves on
  - interior edge lenght 0.02
- UV quickshade
  - bacon.jpg
 

  
  
  
