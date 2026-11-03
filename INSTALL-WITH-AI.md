[Leer en español](INSTALAR-CON-IA.md)

# Install FM Prism with an AI

Instructions for an assistant with access to the user's computer (for example Claude Code or Codex). They install the FM Prism plugin in Football Manager 27 from Steam, on Windows.

If you're the user: ask your assistant "Install FM Prism following exactly https://github.com/FM-Prism/fm-prism-plugin/blob/main/INSTALL-WITH-AI.md and ask me for permission before every change". ChatGPT or Claude in the browser won't do: they can't touch your folders.

---

## For the assistant

Follow these steps in order. Before every change to the user's folders, tell them what you're about to do and wait for their confirmation. Explain each step in plain language and in their language.

### Rules

- Don't delete or modify anything beyond what's listed here.
- Don't touch the user's saved games (`Documents\Sports Interactive`).
- If something doesn't match what's expected (BepInEx version, fingerprint, folders), stop and explain it instead of improvising.

### 1. Download FM Prism

- Download `https://github.com/FM-Prism/fm-prism-plugin/releases/latest/download/fm-prism-plugin.zip`.
- Unzip it into `Documents\FM Prism\instalador` (create the folders if they don't exist).
- Inside there must be `plugin\FmVolcado.dll` and `plugin\logica\FmVolcado.Logica.dll`.

### 2. Check that the game is closed

- If the `fm.exe` process is running, ask the user to close Football Manager 27 and wait.

### 3. Find the game folder

- Read the Steam path from the registry: `HKCU\Software\Valve\Steam`, value `SteamPath`.
- Read `<SteamPath>\steamapps\libraryfolders.vdf` to learn all the Steam libraries (`"path"` entries).
- The game folder is `<library>\steamapps\common\Football Manager 27` and it **must** contain `fm.exe`. If you can't find it, ask the user.

### 4. Install BepInEx 6 (only if it isn't there)

- If `winhttp.dll` already exists in the game folder, BepInEx is already installed: don't touch it and go to step 5.
- If not, download exactly this official file:
  `https://builds.bepinex.dev/projects/bepinex_be/791/BepInEx-Unity.IL2CPP-win-x64-6.0.0-be.791%2Bb782da4.zip`
- Check its SHA-256 fingerprint. It must be exactly:
  `BB1C510909B69522733791F3A0817A487379A52DA6468A492F1C9C19B3EC6F9A`
  If it doesn't match, delete the download, stop and tell the user.
- Before extracting, note down the list of items in the root of the game folder.
- Extract the ZIP **directly** into the game folder: `winhttp.dll` must end up next to `fm.exe`, not in a subfolder.
- Save the names of the new items in the root (one per line) in `<game folder>\BepInEx\fmprism-instalado.txt`, so it can be uninstalled later.

### 5. Copy the plugin

- If `BepInEx\plugins\FmVolcado.dll` or `BepInEx\plugins\logica` exist (old test versions), tell the user and, with their permission, delete them.
- Create `<game folder>\BepInEx\plugins\FMPrism\logica`.
- Copy `plugin\FmVolcado.dll` to `BepInEx\plugins\FMPrism\` and `plugin\logica\FmVolcado.Logica.dll` to `BepInEx\plugins\FMPrism\logica\`.
- Create `Documents\FM Prism\versiones` if it doesn't exist.

### 6. Check

- Show the user how the game folder has ended up (`winhttp.dll`, `BepInEx\`, `BepInEx\plugins\FMPrism\…`).
- Ask them to open Football Manager 27: the first time a black window appears (BepInEx's console) and it takes several minutes. It must not be closed.
- Once it has started, read `<game folder>\BepInEx\LogOutput.log` and confirm that "FM Prism … cargado" appears (the log is always in Spanish). If there are errors, explain them.

### 7. Explain how to use it

- With the save loaded: **F9** saves a snapshot of their squad; **F10** opens the menu to pick countries (up to 15 recommended) (↑ ↓ to move, → to tick, Enter to save); **F10 twice** cancels.
- Snapshots are saved in `Documents\FM Prism\versiones` and loaded on fmprism.com, "Snapshots" tab.
- The in-game texts follow the language of Windows (Spanish or English). To change it: `Idioma = es` or `Idioma = en` in `BepInEx\config\fmprism.plugin.cfg`.

### Uninstalling (only if the user asks)

- With the game closed, delete `BepInEx\plugins\FMPrism` and `BepInEx\config\fmprism.plugin.cfg`.
- If `BepInEx\fmprism-instalado.txt` exists, offer to also remove the root items it lists (BepInEx installed by FM Prism). Don't delete anything else, or the user's snapshots.
