# Plan — Compatibilizar FirstPerson 4.1 + GInput v1.11 + CLEO 4.4.4 en GTA SA (Windows)

## Context

El usuario tiene dos mods para GTA San Andreas en `/Volumes/Bazinga/IA/`:
- `Mod Primera Persona 4.1 GTA SA.rar` — FirstPerson 4.1 (autor: BoPoh).
- `IIIVCSA_GInput_v1.11.zip` — GInput v1.11 (autor: Silent / MixMods).

Va a instalarlos en una **PC con Windows** que **ya tiene CLEO 4.4.4 funcionando** sobre **GTA SA v1.0 US (Hoodlum)**. Reportó que se dice por foros que estos mods (de 2014 / pensados para CLEO 3.x–4.1) son incompatibles con CLEO 4.4.4 y que GInput puede chocar con FirstPerson.

**Deliverable:** un **prompt "casi cocinado"** que se le entregará a otro agente (modelo posiblemente menor) corriendo en la máquina Windows, con instrucciones, ejemplos de código y manejo de variantes (versiones distintas de los mods que pueda haber descargado el usuario).

## Hallazgos de la inspección de los archivos

Inspección no destructiva de los dos paquetes (extracción de muestra a `/tmp/gta_inspect/`):

1. **FirstPerson 4.1 NO es un CLEO Script (.cs)**. Es un **plugin ASI** disfrazado:
   - `FirstPerson.sp` → es un PE32 DLL (mismo formato que `.asi`). Lo carga `Hooks.asi`, no CLEO.
   - `Hooks.asi`, `MotionBlur.asi` → plugins ASI estándar.
   - El paquete trae **una copia vieja de CLEO 4.1** (string `"CLEO 4.1 error"` en el `CLEO.asi`) y los plugins `.cleo` (`FileSystemOperations.cleo`, `IniFiles.cleo`, `IntOperations.cleo`) que **ya vienen con CLEO 4.4.4** por defecto.
   - Trae `bass.dll`, `vorbisFile.dll`, `vorbisHooked.dll`, `msvcr100d.dll`, `D3DX9_40.dll`, `d3dx9_26.dll` y un `gta_sa.exe` v1.0 US (14.383.616 bytes).
   - `FirstPerson.cfg` es un **binario propietario** (floats), no se edita a mano — se configura desde el GUI in-game del mod.
   - `FirstPerson.sp` solo usa `GetKeyState` (Win32) para teclado. No depende de DirectInput ni XInput, así que **a nivel de input puro es ortogonal a GInput**. El choque real, si existe, es a nivel de **cámara** (GInput tiene su propia lógica de cámara/aim de pad).

2. **GInput v1.11** es un plugin ASI moderno y autosuficiente: `GInputSA.asi` + `GInputSA.ini` + `models/` (texturas de botones). Reescribe el handling de pad de DirectInput a XInput.

3. **El "conflicto CLEO" es un falso positivo si se instala bien.** El paquete de FirstPerson distribuye una versión vieja de CLEO solo como "CLEO bundled" para usuarios sin CLEO. Si el usuario copia la carpeta del mod tal cual, **sobrescribe CLEO 4.4.4 con CLEO 4.1**, y eso **rompe** otros mods que dependan de la versión nueva. La fix es **NO copiar los archivos de CLEO del paquete**.

4. Conflicto FirstPerson + GInput: documentado en foros pero generalmente menor — soluciones reportadas pasan por configurar GInput para no hijackear cámara o usar Big Picture con joystick→mouse relativo. No hay un fix de archivo único conocido.

## El prompt cocinado para el agente Windows

**El plan = generar este prompt y entregárselo al usuario.** El agente Windows ejecutará. El prompt en sí es el contenido principal, escrito en un único bloque listo para copiar.

---

````
ROL: Sos un agente de instalación/troubleshooting de mods para GTA San Andreas en Windows.
Vas a instalar dos mods en una instalación EXISTENTE y FUNCIONAL de GTA SA + CLEO 4.4.4
sin romper lo que ya está. Trabajá con cuidado, hacé backups, y verificá cada paso.

CONTEXTO DEL ENTORNO (asumido — VERIFICAR antes de empezar):
- SO: Windows.
- Juego: GTA San Andreas v1.0 US (Hoodlum). El gta_sa.exe debe medir 14.383.616 bytes
  exactos. Si NO mide eso, parar y preguntar al usuario qué versión tiene (v1.0 US es
  la única soportada por estos mods).
- CLEO 4.4.4 ya instalado y funcionando (otros scripts CLEO andan).
- Carpeta del juego típica: "C:\Program Files (x86)\Rockstar Games\GTA San Andreas"
  (puede variar — preguntale al usuario o buscá gta_sa.exe).

MODS A INSTALAR:
1) FirstPerson 4.1 (BoPoh) — el usuario tiene "Mod Primera Persona 4.1 GTA SA.rar"
   o equivalente. Es UN PLUGIN ASI, no un CLEO script. Trae adentro una copia
   VIEJA de CLEO 4.1 que NO hay que copiar.
2) GInput v1.11 (Silent) — el usuario tiene "IIIVCSA_GInput_v1.11.zip" o equivalente.
   Solo usaremos la subcarpeta "SA_GInput".

PROBLEMA A EVITAR (raíz de la incompatibilidad reportada):
Si copiás la carpeta del FirstPerson tal cual a la raíz del juego, sobrescribís
CLEO.asi, bass.dll, vorbisFile.dll, vorbisHooked.dll, etc. con versiones de 2011
(CLEO 4.1). Eso ROMPE CLEO 4.4.4 y hace que parezca "incompatibilidad". La fix es
copiar SOLO los archivos propios del mod FirstPerson, no su CLEO bundled.

================================================================================
PASO 0 — Detectar variantes locales
================================================================================
El usuario puede tener:
- El .rar/.zip que mencioné, o
- Otra versión (ej. "First Person v3.0 Fixed", "FirstPerson v4.0", paquete ya
  extraído, etc.), o
- GInput v1.10 / v1.12 (mismo layout).

Acción: pedile al usuario la ruta a las descargas y/o buscá en
%USERPROFILE%\Downloads\ con PowerShell:

  Get-ChildItem -Path $env:USERPROFILE\Downloads -Recurse -Include `
    "*FirstPerson*","*Primera*Persona*","*GInput*" -ErrorAction SilentlyContinue |
    Select-Object FullName, Length

Si encontrás una versión distinta de FirstPerson (ej. v3.0 Fixed que sí soporta
v1.1/v3.0/Steam), preguntá al usuario cuál quiere usar antes de seguir. Si tiene
v4.0 o 4.1, seguí este plan tal cual; las extensiones de archivo y el layout son
los mismos.

================================================================================
PASO 1 — Backup
================================================================================
ANTES de tocar nada, hacé backup completo de la carpeta del juego:

  $game = "C:\Program Files (x86)\Rockstar Games\GTA San Andreas"   # ajustar
  $stamp = Get-Date -Format "yyyyMMdd-HHmmss"
  Copy-Item -Recurse -Path $game -Destination "$game.backup-$stamp"

Si la carpeta es muy grande, al menos respaldá los archivos críticos:

  $critical = @("gta_sa.exe","cleo.asi","bass.dll","vorbisFile.dll",
                "vorbisHooked.dll","CLEO","modloader")
  foreach ($f in $critical) {
    if (Test-Path "$game\$f") { Copy-Item -Recurse "$game\$f" "$game\_backup\" }
  }

================================================================================
PASO 2 — Verificar el entorno actual
================================================================================
Confirmá que:
  a) gta_sa.exe = 14.383.616 bytes (v1.0 US):
       (Get-Item "$game\gta_sa.exe").Length
  b) CLEO 4.4.4 instalado:
       Test-Path "$game\cleo.asi"
       Test-Path "$game\CLEO\"
       Test-Path "$game\bass.dll"
     Y la versión del cleo.asi:
       (Get-Item "$game\cleo.asi").VersionInfo.FileVersion
     Debería decir 4.4.x. Si es 4.1, el usuario NO tiene 4.4.4 — pará y avisá.
  c) ASI Loader presente. CLEO 4.4 usa Ultimate ASI Loader que se inyecta vía
     vorbisFile.dll renombrado. Confirmá:
       Test-Path "$game\vorbisFile.dll"
     Si NO existe, parar — el paso 3 (Hooks.asi) no va a cargar sin ASI Loader.

================================================================================
PASO 3 — Extraer los mods a una zona temporal (NO al juego todavía)
================================================================================
Creá una carpeta de staging y extraé ahí:

  $staging = "$env:TEMP\gtasa-mods-staging"
  New-Item -ItemType Directory -Force -Path $staging

Para el .rar:
  # requiere 7-Zip instalado (winget install 7zip.7zip)
  & "C:\Program Files\7-Zip\7z.exe" x "ruta\al\Mod Primera Persona 4.1 GTA SA.rar" `
    -o"$staging\firstperson" -y

Para el .zip:
  Expand-Archive "ruta\al\IIIVCSA_GInput_v1.11.zip" -DestinationPath "$staging\ginput" -Force

Inspeccioná layout. El esperado para FirstPerson es:
  $staging\firstperson\Mod Primera Persona 4.1 GTA SA\1.- Mover a carpeta raiz\
y para GInput:
  $staging\ginput\[III,VC,SA] GInput v1.11\GInput - III,VC,SA\SA_GInput\GInputSA\

Si el layout es distinto (otra versión / ya extraído), buscá el archivo clave:
  Get-ChildItem -Recurse -Path $staging -Filter "FirstPerson.sp"
  Get-ChildItem -Recurse -Path $staging -Filter "GInputSA.asi"
y derivá las rutas desde ahí.

================================================================================
PASO 4 — Instalar FirstPerson SOLO con sus archivos propios
================================================================================
SOLO copiá esta lista (TODOS los demás archivos del paquete son la copia vieja
de CLEO 4.1 + dependencias que NO querés sobrescribir):

  WHITELIST (de "1.- Mover a carpeta raiz\" → carpeta del juego):
    FirstPerson.sp           → $game\FirstPerson.sp
    FirstPerson.cfg          → $game\FirstPerson.cfg
    GUI.fp                   → $game\GUI.fp
    Hooks.asi                → $game\Hooks.asi
    MotionBlur.asi           → $game\MotionBlur.asi   (opcional, motion blur)
    MotionBlur.ini           → $game\MotionBlur.ini   (opcional)
    models\FirstPerson.txd   → $game\models\FirstPerson.txd
    data\fonts\fp_font.dat   → $game\data\fonts\fp_font.dat
    data\fonts\fp_font.txd   → $game\data\fonts\fp_font.txd

  BLACKLIST (NO copiar — son CLEO 4.1 viejo o redundantes con CLEO 4.4.4):
    CLEO.asi                              ← rompería CLEO 4.4.4
    CLEO4.chm                             ← solo doc
    CLEO\FileSystemOperations.cleo        ← ya viene con 4.4.4
    CLEO\IniFiles.cleo                    ← ya viene con 4.4.4
    CLEO\IntOperations.cleo               ← ya viene con 4.4.4
    bass.dll                              ← versión vieja
    vorbisFile.dll                        ← rompería ASI Loader
    vorbisHooked.dll                      ← versión vieja
    D3DX9_40.dll                          ← lo provee Windows / DirectX
    d3dx9_26.dll                          ← idem
    msvcr100d.dll                         ← runtime de debug, no hace falta
    gta_sa.exe                            ← NO sobrescribir el del usuario

PowerShell (ejemplo, ajustá $src):

  $src = "$staging\firstperson\Mod Primera Persona 4.1 GTA SA\1.- Mover a carpeta raiz"
  $files = @(
    "FirstPerson.sp","FirstPerson.cfg","GUI.fp","Hooks.asi",
    "MotionBlur.asi","MotionBlur.ini"
  )
  foreach ($f in $files) {
    Copy-Item -Force "$src\$f" "$game\$f"
  }
  New-Item -ItemType Directory -Force -Path "$game\models" | Out-Null
  Copy-Item -Force "$src\models\FirstPerson.txd" "$game\models\FirstPerson.txd"
  New-Item -ItemType Directory -Force -Path "$game\data\fonts" | Out-Null
  Copy-Item -Force "$src\data\fonts\fp_font.dat" "$game\data\fonts\fp_font.dat"
  Copy-Item -Force "$src\data\fonts\fp_font.txd" "$game\data\fonts\fp_font.txd"

================================================================================
PASO 5 — Instalar GInput SA
================================================================================
Del paquete GInput, usá SOLO la subcarpeta SA_GInput\GInputSA:

  $gi = "$staging\ginput\[III,VC,SA] GInput v1.11\GInput - III,VC,SA\SA_GInput\GInputSA"
  Copy-Item -Force "$gi\GInputSA.asi" "$game\GInputSA.asi"
  Copy-Item -Force "$gi\GInputSA.ini" "$game\GInputSA.ini"
  New-Item -ItemType Directory -Force -Path "$game\models" | Out-Null
  Copy-Item -Force "$gi\models\ps3btns.txd"  "$game\models\ps3btns.txd"
  Copy-Item -Force "$gi\models\sixaxis.txd"  "$game\models\sixaxis.txd"
  Copy-Item -Force "$gi\models\x360btns.txd" "$game\models\x360btns.txd"

GInput es independiente del FirstPerson y no sobrescribe nada que ya tengas
(salvo si ya tenías GInput previamente — preguntá antes de pisar).

================================================================================
PASO 6 — Mitigar el choque cámara FirstPerson ↔ GInput
================================================================================
GInput tiene aim asistido propio. Para que no compita con la cámara del FirstPerson,
abrí $game\GInputSA.ini y dejá:

  [GInput]
  FreeAim=1                       ; desactiva el lock-on del pad

  [Pad1]
  ControlsSet=1                   ; clásico de PS2; cambiar a 2 si querés "IV style"
  InvertLook=0                    ; ajustar a gusto

Si el usuario va a jugar en primera persona casi todo el tiempo y usa pad, también
sirve poner SwapSticksDuringAiming=1 para que el aim se sienta natural.

================================================================================
PASO 7 — Probar
================================================================================
1. Lanzá el juego.
2. Cargá una partida (no menú).
3. Activá la primera persona con la tecla por defecto del mod (mirá el README del
   .rar; en FirstPerson 4.1 suele ser "V" o el GUI in-game con F11/F12 — confirmá
   con el usuario).
4. Verificá:
   - El juego no crashea al iniciar ni al cargar partida.
   - El modo primera persona se activa.
   - El gamepad responde con prompts de PS3/X360 (eso confirma que GInput cargó).
   - Cámara fluida; al apuntar con pad no hay "tirones" entre los dos sistemas.

================================================================================
PASO 8 — Si algo falla, diagnóstico
================================================================================
- Crash al iniciar:
    Mirá $game\cleo.log, $game\modloader\modloader.log, $game\asiloader.log
    (existe solo si tenés Ultimate ASI Loader con logging on).
    Buscá la última línea con "loading" — el archivo nombrado ahí es el sospechoso.

- "FirstPerson no se activa":
    Verificá que Hooks.asi cargó. Sin Hooks.asi, FirstPerson.sp queda inerte.
    Confirmá Test-Path "$game\Hooks.asi" y que tu ASI Loader esté inyectado
    (vorbisFile.dll = Ultimate ASI Loader; o revisá si el usuario usa silentpatch
    con su propio loader).

- "El pad no responde / no se ve prompt de Xbox":
    GInputSA.asi no cargó. Mismo chequeo que arriba: ASI loader funcionando.
    Probá renombrar GInputSA.asi a GInputSA.asi (sí, exactamente; algunos loaders
    son sensibles a mayúsculas en path UNC) y volvé a correr.

- "CLEO dejó de cargar otros scripts":
    Probablemente copiaste CLEO.asi del paquete por error. Restaurá del backup
    el cleo.asi, bass.dll, vorbisFile.dll, vorbisHooked.dll, y volvé al paso 4.

- "Crashes intermitentes en misiones específicas":
    Algunos foros reportan que FirstPerson 4.1 choca con misiones que ya manejan
    cámara forzada (cinemáticas, sniper, etc.). Soluciones documentadas:
      a) Salir de primera persona antes de la cinemática (tecla del mod).
      b) Buscar "First-Person v3.0 Fixed" (BoPoh + community fixes) que es
         compatible con v1.1 y v3.0 (Steam) y no trae CLEO bundled.
    Avisá al usuario antes de migrar.

================================================================================
PASO 9 — Reporte final al usuario
================================================================================
Devolvé al usuario:
  - Lista exacta de archivos copiados con sus rutas finales.
  - Lista exacta de archivos del paquete que IGNORASTE y por qué.
  - Resultado de la prueba (carga, FirstPerson activa, pad responde).
  - Si hubo cualquier error, las líneas relevantes de los .log.

NO modifiques nada fuera de la carpeta del juego. NO ejecutes el gta_sa.exe que
viene en el .rar (es viejo y trae cracks). NO instales DirectX runtimes ni VC++
runtimes "por las dudas" — solo si un error lo pide específicamente.
````

---

## Critical files referenced

- Paquete FirstPerson (src): `/Volumes/Bazinga/IA/Mod Primera Persona 4.1 GTA SA.rar`
- Paquete GInput (src): `/Volumes/Bazinga/IA/IIIVCSA_GInput_v1.11.zip`
- Plan file (este archivo): `/Users/barbycus/.claude/plans/tengo-este-mod-vectorized-beaver.md`

No hay archivos del repo a modificar — el deliverable es texto que el usuario va a llevarse a otra máquina.

## Verification

Cómo confirmar que el plan funcionó (lo hace el agente Windows, el usuario reporta):

1. `gta_sa.exe` cargá hasta la pantalla principal sin crashear.
2. Cargar partida → no crashea.
3. Tecla de FirstPerson activa la cámara primera persona.
4. Conectar pad → aparecen prompts con botones Xbox/PS (= GInput cargó).
5. Apuntar con pad en primera persona no produce "tirones" de cámara.
6. Otros mods CLEO previos del usuario siguen funcionando (= no se sobrescribió CLEO 4.4.4).

Si los 6 puntos pasan, el fix está bien.
