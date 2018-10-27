## 0. General
- U to go up
- Ctrl + click to decouple rendering and display flags
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
 ## 7. Fast copy/paste
 - select node and alt drag
 - ctrl + alt + shift drag creates reference node - instance
 ## 8. Add direct dots to wires
 - alt + click on wire, move the dot
## 9. Performance monitor
- to compare performance of two nodes against each other merge the results of both
- go to performance monitor pane
- hit record in performance monitor pane
- hit play in the timeline
- stop after 10 frames or so
- compare the times on the nodes
## 10. Quickmarks
- in network click ctrl+1,2,3,4 or 5
- then just toggle with the 1, 2, 3, 4, or 5 to go to that network or use +
## 11. Editing keyframes
- box handle in curve editor
  - select keys on curves
  - press Y, manipulate
  - Y+shift - can change pivot of manipulation
- on timeline
  - H17 to move keyfram on the timeline - middle mouse and drag
  - shift + left mouse drag to select
  - q to deselect everything, or click anywhere on timeline
  - to deselect a portion of selection press shift + right mouse and drag
  - to scale the selected keys - middle mouse drag in selection
  - to hold (move ) a single key - middle mouse drag, then when happy with position press k
  - mute keys - shift+e
  - unmute - ctrl+e
  - toggle between two last keyframes seen - shift+right mouse in the frame count field on the left from timeline
## 12. To create slider in the viewport
- drag and drop parameter in the viewport
- right click - bunch of options
- can hide
- to unhide click on the pivot tool icon on the left - it has list if hidden sliders.
## 13. keep floating windows on top
- for mplay and cirve editor to stay on top
- Houdini Preferences/General User Interface/Keep floating windows on top checkbox on
## 14. Wireframe and shaded in vieport
- toggle with w
- wireframe on top of shaded shift+w
## 15. Saving colors to swatch
- color picker
- select a color
- go to swatch area on top
- press alt+left mouse to add the color (scroll down in swatch view to see it
- press ctrl+left to delete the color from swatch
## 16. Redner and diplsy flags
- press 1 to set display flag
- press 2 to set render flag 
## 17 Views
- full screen - ctrl+b
- spacebar+1 perspective
- spacebar+2 top, hitting one more time - bottom view
- spacebar+3 front and back
- spacebar+4 left and right
## 18. Handle in world/object space
- right click on handle and find the options in the menu under Align Handle - or hit M key
- press ; key to snap and align selected geo to different geo
- to snap rotation - rotation step - (45 degree by default) press ctrl ahile rotating
- to move by certain amount of units - translate step - press ctrl while moving
- these default settings can be changed when right click on the handle and go to handle parameters
