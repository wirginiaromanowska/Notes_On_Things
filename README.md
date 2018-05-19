# houdini

## 1. Circle
* Attrib Wrangle run over Detail (only once)
```
vector pos = set(0, 0, 0);
int new_prim = addprim(0, "polyline");

for(float angle = 0; angle < (PI * 2); angle+= 0.01){
    float x = cos(angle);
    float y = sin(angle);  
    
    pos = (set(x, y, 0));
    int new_pt = addpoint(0, pos);
    addvertex(0, new_prim, new_pt);
}
```
## 2. Spyro
```
vector pos = set(0, 0, 0);
int new_prim = addprim(0, "polyline");

for(float angle = 0; angle < (PI * 10); angle+= 0.01){
    float x = cos(angle) * angle;
    float y = sin(angle) * angle;  
    
    pos = (set(x, y, 0));
    int new_pt = addpoint(0, pos);
    addvertex(0, new_prim, new_pt);
}
```
## 3. Waves
```
vector pos = set(0, 0, 0);
int new_prim = addprim(0, "polyline");

for(float angle = 0; angle < (PI * 10); angle+= 0.01){
    float x = cos(angle) + angle;
    float y = sin(angle);  
    
    pos = (set(x, y, 0));
    int new_pt = addpoint(0, pos);
    addvertex(0, new_prim, new_pt);
}
```
## 4. Two Circles Adding
```
vector pos = set(0, 0, 0);
vector pos2 = set(0, 0, 0);
int new_prim = addprim(0, "polyline");
int new_prim2 = addprim(0, "polyline");

for(float angle = 0; angle < (PI * 2); angle += 0.0001){
    // 1st circle
    float firstCircleX = cos(angle);
    float firstCircleY = sin(angle);
    // 2nd circle
    float secondCircleX = (1.0f/16.0f) * cos(angle * 8.0f + @Time * 0.2f);
    float secondCircleY = (1.0f/16.0f) * sin(angle * 8.0f + @Time * 0.2f); 
    // 3rd circle
    float thirdCircleX = (1.0f/64.0f) * cos(angle * 4096.0f);
    float thirdCircleY = (1.0f/64.0f) * sin(angle * 4096.0f);

    // first circle
    pos = (set(firstCircleX, firstCircleY, 0));
    // second circle
    pos = (set(secondCircleX, secondCircleY, 0));
    // first circle + second circle
    pos = (set(firstCircleX+secondCircleX, firstCircleY+secondCircleY, 0));

    int new_pt = addpoint(0, pos);    
    addvertex(0, new_prim, new_pt);
}
```
## 5. Many Circles Adding (Frequency Cancel Anim)
```
vector pos = set(0, 0, 0);
vector pos2 = set(0, 0, 0);
int new_prim = addprim(0, "polyline");
int new_prim2 = addprim(0, "polyline");

for(float angle = 0; angle < (PI * 2); angle += 0.001){
    // 1st circle
    float firstCircleX = cos(angle);
    float firstCircleY = sin(angle);
    // 2nd circle
    float secondCircleX = (1.0f/16.0f) * cos(angle * 8.0f + @Time * 0.2f);
    float secondCircleY = (1.0f/16.0f) * sin(angle * 8.0f + @Time * 0.2f);
    // 3nd circle
    float thirdCircleX = (1.0f/16.0f) * cos(angle * 8.0f - @Time * 0.2f);
    float thirdCircleY = (1.0f/16.0f) * sin(angle * 8.0f - @Time * 0.2f);
 
    // first circle
    pos = (set(firstCircleX, firstCircleY, 0));
    // second circle
    pos = (set(secondCircleX, secondCircleY, 0));
    // first circle + second circle
    pos = (set(firstCircleX+secondCircleX, firstCircleY+secondCircleY, 0));
    
    // first circle + second circle + third circle
    pos = (set(firstCircleX+secondCircleX+thirdCircleX, firstCircleY+secondCircleY+thirdCircleY, 0));
    
    int new_pt = addpoint(0, pos);  
    addvertex(0, new_prim, new_pt);
}
```
## 6. Elipsoid Anim
```
vector pos = set(0, 0, 0);
vector pos2 = set(0, 0, 0);
int new_prim = addprim(0, "polyline");
int new_prim2 = addprim(0, "polyline");

for(float angle = 0; angle < (PI * 64); angle += 0.001){
    // 1st circle
    float firstCircleX = cos(angle);
    float firstCircleY = sin(angle);
    // 2nd circle
    float secondCircleX = cos(angle * 0.0625 * @Time) * 2;
    float secondCircleY = sin(angle * 0.0625 * @Time);

    // first circle
    pos = (set(firstCircleX, firstCircleY, 0));
    // second circle
    pos = (set(secondCircleX, secondCircleY, 0));
    // first circle + second circle
    pos = (set(firstCircleX+secondCircleX, firstCircleY+secondCircleY, 0));    
    
    int new_pt = addpoint(0, pos);      
    addvertex(0, new_prim, new_pt);
}
```
## 7. Elipsoid Rotation
[MATH - rotation using sin cos](https://www.siggraph.org/education/materials/HyperGraph/modeling/mod_tran/2drota.htm)
* Attrib Wrangle run over Detail (only once)
```
vector pos = set(0, 0, 0);
int new_prim = addprim(0, "polyline");

for(float rotangle = 0; rotangle < 2 * PI; rotangle += 0.1){
    for(float angle = 0; angle < 2 * PI; angle += 0.01){
        
        // 1st circle
        float firstCircleX = cos(angle) * 2;
        float firstCircleY = sin(angle);
    
        float rotatedAngle = rotangle;
        float rotatedX = firstCircleX * cos( rotatedAngle ) - firstCircleY * sin( rotatedAngle );
        float rotatedY = firstCircleY * cos( rotatedAngle ) + firstCircleX * sin( rotatedAngle );
           
        // first circle
        pos = (set(firstCircleX, firstCircleY, 0));
        // first circle (rotated)
        pos = (set(rotatedX, rotatedY, 0));
    
        
        int new_pt = addpoint(0, pos);     
        addvertex(0, new_prim, new_pt);
    }
}
```
## 8. Sphere
[MATH - sphere using sin and cos](http://mathworld.wolfram.com/Sphere.html)
```
vector pos = set(0, 0, 0);
int new_prim = addprim(0, "polyline");

for ( float theta = 0.0f; theta < PI * 2.0f; theta += 0.1 ) {
    for ( float phi = 0.0f; phi < PI * 2.0f; phi += 0.1 ) {
        float x = cos( theta ) * sin( phi );
        float y = sin( theta ) * sin( phi );
        float z = cos( phi );

        pos = (set(x, y, z));
        int new_pt = addpoint(0, pos);
        addvertex(0, new_prim, new_pt);
    }
}
```
## 9. Add Point Attributes
```
vector pos = set(0, 0, 0);

float loops_f1 = chf("Loops_Frequency_1");
float loops_f2 = chf("Loops_Frequency_2");
float loops_f3 = chf("Loops_Frequency_3");

vector loops_spread = chf("Loops_Spread");
float loop_offset = chf("loop_Offset");

float max_iter = chf("Max_Iterations");
int new_prim = addprim(0, "polyline");

for(float angle = 0; angle < max_iter; angle+= 0.01){
    float x = cos(angle * loops_f1) * (angle/loops_spread) + (angle/loop_offset) ;
    float y = sin(angle * loops_f2) * (angle/loops_spread) ;
    float z = cos(angle * loops_f3) * (angle/loops_spread) ;
    
    vector loops_norm = set(angle/max_iter, angle/max_iter, angle/max_iter);
        
    pos = (set(x, y, z));
    int new_pt = addpoint(0, pos);
    addvertex(0, new_prim, new_pt);
    
    vector color = loops_norm;
    setpointattrib(0, "Cd", new_pt, color);
    
    vector thinkness = loops_norm;
    setpointattrib(0, "width", new_pt, thinkness);
}
```
10. Random notes:
- Ocean tools usee fft (fast fourier transforms) and points - points can be scattered on any surface and they can have orientation - ocean doesn;t have to be flat
20. Flip Tank - can use sucktion force on colliders to make them look like water is falling of them 
21. Favourite looks filters:
- Blockbuster - Classinc Tension (blur on the edges)
- Bloockbuster Cool - Classic Zombies
22. Adobe Media Encoder settings to export 4k HDR video to vimeo
23. Funny gifs: 
- [this is not how it works(https://media1.tenor.co/images/71e4d7f011bfeafc9b4c5d5e393d48ee/tenor.gif?itemid=5332816)
- Blockbuster Warm - Harford Pills
