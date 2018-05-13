# houdini

Links:

1. [MATH - rotation using sin cos](https://www.siggraph.org/education/materials/HyperGraph/modeling/mod_tran/2drota.htm)
* rotated_x = x cos f - y sin f
* rotated_y = y cos f + x sin f
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


2. [MATH - sphere using sin and cos](http://mathworld.wolfram.com/Sphere.html)
* x	=	r * cos f * sin t
* y = r * sin f * cos t
* z = r * cos t
* r - radius
* f, t - angles
