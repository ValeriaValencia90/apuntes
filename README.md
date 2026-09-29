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
# Apuntes y Guía de JavaScript (JS)

Esta guía organiza los conceptos básicos de manipulación de arreglos (Arrays), interacción con el **DOM** y el **BOM**, y manejo de eventos.

---

## 1. Métodos de Arrays

Los arrays (o arreglos) nos permiten almacenar listas de elementos. JavaScript ofrece varios métodos integrados para manipularlos:

```javascript
const peliculas = ["Matrix", "Inception", "Alien"];

// .push(): Añade un elemento al final del array
peliculas.push("Terror"); 

// .pop(): Elimina el último elemento del array
peliculas.pop(); 

// .indexOf(): Busca la posición (índice) de un elemento. Devuelve -1 si no lo encuentra
const indice = peliculas.indexOf("Terror"); 

// .slice(): Extrae una sección del array y devuelve un nuevo array
const subArray = peliculas.slice(1); 

// .join(): Convierte todos los elementos de un array en un string (texto) unido por un separador
const texto = peliculas.join(", "); 

// .split(): Método de String para convertir un texto en un array (dividido por un separador)
const cadena = "hola mundo";
const arrayDesdeTexto = cadena.split(" "); 

// .sort(): Ordena los elementos del array.
// Para números, se utiliza una función de comparación:
const numeros = [5, 2, 8, 1];
numeros.sort((a, b) => a - b); // Ordena de menor a mayor

// .reverse(): Invierte el orden del array
peliculas.reverse(); 

// .find(): Busca y devuelve el primer elemento que cumpla con la condición
const encontrado = peliculas.find(pelicula => pelicula === "Matrix");

// .some(): Comprueba si al menos un elemento cumple una condición (devuelve true o false)
const precios = [10, 5, 20];
const hayMayorOIgualOcho = precios.some(precio => precio >= 8); 

// .forEach(): Recorre cada elemento del array
peliculas.forEach(pelicula => {
  console.log(pelicula);
});

// Iterador for...in: Recorre los índices (o claves) de una estructura
for (let i in peliculas) {
  console.log(i, peliculas[i]);
}
```

---

## 2. Funciones Básicas de Entrada y Salida

```javascript
// prompt(): Muestra un diálogo para que el usuario introduzca texto
let entrada = prompt("Introduce tu nombre:");

// parseInt(): Convierte un string o valor a número entero
let numero = parseInt("42");

// document.write(): Escribe contenido directamente en el documento HTML (no recomendado en producción)
document.write("<h1>Contenido Array</h1>");
```

---

## 3. Manejo del DOM (Document Object Model)

El **DOM** representa los elementos estructurales que forman parte de una página web en forma de árbol de nodos.

### Selección de Elementos

```javascript
// Seleccionar por ID
const caja = document.getElementById("caja");

// Seleccionar por selector CSS (ID, clase o etiqueta)
const cajaQuery = document.querySelector("#micaja");

// Seleccionar múltiples elementos por su etiqueta HTML
const todosLosDivs = document.getElementsByTagName("div");
```

### Modificación de Estilos y Propiedades

```javascript
// Modificar contenido CSS mediante la propiedad style
caja.style.background = "red";
caja.style.padding = "20px";
caja.style.color = "white";

// Modificar o asignar la clase CSS
caja.className = "mi-clase-personalizada";

// Obtener o modificar texto/HTML interno
console.log(caja.textContent); // Obtiene solo el texto
caja.textContent = "Nuevo texto";

caja.innerHTML = "<strong>Otro texto</strong>"; // Asigna HTML interno
```

### Creación e Inserción de Elementos

```javascript
// Crear una etiqueta HTML y un nodo de texto
const nuevoParrafo = document.createElement("p");
const textoParrafo = document.createTextNode("Este es un texto de prueba.");

// Unir el texto al párrafo e insertarlo en el padre
nuevoParrafo.appendChild(textoParrafo);
document.body.appendChild(nuevoParrafo);

// Métodos modernos de inserción:
// .append(): Añade elementos o texto al final dentro del contenedor
caja.append(nuevoParrafo);

// .prepend(): Añade elementos o texto al inicio dentro del contenedor
caja.prepend(nuevoParrafo);

// Inspeccionar el tipo de variable o elemento
console.log(typeof nuevoParrafo);
```

---

## 4. Manejo del BOM (Browser Object Model)

El **BOM** permite interactuar con el navegador fuera del contenido de la página web.

```javascript
// Obtener las dimensiones de la ventana del navegador (viewport)
console.log(window.innerWidth);
console.log(window.innerHeight);

// Obtener la resolución total de la pantalla del usuario
console.log(screen.width);
console.log(screen.height);

// Obtener o cambiar la URL actual de la página
console.log(window.location.href);

// Abrir una nueva ventana o pestaña del navegador
window.open("https://www.google.com");
```

---

## 5. Eventos en JavaScript

Los eventos permiten ejecutar código en respuesta a las acciones del usuario.

### Eventos de Ratón (*Mouse Events*)

* `click`: Se dispara cuando se hace clic sobre un elemento.
* `dblclick`: Se dispara con un doble clic.
* `mouseover`: Se dispara cuando el puntero del ratón entra en un elemento.
* `mouseout`: Se dispara cuando el puntero del ratón sale de un elemento.

```javascript
const boton = document.querySelector("#miBoton");

// Escuchador de eventos recomendada (addEventListener)
boton.addEventListener("click", () => {
  console.log("¡Has hecho clic en el botón!");
});
```
