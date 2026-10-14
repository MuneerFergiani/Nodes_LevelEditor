# HTML Level Editor

Open `index.html` directly in a browser. It is one standalone file, with no build step, external libraries, account, or network calls. For a local HTTP preview, run `python -m http.server 8765 --directory Tools/LevelEditor` from the project root.

On a phone, select a cell and enable **Has Building**. Set its starting team in the details below the grid. Drag between two buildings to toggle their path. Double-click or double-tap a cell to add/remove its building. The right-edge +/− buttons add/remove the last column; the bottom-edge buttons add/remove the last row. Removing occupied cells requires a second press to confirm. Desktop right-click and Ctrl + wheel remain available. Team 0 has no number. New Unity buildings use starting level -1, so Game Settings determines the player starting level.

**Export to Clipboard** copies versioned JSON. If the browser blocks clipboard access, the page reveals a text area with a manual copy option. In Unity, open **Tools > Alchemy > Level Editor > Import**, paste the text, optionally choose a template override, validate, and click **Import as New Scene**. Choose a new scene filename. Existing scene assets cannot be overwritten. Unity offers to save open scenes and switches to the imported scene after successful creation.

The saved template supplies camera, UI, game wiring, and other scene objects. It must have exactly one LevelManager. Only that manager's buildings, paths, and level settings are replaced. Template callbacks remain intact; references to individual old buildings cannot be transferred. The default template is `Assets/Scenes/Levels/Game_3x3.unity`. A clean reusable game template is preferable for long-term use. The scene is not automatically added to Build Settings or a multiplayer map catalog.

JSON transfers scene name, grid dimensions, spacing/origin, building coordinates and offsets (including Z), all paths, starting layouts and selected index, plus project paths for building/path prefabs, Visual Config, and Game Settings. Those assets are resolved from the Unity project; the HTML does not duplicate or modify their contents. Keep the template and prefab scripts in this project. JSON exports contain level authoring data, not arbitrary Unity components or scene objects.

The Unity editor also has **Export**, so an existing grid can be copied into the HTML page using **Load JSON**. Custom starting-level overrides are intentionally excluded.

Drafts save in this browser's local storage when available. Export important work before changing browsers or devices. Undo/Redo is per session. The page supports up to 100 x 100 cells, 100 layouts, and four players per layout.

Verification: `node Tools/LevelEditor/editor.test.cjs` runs model and schema checks. Scene reconstruction still requires a Unity Editor check.
