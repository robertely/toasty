Re-Draw art using aesprint:
  - Create solid color background layer (blue color for contrast.)
  - Import source image as it's own layer. I put this on top, with some transparency.
  - Trace layers in these colors: fr4, copper, mask, silk screen. I took them directly from a photo of an after dark osh pcb.

Export:
  - As Bitmap, use solid background for contrast since this doesn't support transparency.
  - 500% scaled. (warning! going higher will break things later! This is part of how I got a the final size.)
  - Each layer as it's own image. (export each individually, no automatic option for this.)
  - [IMPORTANT]. With oshpark and probably other board houses you can't have silk screen on top of bare copper. When you export the mask you should ADD the Silkscreen layer as well so it has something to sit on.

Covert each bitmap to components using kicads converter:
  - Resolution/DPI is how i came up with the final size.
  - 250 DPI resulted in about 35mm square. Going over 400DPI may get weird with board houses. Maybe this doesn't apply to kicad but I don't know.
  - Some layers need to be imported inverted...
Combine kicad_mod files to merge create final part.
  - The bitmap to Component Converter doesn't have many layer choices.(couriouisly, some but not all.) Use find/replace to change layers in raw files.
  - Create a "merged kicad_mod" by manualy copy-pasting the shapes from all layers into one file.
    - Sounds hard, but once you open the files the structure is visually clear...ish
  - The mask layer is an "inverted" layer. You need to export a negative version of this layer here.
  - Used Eco1.User for fr4 layer. I used this to trace the edge cut line.

Create the part/library:
  - Open the Footprint editor.
  - "Import footprint from kicad file"
  - Inspect using View -> 3d Viewer.
  - Save in a new library. Use a per-project library to keep things in one place.

Create the pcb:
  - No schematic needed here.
  - Click "add footprint"
  - Place the part
  - Add metadata (revision, url)
  - Trace the outline as best you can for the edge cut.

Notes:
- A scale of at least 500% is needed on the inital export and  a DPI of at least 400 if you want sharp lines. Kicad fails at squares lower than this.

Wishlist things that would make this process less painful:
- The bitmap converter doesn't have the same layer options as everything else. It only has a couple. I have to find/repace the copper layer to change the layer.
- The bitmap converter can't import into a preexisting part. You have to create one for each layer then merge them manually.
- Curves in pcbnew for things like edge cuts would help the looks. To get curves i would need to draw them in some vector or cad software then import them. The edge cut would look nicer, but I can't be bothered.