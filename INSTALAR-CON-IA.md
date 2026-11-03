[Read in English](INSTALL-WITH-AI.md)

# Instalar FM Prism con una IA

Instrucciones para un asistente con acceso al ordenador del usuario (por ejemplo Claude Code o Codex). Instalan el plugin FM Prism en Football Manager 27 de Steam, en Windows.

Si eres el usuario: pide a tu asistente «Instala FM Prism siguiendo exactamente https://github.com/FM-Prism/fm-prism-plugin/blob/main/INSTALAR-CON-IA.md y pídeme permiso antes de cada cambio». ChatGPT o Claude en el navegador no sirven: no pueden tocar tus carpetas.

---

## Para el asistente

Sigue estos pasos en orden. Antes de cada cambio en las carpetas del usuario, dile qué vas a hacer y espera su confirmación. Explícale cada paso en lenguaje sencillo y en su idioma.

### Reglas

- No borres ni modifiques nada fuera de lo que se indica aquí.
- No toques las partidas guardadas del usuario (`Documentos\Sports Interactive`).
- Si algo no coincide con lo esperado (versión de BepInEx, huella, carpetas), para y explícalo en lugar de improvisar.

### 1. Descargar FM Prism

- Descarga `https://github.com/FM-Prism/fm-prism-plugin/releases/latest/download/fm-prism-plugin.zip`.
- Descomprímelo en `Documentos\FM Prism\instalador` (crea las carpetas si no existen).
- Dentro debe haber `plugin\FmVolcado.dll` y `plugin\logica\FmVolcado.Logica.dll`.

### 2. Comprobar que el juego está cerrado

- Si el proceso `fm.exe` está en ejecución, pide al usuario que cierre Football Manager 27 y espera.

### 3. Encontrar la carpeta del juego

- Lee la ruta de Steam en el registro: `HKCU\Software\Valve\Steam`, valor `SteamPath`.
- Lee `<SteamPath>\steamapps\libraryfolders.vdf` para conocer todas las bibliotecas de Steam (entradas `"path"`).
- La carpeta del juego es `<biblioteca>\steamapps\common\Football Manager 27` y **debe** contener `fm.exe`. Si no la encuentras, pregunta al usuario.

### 4. Instalar BepInEx 6 (solo si no está)

- Si en la carpeta del juego ya existe `winhttp.dll`, BepInEx ya está instalado: no lo toques y pasa al paso 5.
- Si no, descarga exactamente este archivo oficial:
  `https://builds.bepinex.dev/projects/bepinex_be/791/BepInEx-Unity.IL2CPP-win-x64-6.0.0-be.791%2Bb782da4.zip`
- Comprueba su huella SHA-256. Debe ser exactamente:
  `BB1C510909B69522733791F3A0817A487379A52DA6468A492F1C9C19B3EC6F9A`
  Si no coincide, borra la descarga, para y avisa al usuario.
- Antes de extraer, apunta la lista de elementos de la raíz de la carpeta del juego.
- Extrae el ZIP **directamente** en la carpeta del juego: `winhttp.dll` debe quedar al lado de `fm.exe`, no en una subcarpeta.
- Guarda en `<carpeta del juego>\BepInEx\fmprism-instalado.txt` los nombres de los elementos nuevos de la raíz (uno por línea), para poder desinstalar después.

### 5. Copiar el plugin

- Si existen `BepInEx\plugins\FmVolcado.dll` o `BepInEx\plugins\logica` (versiones de prueba antiguas), díselo al usuario y, con su permiso, bórralos.
- Crea `<carpeta del juego>\BepInEx\plugins\FMPrism\logica`.
- Copia `plugin\FmVolcado.dll` a `BepInEx\plugins\FMPrism\` y `plugin\logica\FmVolcado.Logica.dll` a `BepInEx\plugins\FMPrism\logica\`.
- Crea `Documentos\FM Prism\versiones` si no existe.

### 6. Comprobar

- Enseña al usuario cómo ha quedado la carpeta del juego (`winhttp.dll`, `BepInEx\`, `BepInEx\plugins\FMPrism\…`).
- Pídele que abra Football Manager 27: la primera vez sale una ventana negra (la consola de BepInEx) y tarda varios minutos. No hay que cerrarla.
- Cuando haya arrancado, lee `<carpeta del juego>\BepInEx\LogOutput.log` y confirma que aparece «FM Prism … cargado». Si hay errores, explícaselos.

### 7. Explicar cómo se usa

- Con la partida cargada: **F9** guarda una versión de su plantilla; **F10** abre el menú para elegir países (recomendado hasta 15) (↑ ↓ para moverse, → para marcar, Intro para guardar); **F10 dos veces** cancela.
- Las versiones se guardan en `Documentos\FM Prism\versiones` y se cargan en fmprism.com, pestaña «Versiones».
- Los textos del juego siguen el idioma de Windows (español o inglés). Para cambiarlo: `Idioma = es` o `Idioma = en` en `BepInEx\config\fmprism.plugin.cfg`.

### Desinstalar (solo si el usuario lo pide)

- Con el juego cerrado, borra `BepInEx\plugins\FMPrism` y `BepInEx\config\fmprism.plugin.cfg`.
- Si existe `BepInEx\fmprism-instalado.txt`, ofrece quitar también los elementos de la raíz que lista (BepInEx instalado por FM Prism). No borres nada más ni las versiones del usuario.
