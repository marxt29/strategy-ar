Technology Strategy AR — prototype
A phone-browser AR experience of the Technology Strategy temple (4 themes, 7 pillars, cyber security foundation) with animated binary data around the building. No app install.
What's in the folder
`index.html` — the whole experience in one file (Three.js r128 loaded from CDN).
`reference.png` — the original strategy slide the model is built from.
How it works on each phone
Phone / browser	Mode	What the user does
Android, Chrome (ARCore devices)	True AR (WebXR)	Tap View in AR → scan floor/table → tap to place. Toggle Table size / Life size, Move, walk around it 360°, tap pillars for details.
iPhone, Safari	Camera window	Tap View in AR → allow motion + camera. The building appears ~8 m ahead over the live camera; turn the phone to look around, drag to spin, pinch to resize.
Any desktop / no camera	3D view	Drag to orbit 360°, pinch/scroll to zoom, tap pillars.
Camera and AR need HTTPS. They are blocked inside the claude.ai preview frame, so host the file.
Host it in 3 minutes (GitHub Pages, free)
Create a new public repo on github.com, e.g. `strategy-ar`.
Add file → Upload files → drop `index.html` (and `reference.png`) → Commit.
Settings → Pages → Source: Deploy from a branch → main / root → Save.
After ~1 minute open `https://<your-username>.github.io/strategy-ar/` on your phone.
Optional: turn that URL into a QR code and put it on the printed slide or a poster.
Netlify Drop (app.netlify.com/drop) also works: drag the folder in, get an HTTPS link.
Editing content
At the top of the script in `index.html`:
`THEMES` — the four roof labels
`PILLARS` — the seven pillar labels (index 3 is the Innovation block)
`INNOVATION_LINES` — the text on the Innovation block
`FOUNDATION` — the base label
Pillar detail text lives in the `pickable(...)` calls (`text:`) — replace with your real pillar descriptions.
Architecture
```
index.html
 ├─ Scene builder (Three.js)      model built from boxes/frustums, labels drawn on canvas textures,
 │                                same artwork on front and back so it reads from 360°
 ├─ Data motion layer             spiralling 0/1 glyphs (Points), falling binary rain,
 │                                3 rotating binary rings, packets running up pillars, ground pulses
 ├─ Mode router  (View in AR)
 │   ├─ WebXR immersive-ar        hit-test reticle, tap to place, DOM overlay UI, table/life scale
 │   ├─ Camera window fallback    getUserMedia rear camera + DeviceOrientation → camera rotation
 │   └─ 3D orbit (default)        OrbitControls, auto-rotate
 └─ Interaction                   raycast tap → info sheet + glow highlight
```
Next steps (phase 2 ideas)
iPhone true AR: export the model to USDZ and open it with AR Quick Look (static, no binary animation), or use an image-target library (MindAR) so the building rises out of the printed slide.
Per-pillar detail panels with KPIs, owners and initiatives.
Narrated tour: camera flies pillar to pillar with voice-over.
