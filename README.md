# Guía Básica y Apuntes de Git

Este documento contiene un resumen práctico de los comandos fundamentales para trabajar con Git y la línea de comandos, organizado por etapas de trabajo.

---

## 1. Comandos del Sistema (Terminal)

Comandos básicos de la terminal para navegar y gestionar carpetas antes de usar Git:

* **Muestra la ruta del directorio/ubicación actual:**
  ```bash
  pwd
  ```
* **Crea una nueva carpeta o directorio:**
  ```bash
  mkdir nombre_carpeta
  ```
* **Verifica la versión instalada de Git:**
  ```bash
  git -v
  # o también:
  git --version
  ```

---

## 2. Configuración Inicial de Git

Antes de realizar confirmaciones (*commits*), es necesario configurar la identidad del usuario a nivel global. Esta información se adjuntará a cada commit.

```bash
# Establecer nombre de usuario
git config --global user.name "Tu Nombre"

# Establecer correo electrónico
git config --global user.email "tu_email@example.com"
```

---

## 3. Inicialización y Estado del Repositorio

* **Inicializar un repositorio Git:** Crea la carpeta oculta `.git` en el directorio actual para comenzar el control de versiones.
  ```bash
  git init
  ```

* **Consultar el estado del proyecto:** Muestra los archivos modificados, en *staging* o no rastreados (*untracked*).
  ```bash
  git status
  ```

---

## 4. Flujo Básico de Trabajo (Fotografía del Proyecto)

### Añadir y Confirmar Cambios

* **Añadir un archivo al área de preparación (*Staging Area*):**
  ```bash
  git add hellogit.py
  # Para añadir todos los archivos modificados:
  git add .
  ```

* **Crear un *commit* (guardar cambios):** Crea un punto en el historial. Cada *commit* genera un ID único (hash).
  ```bash
  git commit -m "Este es mi primer commit"
  ```

---

## 5. Historial y Navegación de Commits

* **Ver el historial de commits:**
  ```bash
  git log
  ```

* **Ver las diferencias entre archivos y versiones:**
  ```bash
  git diff
  ```

* **Navegar a un commit específico o cambiar de estado:**
  ```bash
  git checkout <ID_DEL_COMMIT>
  # Ejemplo:
  git checkout c2294f2f2e31e653942069539838adb8c255a269
  ```

* **Deshacer o reiniciar cambios a un commit específico:**
  ```bash
  git reset --hard <ID_DEL_COMMIT>
  # Ejemplo:
  git reset --hard 123414
  ```

* **Ver el historial completo de acciones (incluye acciones eliminadas):**
  ```bash
  git reflog
  ```

---

## 6. Personalización e Historial Gráfico (Alias)

Para ver el historial de commits de forma gráfica y simplificada en una sola línea:

```bash
git log --graph --pretty=oneline
```

### Crear un Alias para simplificar el comando anterior
Puedes crear un comando personalizado llamado `git tree` para ejecutar ese informe gráfico de forma rápida:

```bash
# Crear el alias global
git config --global alias.tree "log --graph --pretty=oneline"

# Uso del nuevo comando personalizado
git tree
```

---

## 7. Ignorar Archivos (`.gitignore`)

Si deseas evitar que ciertos archivos o carpetas se suban al repositorio (por ejemplo, archivos de configuración, bases de datos locales o credenciales):

1. **Crear el archivo `.gitignore`:**
   ```bash
   touch .gitignore
   ```
2. **Añadir dentro del archivo `.gitignore` los nombres de los archivos o carpetas que deseas omitir:**
   ```text
   # Ejemplo de contenido dentro de .gitignore
   secretos.txt
   *.log
   node_modules/
   ```

---

## 8. Etiquetas, Ramas y Fusión (*Tags, Branches & Merges*)

### Crear Etiquetas (*Tags*)
Las etiquetas permiten marcar puntos específicos en el historial (por ejemplo, versiones de lanzamiento o clases):

```bash
git tag clase_1
```

### Gestión de Ramas (*Branches*)

* **Crear una nueva rama:**
  ```bash
  git branch login
  ```

* **Cambiar a una rama existente:**
  ```bash
  git switch login
  # o mediante el comando tradicional:
  git checkout login
  ```

* **Fusionar ramas (*Merge*):** Unir los cambios de otra rama (por ejemplo, `login`) a la rama principal (`main`). Primero asegúrate de estar posicionado en la rama destino (`main`).
  ```bash
  git switch main
  git merge login
  ```
