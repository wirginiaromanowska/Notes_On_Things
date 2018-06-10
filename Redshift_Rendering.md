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
- use AO and Curvature in order to achieve a ink/sketch style render
## 5. Rendering MotionBlur
- Make sure you have v (velocity) attribute on the sop you are rendering, if not add trail sop and set it to calculate velocity.
- Add redshift parms to your geo (obje parms from redshift shelf). Check checkboxes RedshiftOBJ/Render
  - all three to do with motion blurr on
  - deformations blur from velocity atribute
 - In Redshift ROP under Redshift/Motion Blur switch all three checkboxes to do with motion blur


