## 1. Redshift Vops tips
- Vector from float - use Color Maker node
## 2. Setup for AOV Z-Depth:
- turn off progressive rendering in IPR pane
- use render view pane to preview the AOV's
- fon Nuke set to Min Depth
## 3. Formula for the beauty pass from AOV's
- Beauty = DiffuseFilter*DiffuseLightingRaw + DiffuseFilter*GlobalIlluminationRaw + DiffuseFilter*SubsurfaceScatteringRaw + SpecularLighting + Reflections + Refractions + Emission + Caustics
- If using "Caustics Raw" instead of "Caustics", these would have to also be multiplied by "Diffuse Filter".
- (Redshift Doc)[https://docs.redshift3d.com/display/RSDOCS/AOV+Tutorial?product=houdini]
## 4. Toon
### a) For interior edges on SIMPLE geometry 
- good for box with no subdivisions
- in SOPs append polypath after the box
- then poliwire SOP with desired width
- apply black non reflective edge material
### b) For interior eges on SUBDIVIDED geometry
- use Group sop to group the (type) Edges, keep by Normals on and adjust spread angle (for box 0)
- Include by Edges enabled, with min edge angle 45 
- then group promote SOP, promote from edges to points
- delete (by non selected) the new point group with Delete SOP
- another Delete SOP to keep points only
- connect adjacent pieces SOP in adjacent points mode, adjust search radius
- polywire SOP
- apply black non reflective edge material
### b) For exterior edges
- in RS material
- Frenel
- ramp set to alt black and white close together
- this needs to be part of emissive and diffuse color
- this needs to go directly in refl color (so no reflections where black edge is)   
### c) For "shadows"
- in RS material
- Ambient Occlusion
- Part of Diffusse and Emission
### d) For toon light
- In obj level create RS light (point)
- in SOP's
- need Normals on this geo so add Normal sop
- redshift doesn't like attribute named N so rename the N to new_N using rename SOP
- in RS Material
- RS Vertex Attribute - new_N and normalize it
- RS User Data Vector - copy relative ref from RS light pos to Default, normalize the vector
- RS Math Dot Vector the two above
- RS Ramp in alt mode - make the interpomation linear and pick three colors
- Mult this vector with AO vector and Frenel from above
- plug in Diffusse and Emissive
## 5. Rendering MotionBlur
- Make sure you have v (velocity) attribute on the sop you are rendering, if not add trail sop and set it to calculate velocity.
- Add redshift parms to your geo (obje parms from redshift shelf). Check checkboxes RedshiftOBJ/Render
  - all three to do with motion blurr on
  - deformations blur from velocity atribute
 - In Redshift ROP under Redshift/Motion Blur switch all three checkboxes to do with motion blur
## 6. Camera
- Use null to spin camera around subject
## 7. RenderView 
- the pane next to scene pane
- can take a snapshot of the previous render for comparison (camera button at the bottom)
## 8. Redshift and Particles
- by defaoult nothing renders
- use instance geo node and sphere
  - get inside and delete add, 
  - object merge the particles
  - in properties Instance Object is the sphere (or whatever shape are the particles)
  - instance heo node needs to have redshift parms added (from shelf) and in Redshift Obj/Instancing change Instancing using to Redshift Point Clouds
- material must be assigned to the instanced object (i.e. sphere), not to intancing geo node
- motion blur on particles:
  - instance needs to have rs object parms, but motion blur there is on by default
  - in redshift ROP go to redshift/Motion Blur and enable Motion Blur
## 9. Bringing attributes from geo to rs material
- particle attribute lookup = rs point attribute
- rs user data color
- for instanced particles you need to make sure that Cd (or other attributes) are transfered in the instance geo node (otherwise they will not be read in rs material)
## 10. Better instancing
- attrib wrangle after particles/points
```
f@pscale = 0.01; // set the pscale
int rand_num = ceil(rand(@id) *3); //generating random number based on particle id, number is between 0 and 3, so we round it up with ceil function, because we have three meshes to pick from to instance to the points
s@instance = "/obj/pig" + itoa(rand_num); // @instance is a special attribute to let redshift know to instance the thing. it needs path to object level. On obj level we have three pig heads (with names pig1, pig2 and pig3)
```
## 11. Noise
- increase samples
- if floor is noisy (from light/shadow), need to increase Brute Force GI rays
- try irradiance cache with increased rays
- more info https://github.uconn.edu/pages/mjr14019/redshift-docs/render-options/noise/
## 12. Rays and sampling
- primary rays 
  - from camera throught every pixel
  - to have smooth anti-aliased edges dof and motion blur need to have multiple rays through on epixel
- secondary rays
  - from each primary ray hitting any rendering surface shoot secondary rays to define color to render on that surface, looking fo rlights, reflections etc.
  - total rays = primary rays * secondary rays
- in redshift where unified smpling is - this is only for primary rays
- redshift shoots minimum rays (min samples) and shoots more rays either until max samples or if the threshold i slower than specified
- lower the sample threshold to get less noise
- samples on a light - are secondary rays
- brute force gi rays - are secondary rays
- if you have noise where light turns to shadow up the samples on the light
## 13. DOF - get the focus distance 
- if not using houdini camera focus distance
  - click on camera, press enter
  - right click on the camera handle and change to focus handle
  - can move the pink box in viepoert - this is where focus is
## 14. RS material blender
- blend between two materials (vefore going to output node in RS material)
## 15. Rendering particles - new way
- in redshift obj parms
- render object as particles
- set up the pscale to something small
## 16. Creating materials in mat context
- for particles/mesh materials:
  - create RS Material Builder
  - dive inside
  - create basic rs material and connect to out surface
- for volume materials
  - rs material builder
  - dive in
  - volume and plug in volume out
## 17. Basic rop setup
- global ilum - brit force
- optimisations increase reflect, refract and combined to 8, 8, 16
- in sampling options max samples to 512


