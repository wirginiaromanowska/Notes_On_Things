# houdini

Links:

1. [MATH - rotation using sin cos](https://www.siggraph.org/education/materials/HyperGraph/modeling/mod_tran/2drota.htm)
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


2. [MATH - sphere using sin and cos](http://mathworld.wolfram.com/Sphere.html)
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
