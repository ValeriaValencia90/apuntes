# Git desde cero

> **Entorno de referencia:** Windows con Git Bash, Visual Studio Code y cuenta en GitHub.
> **Forma de entrega general:** salvo que se indique otra cosa, cada práctica se entrega como un documento PDF con capturas de pantalla de la terminal **donde se vea el comando y su resultado**, más el enlace al repositorio cuando proceda.

---

## Índice

1. [Introducción al control de versiones](#tema-1--introducción-al-control-de-versiones)
2. [Instalación y configuración](#tema-2--instalación-y-configuración)
3. [Primeros pasos: el repositorio local](#tema-3--primeros-pasos-el-repositorio-local)
4. [Consultar el historial](#tema-4--consultar-el-historial)
5. [Deshacer cambios](#tema-5--deshacer-cambios)
6. [Repositorios remotos con GitHub](#tema-6--repositorios-remotos-con-github)
7. [Ramas](#tema-7--ramas)
8. [Trabajo colaborativo](#tema-8--trabajo-colaborativo)
9. [Extras útiles](#tema-9--extras-útiles)
10. [Proyecto final](#tema-10--proyecto-final)
11. [Anexo: chuleta de comandos](#anexo--chuleta-de-comandos)

---

## Tema 1 · Introducción al control de versiones

### Objetivos
- Entender qué es un sistema de control de versiones (SCV) y qué problema resuelve.
- Distinguir entre SCV locales, centralizados y distribuidos.
- Diferenciar Git (herramienta) de GitHub/GitLab (plataformas).

### Contenidos

**¿Qué problema resuelve?** Todos hemos visto carpetas así:

```
trabajo.docx
trabajo_v2.docx
trabajo_v2_corregido.docx
trabajo_FINAL.docx
trabajo_FINAL_definitivo_ahora_si.docx
```

Problemas: no sabemos qué cambió entre versiones, quién lo cambió, ni podemos combinar el trabajo de dos personas fácilmente. Un SCV guarda **cada versión**, **quién** la hizo, **cuándo** y **por qué**.

**Tipos de SCV**

| Tipo | Cómo funciona | Ejemplo | Inconveniente |
|---|---|---|---|
| Local | Las versiones se guardan en tu propio equipo | Copias manuales, RCS | No sirve para trabajar en equipo |
| Centralizado | Un servidor guarda el historial; los usuarios se conectan a él | SVN | Si cae el servidor, nadie trabaja |
| Distribuido | Cada usuario tiene una copia completa del historial | **Git**, Mercurial | Curva de aprendizaje algo mayor |

**Git vs GitHub**
- **Git** es el programa que se instala en el ordenador y gestiona las versiones. Funciona sin internet.
- **GitHub**, **GitLab** o **Bitbucket** son webs que alojan repositorios Git y añaden herramientas de colaboración.
- Analogía: Git es como Word; GitHub es como OneDrive donde guardas y compartes los documentos.

**Vocabulario básico**
- **Repositorio (repo):** carpeta cuyo historial controla Git.
- **Commit:** una "foto" del proyecto en un momento dado.
- **Rama (branch):** línea de desarrollo independiente.
- **Remoto:** copia del repositorio alojada en otro sitio (p. ej. GitHub).

### Práctica 1 — Investigación: el control de versiones en la vida real

Por parejas, elaborad un documento (Writer o Word) de 2 páginas que responda:

1. Describe una situación real (escolar o laboral) en la que hayas sufrido el problema de las versiones. ¿Cómo lo habría resuelto un SCV?
2. Explica con tus palabras la diferencia entre un SCV centralizado y uno distribuido. Incluye un esquema hecho por ti (draw.io, Impress…).
3. Busca 3 empresas o proyectos conocidos que usen Git/GitHub y qué publican allí.
4. ¿Qué diferencias hay entre GitHub y GitLab? Busca al menos 3.

**📦 Entregable:** PDF con las respuestas, el esquema y las fuentes consultadas.

---

## Tema 2 · Instalación y configuración

### Objetivos
- Instalar Git en Windows.
- Configurar la identidad del usuario.
- Manejar los comandos básicos de la terminal.

### Contenidos

**Instalación**
1. Descargar desde <https://git-scm.com>.
2. Opciones recomendadas durante la instalación:
   - Editor por defecto: **Visual Studio Code**.
   - Nombre de la rama inicial: **main** ("Override the default branch name").
   - Resto: dejar por defecto.
3. Comprobar la instalación abriendo **Git Bash**:

```bash
git --version
```

**Configuración inicial** (solo se hace una vez por equipo):

Git necesita saber quién eres, porque cada commit queda firmado con un nombre y un email. La opción `--global` hace que la configuración sirva para todos los repositorios de tu usuario en ese ordenador.

```bash
# Tu nombre: aparecerá como autor/a de cada commit que hagas
git config --global user.name "Ane Etxeberria"

# Tu email: también queda en cada commit y GitHub lo usa para asociar los commits a tu cuenta
git config --global user.email "ane.etxeberria@ejemplo.com"

# Editor que se abrirá cuando Git necesite que escribas un texto largo
# (por ejemplo, un mensaje de commit sin -m). "--wait" hace que Git espere
# a que cierres el archivo en VS Code antes de continuar
git config --global core.editor "code --wait"

# Nombre de la rama principal que se creará en cada repositorio nuevo.
# Usamos "main" porque es el nombre que utiliza GitHub por defecto
git config --global init.defaultBranch main

# Muestra toda la configuración actual para comprobar que está bien
git config --list
```

> ⚠️ El email debería ser el mismo que usaréis después en GitHub; si no coincide, GitHub no reconocerá vuestros commits como vuestros.

**Terminal básica: Git Bash y Windows**

En Windows podemos usar tres terminales:
- **Git Bash:** se instala con Git y usa comandos de **Linux**. Es la que usaremos en clase.
- **Símbolo del sistema (CMD):** la terminal clásica de Windows, con sus propios comandos.
- **PowerShell:** la terminal moderna de Windows. Tiene sus comandos propios, pero también acepta muchos de los de Linux (`ls`, `cd`, `pwd`, `cat`, `rm`, `clear`).

> 💡 Los comandos de **Git** (`git status`, `git add`…) son **iguales en las tres terminales**. Lo que cambia son los comandos para moverse por carpetas y manejar archivos.

| Para qué sirve | Git Bash (Linux) | CMD (Windows) | PowerShell (Windows) |
|---|---|---|---|
| Ver en qué carpeta estoy | `pwd` | `cd` (sin nada detrás) | `pwd` |
| Listar el contenido de la carpeta | `ls` | `dir` | `dir` o `ls` |
| Listar incluyendo archivos ocultos (como `.git`) | `ls -la` | `dir /a` | `dir -Force` |
| Entrar en una carpeta | `cd Documentos` | `cd Documentos` | `cd Documentos` |
| Subir a la carpeta anterior | `cd ..` | `cd ..` | `cd ..` |
| Crear una carpeta | `mkdir proyecto` | `mkdir proyecto` | `mkdir proyecto` |
| Crear un archivo vacío | `touch notas.txt` | `type nul > notas.txt` | `New-Item notas.txt` |
| Escribir texto en un archivo (lo crea o lo sobrescribe) | `echo "Hola" > notas.txt` | `echo Hola > notas.txt` | `echo "Hola" > notas.txt` |
| Añadir texto al final de un archivo | `echo "Adiós" >> notas.txt` | `echo Adiós >> notas.txt` | `echo "Adiós" >> notas.txt` |
| Ver el contenido de un archivo | `cat notas.txt` | `type notas.txt` | `cat notas.txt` o `type notas.txt` |
| Borrar un archivo | `rm notas.txt` | `del notas.txt` | `rm notas.txt` o `del notas.txt` |
| Borrar una carpeta con todo su contenido | `rm -r proyecto` | `rmdir /s proyecto` | `rm -r proyecto` |
| Limpiar la pantalla | `clear` | `cls` | `clear` o `cls` |

**Diferencias importantes**
- **Barras en las rutas:** Git Bash usa `/` y Windows usa `\`.
  - Git Bash: `cd /c/Users/ane/Documentos`
  - CMD y PowerShell: `cd C:\Users\ane\Documentos`
- **Comillas en CMD:** en CMD, `echo "Hola" > notas.txt` guarda también las comillas dentro del archivo; por eso allí se escribe sin ellas.
- **Carpeta personal:** en Git Bash y PowerShell, `~` es tu carpeta de usuario (`cd ~/Documentos`); en CMD no funciona y se usa `cd %USERPROFILE%\Documentos`.

> ⚠️ Cuidado con `rm -r` y `rmdir /s`: borran sin pasar por la papelera.

> 💡 Consejo: usa la tecla **Tab** para autocompletar y las flechas **↑ ↓** para recuperar comandos anteriores.

### Práctica 2 — Instalación y manejo de la terminal

1. Instala Git y captura la salida de `git --version`.
2. Configura tu nombre y email y captura `git config --list`.
3. Usando **solo la terminal**, crea esta estructura dentro de `Documentos`:

```
practicas-git/
├── tema2/
│   ├── apuntes.txt   (con el texto "Mis apuntes de Git")
│   └── dudas.txt
└── leeme.txt
```

4. Muestra la estructura con `ls -R practicas-git` y el contenido de `apuntes.txt` con `cat`.
5. Abre **CMD** y, con los comandos de Windows, entra en `practicas-git\tema2`, lista su contenido con `dir`, muestra `apuntes.txt` con `type` y crea un archivo `windows.txt` con el texto "Creado desde CMD".
6. Vuelve a Git Bash y comprueba con `cat` que `windows.txt` existe y tiene el texto.

**📦 Entregable:** PDF con las capturas de cada paso.

---

## Tema 3 · Primeros pasos: el repositorio local

### Objetivos
- Crear un repositorio.
- Comprender las tres áreas de Git.
- Realizar commits con mensajes adecuados.

### Contenidos

**Crear un repositorio**

```bash
mkdir mi-primer-repo   # Crea una carpeta nueva para el proyecto
cd mi-primer-repo      # Entra en esa carpeta
git init               # Convierte la carpeta en un repositorio de Git
```

Git crea una carpeta oculta `.git` donde guarda todo el historial. **Nunca se toca a mano.**

**Las tres áreas de Git**

| Orden | Área | Qué contiene | Cómo se pasa a la siguiente |
|---|---|---|---|
| 1 | **Directorio de trabajo** | Los archivos tal y como los estás editando | `git add` los lleva al staging |
| 2 | **Staging** (área de preparación) | Los cambios elegidos para el próximo commit | `git commit` los guarda en el repositorio |
| 3 | **Repositorio** | El historial con todos los commits guardados | — |

**Directorio de trabajo** → `git add` → **Staging** → `git commit` → **Repositorio**

Analogía: preparar un paquete para enviarlo por correo. Los archivos de tu mesa son el directorio de trabajo, la caja abierta donde vas metiendo cosas es el staging, y cerrar y enviar la caja es el commit.

**Estados de un archivo**
- **Untracked:** Git no lo controla todavía.
- **Modified:** ha cambiado desde el último commit.
- **Staged:** preparado para el próximo commit.
- **Committed:** guardado en el historial.

**Comandos**

```bash
git status                  # ¿En qué estado está todo?
git add archivo.txt         # Añade un archivo al staging
git add .                   # Añade todos los cambios de la carpeta
git commit -m "Mensaje"     # Guarda el commit
```

**Ejemplo completo**

```bash
# Crea el archivo compra.md con una línea de título (">" crea o sobrescribe el archivo)
echo "# Lista de la compra" > compra.md

git status                         # compra.md aparece como untracked (Git aún no lo controla)
git add compra.md                  # Lo pasa al staging
git status                         # Ahora aparece como staged (listo para el commit)
git commit -m "Añade lista de la compra"   # Guarda la primera versión en el historial

# Añade una línea al final del archivo (">>" añade sin borrar lo que había)
echo "- Leche" >> compra.md

git status                         # Aparece como modified (ha cambiado desde el último commit)
git add compra.md                  # Prepara el cambio
git commit -m "Añade leche a la lista"     # Guarda la segunda versión
```

**Buenos mensajes de commit**

| ❌ Mal | ✅ Bien |
|---|---|
| `cambios` | `Añade tabla de precios al presupuesto` |
| `asdf` | `Corrige faltas de ortografía en la introducción` |
| `ya funciona` | `Arregla el formato de fechas en la portada` |

Reglas: verbo en presente ("Añade", "Corrige", "Elimina"), breve (máximo ~50 caracteres) y que explique **qué** cambia.

### Práctica 3 — Mi primer repositorio

1. Crea el repositorio `receta-git` dentro de `practicas-git`.
2. Crea `receta.md` con el título de tu receta favorita y haz el primer commit.
3. Añade los ingredientes → commit.
4. Añade los pasos de preparación → commit.
5. Crea `foto.txt` (simula una imagen) y `notas.txt`. Añade **solo** `foto.txt` al staging y captura `git status` para que se vean los dos estados distintos. Haz commit.
6. Haz commit también de `notas.txt`.

Debes tener **al menos 5 commits** con mensajes correctos.

**📦 Entregable:** PDF con capturas de `git status` en cada paso y una captura final de `git log --oneline`. Comprime la carpeta `receta-git` **incluyendo la carpeta `.git`** y entrégala en .zip.

---

## Tema 4 · Consultar el historial

### Objetivos
- Consultar y filtrar el historial.
- Ver las diferencias entre versiones.
- Excluir archivos con `.gitignore`.

### Contenidos

**Ver el historial**

```bash
git log                          # Historial completo
git log --oneline                # Una línea por commit
git log --oneline --graph --all  # Con gráfico de ramas
git log -3                       # Solo los 3 últimos
git log --author="Ane"           # Commits de una persona
git log -- receta.md             # Commits que afectan a un archivo
```

Cada commit tiene un identificador único (hash), por ejemplo `a1b2c3d`. Basta con los primeros 7 caracteres para referirse a él.

**Ver diferencias**

```bash
git diff                   # Cambios aún no añadidos al staging
git diff --staged          # Cambios en staging (lo que irá al commit)
git diff a1b2c3d e4f5g6h   # Diferencias entre dos commits
git show a1b2c3d           # Qué cambió en un commit concreto
```

En la salida, las líneas con `+` (verde) se han añadido y las de `-` (rojo) se han eliminado.

**El archivo `.gitignore`**

**¿Qué es?** Es un archivo de texto llamado exactamente `.gitignore` que se coloca en la carpeta principal del repositorio. Contiene una lista de archivos y carpetas que Git debe **ignorar**: no aparecerán en `git status`, `git add .` no los añadirá y nunca llegarán a GitHub.

**¿Para qué sirve?** En una carpeta de trabajo hay archivos que no deben guardarse en el historial:

| Tipo de archivo | Ejemplo | Por qué ignorarlo |
|---|---|---|
| Temporales de Office | `~$informe.docx` | Word los crea mientras el documento está abierto y los borra al cerrarlo |
| Archivos del sistema | `Thumbs.db`, `desktop.ini` | Windows los crea solo; no forman parte del proyecto |
| Datos privados | `contraseñas.txt` | Si se suben a GitHub, cualquiera puede verlos |
| Archivos generados | `informe.pdf` (exportado desde el `.docx`) | Se pueden volver a crear en cualquier momento |
| Archivos muy pesados | vídeos, copias de seguridad | Ralentizan el repositorio |

> 💡 El propio `.gitignore` **sí** se guarda en el repositorio (se hace `add` y `commit` de él), para que todas las personas que trabajen en el proyecto ignoren los mismos archivos.

**Cómo crearlo**

Al empezar por un punto, es un archivo "oculto". Lo más sencillo es crearlo desde la terminal, dentro de la carpeta del repositorio:

```bash
# Git Bash: crea el archivo .gitignore vacío
touch .gitignore

# Abre el archivo en VS Code para escribir dentro
code .gitignore

# Lista también los archivos ocultos: así comprobamos que .gitignore existe
ls -la
```

En **CMD** se crea con `type nul > .gitignore` y en **PowerShell** con `New-Item .gitignore`. También se puede crear desde VS Code con *Nuevo archivo* y escribiendo el nombre `.gitignore`.

> ⚠️ El nombre debe ser exactamente `.gitignore`: con el punto delante y **sin extensión**. Si el Bloc de notas lo guarda como `.gitignore.txt`, no funcionará.

**Cómo se escribe**

Cada línea es una regla. Las líneas vacías se ignoran y las que empiezan por `#` son comentarios para explicar las reglas.

```gitignore
# Ignora este archivo concreto, esté en la carpeta que esté
contraseñas.txt

# Ignora la carpeta temporal y todo lo que haya dentro
temporal/
```

**Atajos (patrones) que se pueden usar**

| Atajo | Qué significa | Ejemplo | Qué ignora |
|---|---|---|---|
| `*` | Cualquier texto (también ninguno) | `*.tmp` | Todos los archivos que terminan en `.tmp` |
| `?` | Exactamente **un** carácter cualquiera | `foto?.png` | `foto1.png`, `fotoA.png`… pero **no** `foto10.png` |
| `[ ]` | Un carácter de los indicados o de un rango | `foto[0-9].png` | `foto1.png`, `foto7.png`… pero **no** `fotoA.png` |
| `/` al final | Solo carpetas | `copias/` | La carpeta `copias` y todo su contenido |
| `/` al principio | Solo en la carpeta principal del repositorio | `/notas.txt` | `notas.txt` de la carpeta principal, pero **no** `docs/notas.txt` |
| `**` | Cualquier número de carpetas | `**/borradores` | Una carpeta `borradores` esté donde esté |
| `!` | Excepción: **no** ignorar algo que una regla anterior ignoraba | `!importante.tmp` | Vuelve a incluir `importante.tmp` aunque esté `*.tmp` |
| `#` | Comentario | `# Archivos de Office` | Nada, solo es una explicación |

> 💡 Una regla **sin `/`** (como `notas.txt` o `*.tmp`) se aplica en **todas** las carpetas del repositorio. Una regla con `/` en medio (como `docs/borrador.txt`) se aplica solo a esa ruta exacta.

**Cuidado con las excepciones `!`**

Si se ignora una carpeta entera, Git ni siquiera mira lo que hay dentro, así que una excepción no puede recuperar un archivo de esa carpeta:

```gitignore
# ❌ NO funciona: importante.txt sigue ignorado
temporal/
!temporal/importante.txt

# ✅ SÍ funciona: se ignora el contenido de la carpeta, no la carpeta,
# y después se recupera el archivo que nos interesa
temporal/*
!temporal/importante.txt
```

**Ejemplo completo para un trabajo de ofimática**

```gitignore
# --- Archivos temporales de Office ---
# Word, Excel y PowerPoint crean archivos que empiezan por ~$ mientras están abiertos
~$*
*.tmp

# --- Archivos del sistema Windows ---
Thumbs.db
desktop.ini

# --- PDF exportados (se pueden volver a generar) ---
*.pdf
# ...excepto el enunciado de la práctica, que sí queremos guardar
!enunciado.pdf

# --- Datos privados ---
contraseñas.txt
datos-personales/

# --- Copias de seguridad, estén en la carpeta que estén ---
**/copias/
```

**Comprobar que funciona**

```bash
# Los archivos ignorados ya no deben aparecer en la lista de "untracked"
git status

# Dice si un archivo está ignorado y qué línea del .gitignore lo ignora.
# Si no muestra nada, el archivo NO está ignorado
git check-ignore -v contraseñas.txt
```

Ejemplo de salida de `git check-ignore -v`: `.gitignore:16:contraseñas.txt   contraseñas.txt` (archivo `.gitignore`, línea 16, regla aplicada y archivo afectado).

**¿Y si el archivo ya estaba en el repositorio?**

`.gitignore` solo afecta a archivos que Git **todavía no controla**. Si un archivo ya se había guardado en un commit, añadirlo después al `.gitignore` no hace nada. Hay que decirle a Git que deje de controlarlo:

```bash
# Saca el archivo del control de Git, pero NO lo borra de tu carpeta
git rm --cached contraseñas.txt

# Lo mismo para una carpeta entera ("-r" = con todo su contenido)
git rm -r --cached temporal/

# Guarda el cambio: a partir de ahora el .gitignore ya lo ignora
git commit -m "Deja de controlar archivos que deben ignorarse"
```

> ⚠️ El archivo sigue existiendo en los commits antiguos. Por eso las contraseñas **nunca** deben llegar a guardarse en un commit: lo mejor es crear el `.gitignore` al principio del proyecto.

**Plantillas ya hechas**
- Al crear un repositorio en GitHub se puede elegir una plantilla de `.gitignore` según el tipo de proyecto.
- En <https://github.com/github/gitignore> hay plantillas para casi cualquier programa o lenguaje.

### Práctica 4 — Detective del historial

1. En tu repositorio `receta-git`, modifica la receta (cambia una cantidad y añade un ingrediente). **Antes** de hacer `add`, captura `git diff`.
2. Haz `add` y captura `git diff --staged`. Haz commit.
3. Elige un commit antiguo y captura `git show` de ese commit.
4. Crea estos archivos y carpetas: `temporal/` con `prueba.txt` e `importante.txt` dentro, `borrador.tmp`, `apuntes.tmp`, `contraseñas.txt`, `foto1.png`, `foto2.png` y `foto10.png`. Captura `git status`.
5. Crea un `.gitignore` que, usando los atajos explicados:
   - Ignore todos los archivos `.tmp` con **una sola regla**.
   - Ignore `contraseñas.txt`.
   - Ignore `foto1.png` y `foto2.png` pero **no** `foto10.png`, con **una sola regla**.
   - Ignore el contenido de `temporal/` **excepto** `importante.txt`.
   - Tenga un comentario `#` explicando cada regla.
6. Captura `git status` después de crear el `.gitignore` y comprueba con `git check-ignore -v` qué regla ignora `apuntes.tmp` y `foto2.png`.
7. Haz commit del `.gitignore` y del resto de archivos que no estén ignorados.
8. Crea `notas-privadas.txt`, haz commit de él y **después** añádelo al `.gitignore`. Comprueba que Git lo sigue controlando y arréglalo con `git rm --cached`.
9. Responde por escrito: ¿cuántos commits tiene tu repositorio?, ¿cuál es el hash del primero?, ¿qué día y a qué hora se hizo?

**📦 Entregable:** PDF con las capturas y las respuestas.

---

## Tema 5 · Deshacer cambios

### Objetivos
- Recuperar archivos y deshacer cambios en las tres áreas.
- Corregir el último commit.
- Diferenciar `reset` y `revert` y saber cuándo usar cada uno.

### Contenidos

**Tabla resumen: "la he liado, ¿qué hago?"**

| Situación | Comando |
|---|---|
| He modificado un archivo y quiero dejarlo como estaba en el último commit | `git restore archivo.txt` |
| He hecho `add` de algo por error | `git restore --staged archivo.txt` |
| Me he equivocado en el mensaje del último commit | `git commit --amend -m "Mensaje correcto"` |
| Se me olvidó un archivo en el último commit | `git add olvidado.txt` y `git commit --amend --no-edit` |
| Quiero anular un commit **ya compartido** | `git revert <hash>` |
| Quiero eliminar commits **locales** que nadie ha visto | `git reset <hash>` |

**`git reset` — viajar atrás borrando historial**

```bash
git reset --soft HEAD~1   # Deshace el commit; los cambios quedan en staging
git reset HEAD~1          # Deshace el commit; los cambios quedan en el directorio (por defecto)
git reset --hard HEAD~1   # Deshace el commit y BORRA los cambios ⚠️
```

`HEAD~1` significa "el commit anterior al actual".

**`git revert` — anular sin borrar**

```bash
git revert a1b2c3d
```

Crea un **commit nuevo** que hace lo contrario del indicado. El historial se mantiene intacto.

> 🚦 **Regla de oro:** si el commit ya está subido a GitHub, usa `revert`. `reset` reescribe la historia y puede romper el trabajo de tus compañeros.

**Volver a ver una versión antigua (solo mirar)**

```bash
git switch --detach a1b2c3d   # Ver el proyecto tal y como estaba
git switch main               # Volver al presente
```

### Práctica 5 — Escape room de Git

Crea un repositorio `escape-room` y resuelve cada "sala". Para cada una: captura antes, comando usado y captura después.

1. **Sala 1:** Crea `diario.txt`, escribe tres líneas y haz commit. Después borra el contenido del archivo sin querer (sin hacer commit). Recupéralo.
2. **Sala 2:** Crea `secreto.txt`, haz `git add .` y date cuenta de que no querías incluirlo. Sácalo del staging sin borrarlo.
3. **Sala 3:** Haz un commit con el mensaje `asdfg`. Corrígelo por un mensaje adecuado.
4. **Sala 4:** Haz un commit y date cuenta de que te faltaba un archivo. Inclúyelo en ese mismo commit.
5. **Sala 5:** Haz un commit que añada una línea incorrecta en `diario.txt`. Anúlalo con `revert` y explica qué ha pasado en el historial.
6. **Sala 6:** Haz dos commits de prueba y elimínalos con `reset` (sin `--hard`). ¿Dónde han quedado los cambios?

**Pregunta final:** explica con tus palabras la diferencia entre `reset` y `revert` y pon un ejemplo de cuándo usarías cada uno.

**📦 Entregable:** PDF con las capturas de las 6 salas y la respuesta final.

---

## Tema 6 · Repositorios remotos con GitHub

### Objetivos
- Entender qué es un repositorio remoto.
- Hacer una subida completa de un repositorio local a GitHub.
- Sincronizar cambios en ambas direcciones.

### Contenidos

**¿Qué es un repositorio remoto?**

Hasta ahora el repositorio solo existía en tu ordenador. Un **repositorio remoto** es una copia del mismo alojada en internet (en nuestro caso, en GitHub). Sirve para:
- Tener una **copia de seguridad** del proyecto y su historial.
- **Trabajar desde varios ordenadores** (el de clase y el de casa).
- **Compartir** el proyecto y colaborar con otras personas.

```
   Tu ordenador                                GitHub
 ┌──────────────────┐     git push ──▶     ┌──────────────────┐
 │ Repositorio local │                      │ Repositorio remoto│
 └──────────────────┘     ◀── git pull      └──────────────────┘
```

> En este tema trabajamos solo con la rama principal, `main`. De momento basta con saber que es la línea principal del proyecto donde hemos hecho todos los commits; las ramas se explican en el tema siguiente.

**Autenticación**

GitHub no acepta la contraseña de la cuenta desde la terminal. En Windows, **Git Credential Manager** (se instala junto con Git) abre el navegador la primera vez que subes algo: inicias sesión en GitHub, autorizas y queda guardado para las siguientes veces.

> ⚠️ Comprobad que el email configurado en Git (`git config user.email`) es el de vuestra cuenta de GitHub; si no, los commits no aparecerán asociados a vuestro perfil.

**Subida completa paso a paso**

Vamos a subir el repositorio `receta-git` que creamos en el Tema 3.

**Paso 1 · Crear el repositorio vacío en GitHub**
1. En GitHub, pulsar el botón **+** (arriba a la derecha) → **New repository**.
2. *Repository name*: `receta-git` (mejor el mismo nombre que la carpeta local).
3. Elegir **Public** para que el profesor pueda verlo.
4. **No marcar** *Add a README file*, *.gitignore* ni *license*: el repositorio debe estar **vacío**, porque el contenido ya lo tenemos en local.
5. Pulsar **Create repository** y copiar la dirección HTTPS que aparece (`https://github.com/usuario/receta-git.git`).

**Paso 2 · Comprobar el repositorio local antes de subir**

```bash
cd ~/Documentos/practicas-git/receta-git   # Entra en la carpeta del repositorio local
git status                                 # Debe decir "nothing to commit": todo guardado en commits
git log --oneline                          # Muestra los commits que se van a subir
```

> Solo se suben los **commits**. Si `git status` muestra cambios sin guardar, haz antes `git add` y `git commit`.

**Paso 3 · Enlazar el repositorio local con GitHub**

```bash
# Le dice al repositorio local dónde está su copia en GitHub.
# "origin" es el nombre que damos al remoto (es el nombre habitual)
# y después va la dirección copiada en el paso 1
git remote add origin https://github.com/usuario/receta-git.git

# Muestra los remotos enlazados para comprobar que la dirección es correcta
# (aparece dos veces: una para descargar "fetch" y otra para subir "push")
git remote -v
```

**Paso 4 · Primera subida**

```bash
# Sube los commits de la rama main al remoto origin.
# "-u" deja enlazada la rama local con la de GitHub, así las próximas
# veces basta con escribir "git push"
git push -u origin main
```

La primera vez se abrirá el navegador para iniciar sesión en GitHub.

**Paso 5 · Comprobar en GitHub**

Recarga la página del repositorio: deben aparecer los archivos. Pulsando en **commits** verás el mismo historial que con `git log`, con los mismos mensajes, autores y fechas.

**Paso 6 · Las siguientes subidas**

A partir de ahora el ciclo de trabajo es siempre el mismo:

```bash
# (editas archivos)
git add .                                  # Prepara los cambios
git commit -m "Añade tiempo de preparación"  # Los guarda en el historial local
git push                                   # Sube los nuevos commits a GitHub
```

**Errores habituales en la primera subida**

| Mensaje de error | Qué significa | Solución |
|---|---|---|
| `remote origin already exists` | Ya habías enlazado un remoto | `git remote set-url origin <url>` para cambiar la dirección |
| `src refspec main does not match any` | No hay commits o la rama no se llama `main` | Haz un commit primero; comprueba el nombre de la rama con `git status` |
| `rejected ... fetch first` | En GitHub hay commits que tú no tienes (por ejemplo, marcaste "Add README") | Haz `git pull` antes de `git push` |
| `Repository not found` | La dirección está mal escrita | Revisa la URL con `git remote -v` |

**Descargar un repositorio**

```bash
# Descarga el repositorio completo (archivos e historial) en una carpeta nueva
# con el mismo nombre, ya enlazado con GitHub
git clone https://github.com/usuario/repositorio.git
```

**Sincronizar**

| Comando | Qué hace |
|---|---|
| `git push` | Sube mis commits al remoto |
| `git fetch` | Descarga los cambios del remoto **sin aplicarlos** |
| `git pull` | Descarga **y aplica** los cambios del remoto en tus archivos |

> 💡 Rutina recomendada: `git pull` antes de empezar a trabajar y `git push` al terminar.

**El archivo README.md**

Es la portada del repositorio en GitHub. Se escribe en **Markdown**:

```markdown
# Título
## Subtítulo
**negrita** y *cursiva*
- elemento de lista
[enlace](https://ejemplo.com)
![imagen](foto.png)
```

### Práctica 6 — Mi repositorio en la nube

1. **Subida completa de `receta-git`:** sigue los 6 pasos explicados. Captura el repositorio vacío recién creado en GitHub, la salida de `git remote -v`, la de `git push -u origin main` y la página del repositorio con los archivos.
2. Comprueba que el historial de GitHub coincide con el local: captura la lista de commits en GitHub junto a `git log --oneline`.
3. Sube también el repositorio `escape-room` del Tema 5 siguiendo los mismos pasos.
4. Añade a `receta-git` un `README.md` con: título, descripción, una lista y un enlace. Hazlo en local, haz commit y súbelo con `git push`.
5. Edita el README **directamente desde la web de GitHub** (botón del lápiz) y haz el commit allí.
6. En local, trae ese cambio con `git pull` y comprueba con `cat README.md` que aparece.
7. Borra la carpeta local de `receta-git` y recupérala con `git clone`. Comprueba con `git log --oneline` que el historial completo ha vuelto.

**📦 Entregable:** enlaces a los dos repositorios públicos y PDF con las capturas de cada paso.

---

## Tema 7 · Ramas

### Objetivos
- Entender para qué sirven las ramas.
- Crear ramas, moverse entre ellas y fusionarlas.
- Resolver conflictos.

### Contenidos

**¿Para qué sirven?** Permiten trabajar en algo nuevo sin estropear la versión que funciona. Ejemplo: tienes un currículum terminado (`main`) y quieres probar un diseño nuevo. Creas una rama `diseño-nuevo`; si te gusta, la fusionas; si no, la borras.

```
main:          A───B───────────E  (merge)
                    \         /
diseño-nuevo:        C───────D
```

**Comandos**

```bash
git branch                    # Lista las ramas (* = la actual)
git branch diseño-nuevo       # Crea una rama
git switch diseño-nuevo       # Cambia a esa rama
git switch -c otra-rama       # Crea y cambia a la vez
git merge diseño-nuevo        # Fusiona diseño-nuevo en la rama actual
git branch -d diseño-nuevo    # Borra una rama ya fusionada
```

**Ejemplo**

```bash
git switch -c apartado-idiomas    # Crea la rama "apartado-idiomas" y se cambia a ella

# Añade una línea al final de cv.md
echo "## Idiomas: euskera, castellano, inglés B1" >> cv.md

git add cv.md                              # Prepara el cambio
git commit -m "Añade apartado de idiomas"  # Lo guarda en la rama apartado-idiomas

git switch main                   # Vuelve a main: cv.md ya no tiene los idiomas
git merge apartado-idiomas        # Trae a main los cambios de la rama: ahora sí aparecen
git branch -d apartado-idiomas    # Borra la rama, ya no hace falta porque está fusionada
```

**Conflictos**

Ocurren cuando dos ramas modifican **la misma línea** del mismo archivo. Git no sabe cuál elegir y marca el archivo así:

```
<<<<<<< HEAD
Teléfono: 944 000 000
=======
Teléfono: 600 111 222
>>>>>>> cambio-telefono
```

**Cómo resolverlo:**
1. Abrir el archivo (VS Code ofrece botones: *Accept Current*, *Accept Incoming*, *Accept Both*).
2. Dejar el contenido correcto y borrar las marcas `<<<<<<<`, `=======` y `>>>>>>>`.
3. `git add archivo` y `git commit`.

### Práctica 7 — Mi currículum con ramas

1. Crea el repositorio `cv-git` con un archivo `cv.md` que contenga: nombre, datos de contacto y formación. Commit en `main`.
2. Crea la rama `experiencia`, añade un apartado de experiencia (puede ser inventada o de prácticas) y haz commit.
3. Crea desde `main` la rama `idiomas`, añade un apartado de idiomas y haz commit.
4. Fusiona las dos ramas en `main`.
5. **Provoca un conflicto:** crea las ramas `telefono-casa` y `telefono-movil`; en cada una cambia la misma línea del teléfono con un número distinto y haz commit. Fusiona las dos en `main` y resuelve el conflicto.
6. Borra las ramas ya fusionadas.
7. Captura `git log --oneline --graph --all`.
8. Sube `cv-git` a GitHub siguiendo la subida completa del Tema 6 y comprueba en la web (*Insights → Network*) que se ve el gráfico de ramas.

**📦 Entregable:** enlace al repositorio `cv-git` y PDF con capturas de cada paso, especialmente del archivo con el conflicto **antes y después** de resolverlo, y el gráfico final.

---

## Tema 8 · Trabajo colaborativo

### Objetivos
- Trabajar varias personas sobre el mismo repositorio.
- Contribuir mediante fork y pull request.
- Aplicar un flujo de trabajo en equipo.

### Contenidos

**Dos formas de colaborar**

| Forma | Cuándo se usa | Cómo |
|---|---|---|
| **Colaborador** | Equipo de confianza (compañeros de clase, empresa) | El dueño invita: *Settings → Collaborators* |
| **Fork + Pull Request** | Proyectos ajenos o abiertos | Copias el repo a tu cuenta y propones cambios |

**Pull Request (PR)**

Es una **propuesta de cambios**: "he hecho esto en mi rama, ¿lo incorporáis?". Permite revisar, comentar y aprobar antes de fusionar.

**GitHub Flow (flujo de trabajo recomendado)**

1. `main` siempre debe funcionar.
2. Para cada tarea, crear una rama con nombre descriptivo:
   ```bash
   git switch -c añade-seccion-contacto   # Crea la rama de la tarea y se cambia a ella
   ```
3. Hacer commits en esa rama y subirla:
   ```bash
   # Sube la rama a GitHub (que todavía no la tiene) y la deja enlazada
   git push -u origin añade-seccion-contacto
   ```
4. En GitHub, abrir una **Pull Request** hacia `main`.
5. Un compañero la revisa, comenta y aprueba.
6. Se fusiona (*Merge pull request*) y se borra la rama.
7. Todos actualizan su `main`:
   ```bash
   git switch main   # Vuelve a la rama principal
   git pull          # Descarga y aplica los cambios fusionados en GitHub
   ```

**Fork paso a paso**
1. En el repositorio ajeno, pulsar **Fork**.
2. Clonar **tu** fork.
3. Crear rama, hacer cambios, `push` a tu fork.
4. En GitHub, abrir una PR desde tu fork al repositorio original.

### Práctica 8 — Revista digital de clase

Grupos de 3–4 personas.

1. Una persona crea el repositorio `revista-grupoX` con un `README.md` (portada de la revista) e invita al resto como colaboradores.
2. Cada miembro:
   - Crea una rama `articulo-nombre`.
   - Escribe un artículo en `articulos/nombre.md` (mínimo 150 palabras sobre un tema tecnológico).
   - Añade un enlace a su artículo en el índice del `README.md` (¡aquí aparecerán conflictos!).
   - Abre una Pull Request.
3. Cada PR debe ser revisada por **otro miembro**, que deja al menos un comentario antes de aprobarla.
4. Resolved los conflictos que surjan y fusionad todas las PR.
5. **Individual:** haz un fork del repositorio de **otro grupo**, corrige una errata o añade una mejora y envíales una PR.

**📦 Entregable:** enlace al repositorio del grupo, enlace a la PR enviada al otro grupo y un PDF individual explicando qué conflicto tuvisteis y cómo lo resolvisteis.

---

## Tema 9 · Extras útiles

### Objetivos
- Marcar versiones con etiquetas.
- Guardar cambios temporalmente.
- Usar Git desde herramientas gráficas.
- Publicar una web gratuita con GitHub Pages.

### Contenidos

**Etiquetas (`git tag`)**: marcan versiones importantes.

```bash
git tag -a v1.0 -m "Primera versión entregable"
git tag                       # Listar etiquetas
git push origin v1.0          # Las etiquetas no se suben con un push normal
```

En GitHub se pueden convertir en **Releases**.

**`git stash`**: guarda cambios a medias para cambiar de tarea sin hacer commit.

```bash
git stash                     # Guarda y deja el directorio limpio
git stash list                # Ver lo guardado
git stash pop                 # Recuperar lo guardado
```

Ejemplo: estás redactando algo en `main` y te piden una corrección urgente en otra rama. `stash`, cambias de rama, corriges, vuelves y `stash pop`.

**Herramientas gráficas**
- **Visual Studio Code:** pestaña *Source Control* (Ctrl+Shift+G): ver cambios, hacer stage con `+`, commit, push/pull, cambiar de rama en la barra inferior y resolver conflictos con botones.
- **GitHub Desktop:** aplicación sencilla para todo el flujo básico sin terminal.

> Saber usar la terminal permite entender lo que hacen estos botones y solucionar problemas cuando algo falla.

**GitHub Pages**: publica gratis una web estática desde un repositorio.
1. Repositorio con un `index.html` en la raíz.
2. *Settings → Pages → Branch: main → Save*.
3. En unos minutos la web estará en `https://usuario.github.io/repositorio/`.

### Práctica 9 — Mi portfolio web

1. Crea el repositorio `portfolio` con un `index.html` sencillo: tu nombre, una breve presentación y enlaces a tus repositorios anteriores. (Se proporcionará una plantilla HTML básica.)
2. Haz **al menos 3 commits desde VS Code** (sin terminal). Captura el panel de Source Control.
3. Mientras editas, simula una interrupción: usa `git stash`, cambia algo en otra rama, vuelve y recupera los cambios con `git stash pop`.
4. Etiqueta la versión como `v1.0` y súbela. Crea una Release en GitHub.
5. Publica la web con GitHub Pages.

**📦 Entregable:** URL pública del portfolio, enlace al repositorio y PDF con capturas de VS Code, `stash` y la Release.

---

## Tema 10 · Proyecto final

### Descripción

Por grupos de 3–4 personas, crearéis una **guía web sobre un tema elegido por el grupo** (por ejemplo: "Guía de ofimática para principiantes", "Rutas por Bizkaia", "Guía de hardware para montar un PC"), aplicando todo lo aprendido.

### Requisitos obligatorios

**Repositorio y organización**
- [ ] Repositorio en GitHub con todos los miembros como colaboradores.
- [ ] `README.md` completo: descripción, miembros, reparto de tareas y enlace a la web.
- [ ] `.gitignore` adecuado.
- [ ] Uso de **Issues** de GitHub para repartir las tareas (al menos una por miembro).

**Flujo de trabajo**
- [ ] Rama `main` protegida: solo se modifica mediante Pull Requests.
- [ ] Mínimo **3 Pull Requests por miembro**, cada una revisada por otro compañero.
- [ ] Mínimo **10 commits por miembro** con mensajes correctos.
- [ ] Al menos un conflicto resuelto y documentado.

**Resultado**
- [ ] Web publicada con GitHub Pages (mínimo una página por miembro).
- [ ] Al menos dos versiones etiquetadas (`v1.0` y `v2.0`) con su Release.

### Entregables
1. Enlace al repositorio.
2. Enlace a la web publicada.
3. Memoria individual en PDF (2–3 páginas): qué has hecho, tus PR, el conflicto más difícil y cómo lo resolvisteis, y qué has aprendido.
4. Exposición en clase (5–10 minutos por grupo) mostrando el historial (`git log --graph`) y la web.

### Rúbrica de evaluación

| Criterio | Peso | Excelente (10) | Adecuado (6) | Insuficiente (3) |
|---|---|---|---|---|
| Commits | 20 % | Frecuentes, pequeños y con mensajes claros | Suficientes, algunos mensajes poco claros | Pocos, grandes o con mensajes sin sentido |
| Ramas y Pull Requests | 25 % | Todas las aportaciones vía PR revisada con comentarios útiles | Uso de PR con revisión superficial | Trabajo directo en `main` |
| Colaboración y conflictos | 15 % | Conflicto resuelto correctamente y bien explicado | Conflicto resuelto con explicación pobre | No se resuelve o no se documenta |
| Repositorio (README, Issues, .gitignore, tags) | 15 % | Completo y bien organizado | Faltan algunos elementos | Desordenado o incompleto |
| Web publicada | 10 % | Funciona, completa y cuidada | Funciona con carencias | No publicada o rota |
| Memoria y exposición | 15 % | Clara, reflexiva y demuestra dominio | Correcta pero superficial | Incompleta o no demuestra comprensión |

> 💡 El historial de Git permite comprobar objetivamente la aportación de cada miembro: *Insights → Contributors* en GitHub.

---

## Anexo · Chuleta de comandos

| Categoría | Comando | Para qué sirve |
|---|---|---|
| Configuración | `git config --global user.name "Nombre"` | Configurar el nombre |
| | `git config --global user.email "email"` | Configurar el email |
| Inicio | `git init` | Crear un repositorio |
| | `git clone <url>` | Descargar un repositorio |
| Básico | `git status` | Ver el estado |
| | `git add <archivo>` / `git add .` | Preparar cambios |
| | `git commit -m "mensaje"` | Guardar cambios |
| Historial | `git log --oneline --graph --all` | Ver historial |
| | `git diff` / `git diff --staged` | Ver diferencias |
| | `git show <hash>` | Ver un commit |
| Deshacer | `git restore <archivo>` | Descartar cambios |
| | `git restore --staged <archivo>` | Sacar del staging |
| | `git commit --amend` | Corregir el último commit |
| | `git revert <hash>` | Anular un commit (seguro) |
| | `git reset <hash>` | Volver atrás (solo local) |
| Remoto | `git remote add origin <url>` | Enlazar con GitHub |
| | `git remote -v` | Ver los remotos enlazados |
| | `git push -u origin main` | Primera subida |
| | `git push` / `git pull` / `git fetch` | Sincronizar |
| Ramas | `git branch` | Listar ramas |
| | `git switch -c <rama>` | Crear y cambiar de rama |
| | `git switch <rama>` | Cambiar de rama |
| | `git merge <rama>` | Fusionar |
| | `git branch -d <rama>` | Borrar rama |
| Extras | `git tag -a v1.0 -m "msg"` | Etiquetar versión |
| | `git stash` / `git stash pop` | Guardar y recuperar cambios temporales |

---

### Recursos recomendados
- Libro oficial *Pro Git* (en español, gratuito): <https://git-scm.com/book/es/v2>
- Práctica visual de ramas: <https://learngitbranching.js.org/?locale=es_ES>
- Documentación de GitHub en español: <https://docs.github.com/es>
