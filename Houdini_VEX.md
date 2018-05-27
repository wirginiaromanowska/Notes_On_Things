## 1. Writing VEX
- alt+E to open external editor
- generally all attributes initialize to 0 by default
- color initializes to 1, 1, 1 by default
- normal @N - computes surface normal when initialized
## 2. Add point
```
addpoint(0, @P);
addpoiny(0, {0, 0, 0});
```
- does not return a value, but creates a point
- addpoint(geometry_string, position)
```
int newpt = addpoint(0,{0, 0, 0))
```
- returns a value
## 3. VEX Attributes (from Entagma)
### a. General
- int @ptnum Point Number
- int @numpt Total number of points
- float	 @Time 	 Current time, in seconds
- float	 @TimeInc	 Time increment per frame in seconds
- float	 @Frame	 Current frame
- int @primnum Primitive Number
- int @numprim Total number of primitives
- int @vtxnum Vertex number
- int	 @numvtx	 Total number of vertices
### b. Geometry
- vec3	 @P	 Point/Primitive Position
- vec3	 @N	 Point/Primitive/Vertex Normal - to initialize normals @N = @N
- vec3	 @v	 Velocity (e.g. for motion blur / in particle systems)
- float	 @pscale	 Uniform scale. Used in copy-SOP or particle systems
- vec3	 @scale	 Non-Uniform scale. For use see pscale
- vec3	 @up	 Up-Vector. Used together with @N to orient point/particle/instance
- vec4	 @orient	 Quaternion defining the rotation of a point/particle/instance
- vec4	 @rot Quaternion defining additional rotation
- vec3	 @trans	 Translation of instance
- matrix	 @transform	 Transformation matrix (used e.g. in Copy-SOP)
- vec3	 @pivot	 Local pivot point for instance
- float	 @lod	 Detail/Primitive Level of detail
- vec3	 @rest	 Rest position
- vec3	 @force	 Force (e.g. acting on particle)
- float	 @age 	 Particle Age
- float	 @life Max. Particle Life
### c. Volumes
- float	 @density	 Density of voxel
- int	 @ix, @iy, @iz	 Voxel indices along each axis. Ranging from 0 to resolution-1
- vec3	 @center	 Center of current Volume
- vec3	 @orig	 Bottom left corner of current Volume
- vec3	 @size	 Size of current Volume
- vec3	 @dPdx	 Change in position to get from one voxel to the next in x direction
- vec3	 @dPdy	 Change in position to get from one voxel to the next in y direction
- vec3	 @dPdz	 Change in position to get from one voxel to the next in z direction
- vec3	 @BB relative position inside bounding box. Ranging from {0,0,0} to {1,1,1}
### d. Shading
- vec3	 @Cd	 Diffuse Color
- float	 @Alpha	 Alpha transparency
- vec3	 @uv Point/Vertex UV coordinates
- vec3	 @Cs Specular Color
- vec3	 @Cr Reflective Color
- vec3	 @Ct Transmissive Color
- vec3	 @Ce Emissive Color
- float	 @rough 	 Roughness
- float	 @fresnel 	 Fresnel coefficient
- float	 @shadow 	 Shadow intensity
- float	 @sbias 	 Shadow bias
### e. Used As Instancing Point Attribute in Copy-To-Point-SOP
- vec3	 @P	 Instance Position
- float	 @pscale	 Uniform scale
- vec3	 @scale	 Non-Uniform scale
- vec3	 @N	 Normal (+Z axis of the copy, if no orient)
- vec3	 @up	 Up-Vector. Used together with @N to orient instance (+Y axis of the copy, if no orient)
- vec4	 @orient	 Quaternion defining the rotation of a point/particle/instance
- vec4	 @rot Quaternion defining additional rotation (applied after @orient)
- vec3	 @v	 Velocity (motion blur, also used as +Z axis of the copy if no orient or N is present)
- vec3	 @trans	 Translation of instance
- matrix	 @transform	 Transformation matrix (used e.g. in Copy-SOP)
- vec3	 @pivot	 Local pivot point for instance
## 4. Transform and pivot 
### a) set to center
- (-$CEX) (-$CEY) and (-$CEZ) in Trandlate
- $CEX $CEY and $CEZ in Pivot Translate
### b) have bottom on the floor
- in Center Y: ch("sizey")/2
## 5. Variable types
```
int someNameA = 5;
float someNameB = 2.3;
string someNameC = "Coolbert";
vector someNameD = {2.5, 1.7, 10.5}
```
## 6. Random
```
float pscale = rand(@ptnum);
vector direction = rand(@ptnum); //will create rand float for x, y and z direction
```
## 7. Channel Reference
```
float slider = chf("Name_Of_Slider");
```
## 8. Fit Function
```
fit(direction, {0, 0, 0}, {1, 1, 1}, {-1, -1, -1}, {1, 1, 1});
fit01(direction, {-1, -1, -1}, {1, 1, 1});
```
- fit(Variable_To_Fit, OldMin, OldMax, NewMin, NewMax)
- fit01(Variable_To_Fit, NewMin, NewMax) - assumes old min and max are 0 and 1

## 9. Reading attribute from second input in wrangle
### a) Using point function
- use with different geo (grid and sphere)
- point(Imput_Number, Name_Of_Attribute, Point_Number)
```
vector pointpos = point(1, "p", 0);
vector pointpos = point(1, "P", @ptnum);
```
### b) Wagner way 
- use if points match 1:1 (e.g. grid and grid etc)
- if it's not input 0 then have to declare with variable type (f, v, i s etc)
```
@P // fetch point position from first imput
v@opinmut1_P // fetch attribute from second input

f@foo // fetch first input foo
f@opinput1_foo // fetch second input foo
```
### c) Accessing attrib of detail when running wrangle over points
- by default you can access only type of attribute the wrangle runs over
```
float max_curvature = detail(1, "curvature_max", 0);
```
### d) getattribute or getattrib functions (see Houdini help)
## 10. Interesting VEX functions
```
vector frequency = chv("Frequency");
vector offset = chv("Offset");

vector dir = curlnoise((@P * frequency) + offset);
```
- curlnoise function - perlin
- curlxnoise function - simplex
## 11. Arrays
- accessing myArray[element_number] = value
```
myArray[1] = 42;
```
## 12. If
- short version
```
int condition = (@P.x > 0) ? 1: 3;
@Cd = set(condition, 0, 0); // write condition to red color
```
## 13. Color
- by default initialized to 1, 1, 1
- if chenging only @Cd.x = variable, then assume that G and B are white
- have to manually initialize the color first to black @Cd = {0, 0, 0}
- or can work on color as vector @Cd = (variable, 0, 0), not @Cd.x = variable
