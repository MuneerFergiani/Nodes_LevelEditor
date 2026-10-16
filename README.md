# HTML Level Editor

Open `index.html` directly in a browser. It is one standalone file, with no build step, external libraries, account, or network calls. For a local HTTP preview, run `python -m http.server 8765 --directory Tools/LevelEditor` from the project root.

On a phone, double-tap a cell to add a building. Set its starting team in the details below the grid. Drag between two buildings to toggle their path. Double-click or double-tap a cell to add/remove its building. The right-edge +/− buttons add/remove the last column; the bottom-edge buttons add/remove the last row. Removing occupied cells requires a second press to confirm. Desktop right-click and Ctrl + wheel remain available. Team 0 has no number. New Unity buildings use starting level -1, so Game Settings determines the player starting level.

**Export Text File** downloads a `.txt` file containing versioned JSON. **Load Text File** opens a `.txt` or `.json` export for editing. In Unity, open **Tools > Alchemy > Level Editor > Import**, drop multiple files onto the panel (or use **Add Folder...**), optionally choose a template override, then **Import All as New Scenes...**. Set **Grid spacing (X/Y)** (defaults to 2.5 / 2.5) and **Grid origin** (defaults to zero) in the import panel. These settings override values in every selected file; per-building offsets are preserved. Choose a destination folder under Assets. Each file creates a separate scene; duplicate names get unique filenames. Invalid documents stop the batch before importing; asset/scene failures are reported per file while other files continue. The last successful scene stays open.

The saved template supplies camera, UI, game wiring, and other scene objects. It must have exactly one LevelManager. Only that manager's buildings, paths, and level settings are replaced. Template callbacks remain intact; references to individual old buildings cannot be transferred. The default template is `Assets/Scenes/Levels/Game_3x3.unity`. A clean reusable game template is preferable for long-term use. Imported scenes use the Game_ prefix and are automatically added and enabled in the Build Settings scene list. The separate multiplayer MapSceneDatabase is not modified.

JSON transfers scene name, grid dimensions, spacing/origin, building coordinates and offsets (including Z), all paths, starting layouts and selected index, plus project paths for building/path prefabs, Visual Config, and Game Settings. Those assets are resolved from the Unity project; the HTML does not duplicate or modify their contents. Keep the template and prefab scripts in this project. JSON exports contain level authoring data, not arbitrary Unity components or scene objects.

The Unity editor also has **Export**, so an existing grid can be exported as a text file and opened with **Load Text File**. Custom starting-level overrides are intentionally excluded.

Drafts save in this browser's local storage when available. Export important work before changing browsers or devices. Undo/Redo is per session. The page supports up to 100 x 100 cells, 100 layouts, and four players per layout.

Verification: `node Tools/LevelEditor/editor.test.cjs` runs model and schema checks. Scene reconstruction still requires a Unity Editor check.
