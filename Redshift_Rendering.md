## 1. Redshift Vops tips
- Vector from float - use Color Maker node
## 2. Setup for AOV Z-Depth:
- turn off progressive rendering in IPR pane
- use render view pane to preview the AOV's
## 3. Formula to pu the beauty pass together from AOV's
- Beauty = DiffuseFilter*DiffuseLightingRaw + DiffuseFilter*GlobalIlluminationRaw + DiffuseFilter*SubsurfaceScatteringRaw + SpecularLighting + Reflections + Refractions + Emission + Caustics
- Please note that if we were using "Caustics Raw" instead of "Caustics", these would have to also be multiplied by "Diffuse Filter".
- (Redshift Doc)[https://docs.redshift3d.com/display/RSDOCS/AOV+Tutorial?product=houdini]
