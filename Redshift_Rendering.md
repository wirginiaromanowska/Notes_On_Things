## 1. Redshift Vops tips
- Vector from float - use Color Maker node
## 2. Setup for AOV Z-Depth:
- turn off progressive rendering in IPR pane
- use render view pane to preview the AOV's
## 3. Formula for the beauty pass from AOV's
- Beauty = DiffuseFilter*DiffuseLightingRaw + DiffuseFilter*GlobalIlluminationRaw + DiffuseFilter*SubsurfaceScatteringRaw + SpecularLighting + Reflections + Refractions + Emission + Caustics
- If using "Caustics Raw" instead of "Caustics", these would have to also be multiplied by "Diffuse Filter".
- (Redshift Doc)[https://docs.redshift3d.com/display/RSDOCS/AOV+Tutorial?product=houdini]
## 4. Toon
- use AO and Curvature in order to achieve a ink/sketch style render
