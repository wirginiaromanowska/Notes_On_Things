- U to go up
- node graph/view/show dependencies for selected nodes/or all nodes - to see dependencies (links) in dops
- To see whites above 1 in viewport:
  - HDR rendering in viewport is in D/Effects - switches viewport to 16bit  
  - In perspective viewpoer under perspective turn on "correction toolbar" - bar will show up at the btoom of perspective view
  - switch addaptive full arnge on the color (most right button)
- versioning - use :: e.g. smoke_trail::001
## 1. Subnets and Digital Assets
- subnet - yellow button on the top far right of node view - packs selected nodes in to one subnetwork
- create digital asset (.hda) - by right click on the subnet/context menu
- to lock the newly created subnet - right click/contect menu/match current definition
- right click on digital asset subnet/Type properties
  - change number of imputs
  - match number of imputs to 4 so it resolves to the same as the dop network automatically
 - show in asset manager when right click on hda subnet
 - Digital asset creation - details from webinar by Jeff Wagner here [https://vimeo.com/272793390]
 ## 2. Units
 - meters
 - to scale the asset inside geo object
    - to m use transform
    - to scale it back to original (restore) duplicate the same transform and chech "reverse transform" checkbox and append at the end
 - on object level )oreffered in production)
    - add null on top of object and scale there
 ## 3. Projects
 - under Edit/Aliases and Variables/ Variables pane
 - HIP variable that say where is scene file directory
 - HIPFILE - full path
 - JOB - lowest level of the particular project
 ## 4. Takes
 - Good explanation in Steve Knipping tutorial - Applied Houdini - Dynamics I under "Using the Take System"
 - take list pane
    - add HQ and LQ (they inherit from Main)
    - you can change anything in Main take
    - Add overrides by right click/include in take on given slider
 - There is indication which take you're looking at in the top right corner of whole Houdini
 - Matra can render Current take or force it to render one of the takes (from dropdown in matra properties)
 ## 5. Selecting connected primitives in scene view (by attribute)
 - to select pieces of voronoi fracture
 - in select mode in  select menu on top of scene view push on the square button select groups or connected geometry
 - menu will show up on the right
 - go to gear/settings and choose Attributes/name
 ## 6. Animation Editor (curves)
 - shift + click on animated or expression channel
 - space + G to center the curve in the view
