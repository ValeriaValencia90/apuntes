# JavaScript de 0 a experto (edición 2026)

> Guía completa, explicada de forma sencilla y con ejemplos, actualizada hasta **ECMAScript 2026** e incluyendo lo que ya está aprobado para **ECMAScript 2027** (Temporal y `using`).
>
> Las novedades se marcan con su edición: **(ES2022)**, **(ES2025)**… y las de este año con ⭐ **(ES2026)**.

## Cómo usar esta guía

- Cada capítulo tiene: **explicación**, **ejemplos** y, al final, **ideas clave**.
- Copia los ejemplos y ejecútalos. Aprender JS leyendo sin escribir código no funciona.
- Al final de cada nivel hay una sección de **ejercicios** (45 en total) con su dificultad (🟢 fácil · 🟡 medio · 🔴 difícil) y la solución plegada: intenta resolverlos antes de abrirla.
- Los ejemplos de los niveles 0–4 funcionan en cualquier **Node.js 22 o superior** y en cualquier navegador actual.
- Las novedades de **ES2025 y ES2026** son muy recientes: necesitan la última versión de Chrome, Firefox, Safari o Node. Si tu entorno aún no las tiene, puedes probarlas con el polyfill **core-js** (se explica en el capítulo 56). Para Temporal existe el polyfill `@js-temporal/polyfill`.

## Índice

- **Nivel 0 — Fundamentos y entorno** (cap. 1–4)
- **Nivel 1 — El lenguaje básico** (cap. 5–12)
- **Nivel 2 — Funciones y estructuras de datos** (cap. 13–24)
- **Nivel 3 — Programación orientada a objetos** (cap. 25–31)
- **Nivel 4 — Asincronía** (cap. 32–39)
- **Nivel 5 — Iteradores, generadores y metaprogramación** (cap. 40–45)
- **Nivel 6 — Errores, módulos y datos binarios** (cap. 46–53)
- **Nivel 7 — Lo que llega en ES2027** (cap. 54–56)
- **Nivel 8 — JavaScript profesional** (cap. 57–65)
- Cada nivel termina con sus **ejercicios** (🏋️)
- **Anexo — Tabla de novedades por edición**

---

# NIVEL 0 — Fundamentos y entorno

## 1. Qué es JavaScript

JavaScript (JS) es un lenguaje de programación creado en 1995 por Brendan Eich en solo 10 días para dar interactividad a las páginas web. Hoy se usa en todas partes: webs, servidores, apps móviles, apps de escritorio e incluso microcontroladores.

### JavaScript vs ECMAScript

- **ECMAScript** es la *especificación*: el documento oficial que dice cómo debe comportarse el lenguaje. Su nombre técnico es **ECMA-262**.
- **JavaScript** es la *implementación* que usamos (en Chrome, Firefox, Node…).

Piensa en ECMAScript como "las reglas del ajedrez" y en JavaScript como "el tablero concreto con el que juegas".

### TC39 y el proceso de propuestas

El comité **TC39** (empresas como Google, Mozilla, Apple, Microsoft, Bloomberg…) decide qué entra en el lenguaje. Cada nueva funcionalidad pasa por fases:

| Stage | Significado |
|---|---|
| 0 | Idea inicial |
| 1 | Propuesta formal: el comité considera que merece estudio |
| 2 | Borrador de la especificación |
| 2.7 | Especificación aprobada, faltan tests |
| 3 | Lista para implementarse en los navegadores |
| 4 | Terminada: entra en la siguiente edición anual |

### Ediciones anuales

Desde 2015 sale una edición cada año (en junio):

- **ES2015 (ES6)**: el gran salto: `let`/`const`, clases, arrow functions, promesas, módulos…
- **ES2016 – ES2024**: mejoras incrementales.
- **ES2025**: iterator helpers, métodos de `Set`, `Promise.try`, `RegExp.escape`…
- **ES2026** (aprobada el 30 de junio de 2026): 7 novedades de la librería estándar, sin sintaxis nueva.
- **ES2027** (prevista para junio de 2027): Temporal, `using`/`await using`…

> **Ideas clave**: JavaScript implementa ECMAScript. TC39 decide las novedades. Hay una versión nueva cada año.

## 2. Dónde se ejecuta JavaScript

El código JS necesita un **motor** (engine) que lo ejecute:

| Motor | Dónde está |
|---|---|
| V8 | Chrome, Edge, Node.js, Deno |
| SpiderMonkey | Firefox |
| JavaScriptCore | Safari, Bun |

Y un **entorno** (runtime) que le da "poderes" extra:

- **Navegador**: te da `document`, `window`, `fetch`, eventos de ratón… (el DOM).
- **Node.js**: te da acceso a archivos, red, procesos… No tiene `document`.
- **Deno** y **Bun**: alternativas modernas a Node, con TypeScript integrado.

```js
// Esto funciona en el navegador, pero NO en Node:
document.title = "Hola";

// Esto funciona en Node, pero NO en el navegador:
import { readFile } from "node:fs/promises";
```

El lenguaje (variables, funciones, arrays…) es el mismo en todos los entornos. Lo que cambia son las APIs disponibles.

> **Ideas clave**: el motor ejecuta el lenguaje; el entorno aporta las APIs (DOM en navegador, sistema de archivos en Node).

## 3. Herramientas

### Lo mínimo que necesitas

1. **Visual Studio Code**: editor de código.
2. **Node.js** (versión LTS): para ejecutar JS fuera del navegador. Se descarga en nodejs.org.
3. **Un navegador** con DevTools (Chrome, Firefox, Edge).

### Comprobar que Node está instalado

Abre una terminal y escribe:

```bash
# Muestra la versión de Node instalada (debe ser 22 o superior)
node --version

# Muestra la versión de npm, el gestor de paquetes que viene con Node
npm --version
```

### Formas de ejecutar JS

**a) La consola del navegador**: pulsa `F12` → pestaña *Console* y escribe:

```js
2 + 2          // 4
"Hola".length  // 4
```

**b) El REPL de Node** (una consola interactiva en la terminal):

```bash
# Abre la consola interactiva de Node; sales con Ctrl+D o escribiendo .exit
node
```

**c) Ejecutar un archivo**:

```bash
# Ejecuta el archivo app.js una vez
node app.js

# Ejecuta app.js y lo vuelve a ejecutar automáticamente cada vez que guardas cambios
node --watch app.js
```

### console: tu mejor amigo para depurar

```js
console.log("Mensaje normal");
console.error("Algo ha ido mal");
console.warn("Cuidado");
console.table([{ nombre: "Ana", edad: 30 }, { nombre: "Luis", edad: 25 }]);
console.time("bucle");
for (let i = 0; i < 1e6; i++) {}
console.timeEnd("bucle"); // bucle: 2.1ms
```

> **Ideas clave**: VS Code + Node + navegador. Usa `console.log` y `console.table` sin miedo.

## 4. Tu primer programa

### En el navegador

Crea `index.html`:

```html
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Mi primer JS</title>
</head>
<body>
  <h1 id="titulo">Hola</h1>

  <!-- type="module" activa los módulos modernos y el modo estricto -->
  <script type="module" src="app.js"></script>
</body>
</html>
```

Y `app.js`:

```js
const titulo = document.querySelector("#titulo");
titulo.textContent = "¡Hola desde JavaScript!";
console.log("El script se ha cargado");
```

¿Por qué `type="module"`?

- Permite usar `import` / `export`.
- Activa automáticamente el **modo estricto** (detecta más errores).
- Se ejecuta **después** de que el HTML esté cargado (como `defer`).

### En Node

Crea `hola.mjs` (la extensión `.mjs` le dice a Node que es un módulo moderno):

```js
const nombre = "Alberto";
console.log(`Hola, ${nombre}`);
```

```bash
# Ejecuta el archivo hola.mjs con Node
node hola.mjs
```

> Alternativa a `.mjs`: añadir `"type": "module"` en el `package.json` del proyecto, y así todos los `.js` se tratan como módulos.

> **Ideas clave**: en web, usa siempre `<script type="module">`. En Node, `.mjs` o `"type": "module"`.

---

# NIVEL 1 — El lenguaje básico

## 5. Variables: `let`, `const` y `var`

Una variable es una "caja con nombre" donde guardas un valor.

```js
let edad = 30;       // puede cambiar
const PI = 3.1416;   // no se puede reasignar
var antiguo = "no"; // forma antigua: evítala
```

### `const` por defecto, `let` cuando necesites reasignar

```js
const nombre = "Ana";
nombre = "Luis"; // ❌ TypeError: Assignment to constant variable

let contador = 0;
contador = contador + 1; // ✅
```

**Ojo**: `const` impide *reasignar*, no *modificar* el contenido de un objeto:

```js
const usuario = { nombre: "Ana" };
usuario.nombre = "Luis"; // ✅ se modifica el contenido
usuario = {};            // ❌ no se puede reasignar
```

### ¿Por qué evitar `var`?

1. **No respeta los bloques** `{ }`:

```js
if (true) {
  var a = 1;
  let b = 2;
}
console.log(a); // 1  😱 se "escapa" del bloque
console.log(b); // ReferenceError: b is not defined ✅
```

2. **Se puede redeclarar** sin error, lo que provoca bugs:

```js
var x = 1;
var x = 2; // no da error (mal)
let y = 1;
let y = 2; // SyntaxError (bien)
```

### Nombres de variables

- Pueden tener letras, números, `_` y `$`, pero no empezar por número.
- Se usa **camelCase**: `precioTotal`, `nombreUsuario`.
- Constantes "de verdad" (valores fijos de configuración): `MAX_INTENTOS`.
- Distingue mayúsculas: `edad` y `Edad` son distintas.

> **Ideas clave**: `const` siempre que puedas, `let` si necesitas reasignar, `var` nunca.

## 6. Tipos de datos primitivos

JS tiene **7 tipos primitivos** y luego los **objetos**.

| Tipo | Ejemplo | Para qué |
|---|---|---|
| `string` | `"hola"`, `'hola'`, `` `hola` `` | Texto |
| `number` | `42`, `3.14`, `NaN`, `Infinity` | Números (enteros y decimales) |
| `bigint` **(ES2020)** | `9007199254740993n` | Enteros enormes |
| `boolean` | `true`, `false` | Sí / no |
| `undefined` | `undefined` | "No tiene valor asignado" |
| `null` | `null` | "Vacío a propósito" |
| `symbol` | `Symbol("id")` | Identificadores únicos |

### `typeof`: saber el tipo

```js
typeof "hola";     // "string"
typeof 42;         // "number"
typeof 10n;        // "bigint"
typeof true;       // "boolean"
typeof undefined;  // "undefined"
typeof Symbol();   // "symbol"
typeof null;       // "object"  ⚠️ bug histórico del lenguaje
typeof {};         // "object"
typeof [];         // "object"  (los arrays son objetos)
typeof function(){}; // "function"
```

Para comprobar arrays usa `Array.isArray([])` → `true`.

### Números: todo es "number"

JS no distingue enteros de decimales: todo es coma flotante de 64 bits.

```js
0.1 + 0.2;            // 0.30000000000000004 😅
Number.MAX_SAFE_INTEGER; // 9007199254740991
10 / 0;               // Infinity
"hola" * 2;           // NaN (Not a Number)
Number.isNaN(NaN);    // true
```

### BigInt para enteros enormes (ES2020)

```js
const grande = 9007199254740991n + 2n; // 9007199254740993n
// No se pueden mezclar con number:
10n + 5;   // ❌ TypeError
10n + 5n;  // ✅ 15n
```

### `undefined` vs `null`

```js
let a;              // undefined: nadie le ha dado valor
let b = null;       // null: yo digo explícitamente "no hay nada"
```

### Primitivos son inmutables y se copian por valor

```js
let x = 10;
let y = x;  // se copia el valor
y = 20;
console.log(x); // 10 (no cambia)
```

Los objetos, en cambio, se copian **por referencia** (lo veremos en el cap. 18).

> **Ideas clave**: 7 primitivos. `typeof null === "object"` es un bug famoso. Cuidado con los decimales.

## 7. Operadores

### Aritméticos

```js
10 + 3;   // 13
10 - 3;   // 7
10 * 3;   // 30
10 / 3;   // 3.3333333333333335
10 % 3;   // 1  (resto de la división)
2 ** 10;  // 1024 (potencia, ES2016)

let n = 5;
n++;      // 6
n += 10;  // 16
```

**Cuidado con `+` y strings**: si uno de los dos es texto, concatena.

```js
"5" + 3;  // "53"
"5" - 3;  // 2   (el - convierte a número)
```

### Comparación: usa SIEMPRE `===`

```js
5 == "5";    // true  😱 (convierte tipos)
5 === "5";   // false ✅ (compara valor y tipo)
0 == false;  // true  😱
0 === false; // false ✅
null == undefined;  // true
null === undefined; // false

5 !== "5";   // true
```

Regla: **`===` y `!==` siempre**. La única excepción aceptada es `x == null` para comprobar a la vez `null` y `undefined`.

### Lógicos

```js
true && false; // false (Y)
true || false; // true  (O)
!true;         // false (NO)
```

En JS, `&&` y `||` **devuelven uno de los operandos**, no necesariamente un booleano:

```js
"Ana" || "Anónimo";   // "Ana"
"" || "Anónimo";      // "Anónimo" (porque "" es falsy)
usuario && usuario.nombre; // si usuario existe, devuelve su nombre
```

### Ternario

```js
const edad = 20;
const mensaje = edad >= 18 ? "Mayor de edad" : "Menor de edad";
```

> **Ideas clave**: `===` siempre. `+` concatena si hay strings. `&&` y `||` devuelven valores.

## 8. Operadores modernos: `?.`, `??` y asignación lógica

### Encadenamiento opcional `?.` (ES2020)

Accede a propiedades que **pueden no existir** sin que explote el programa:

```js
const usuario = { nombre: "Ana", direccion: null };

// Antes:
const ciudad1 = usuario.direccion && usuario.direccion.ciudad;

// Ahora:
const ciudad2 = usuario.direccion?.ciudad;   // undefined (sin error)
usuario.direccion.ciudad;                    // ❌ TypeError

// Funciona con métodos y arrays:
usuario.saludar?.();     // si no existe el método, no hace nada
usuario.amigos?.[0];     // si no hay array, undefined
```

### Coalescencia nula `??` (ES2020)

Da un valor por defecto **solo** si el valor es `null` o `undefined`:

```js
const cantidad = 0;

cantidad || 10;  // 10  ❌ (0 es falsy, ¡pero era un valor válido!)
cantidad ?? 10;  // 0   ✅ (0 no es null ni undefined)

const config = { volumen: 0, tema: "" };
config.volumen ?? 50; // 0
config.tema ?? "claro"; // ""
config.idioma ?? "es";  // "es"
```

**Regla práctica**: para valores por defecto, `??` es casi siempre lo que quieres.

### Asignación lógica (ES2021)

```js
let a = null;
a ??= "valor por defecto";  // a = a ?? "valor..."  → solo asigna si es null/undefined

let b = "";
b ||= "relleno";   // asigna si b es falsy → "relleno"

let c = { activo: true };
c &&= { ...c, revisado: true }; // asigna solo si c es truthy

// Caso real: inicializar caché
const cache = {};
cache.usuarios ??= [];
cache.usuarios.push("Ana");
```

### Separadores numéricos (ES2021)

Guiones bajos para leer números largos. No cambian el valor:

```js
const millon = 1_000_000;
const precio = 1_299.99;
const bytes = 0xFF_FF_FF;
```

> **Ideas clave**: `?.` para acceder con seguridad. `??` para valores por defecto. `??=` para inicializar.

## 9. Strings (cadenas de texto)

### Tres formas de crear strings

```js
const a = 'comillas simples';
const b = "comillas dobles";
const c = `backticks (template literal)`;
```

### Template literals (ES2015)

Permiten **insertar variables** y **varias líneas**:

```js
const nombre = "Ana";
const edad = 30;

const frase = `Hola, me llamo ${nombre} y tengo ${edad} años.
El año que viene tendré ${edad + 1}.`;
```

Dentro de `${ }` puedes poner cualquier expresión: operaciones, llamadas a funciones, ternarios…

### Métodos útiles

```js
const texto = "  JavaScript es genial  ";

texto.length;               // 24
texto.trim();               // "JavaScript es genial"
texto.toUpperCase();        // "  JAVASCRIPT ES GENIAL  "
texto.includes("genial");   // true
texto.startsWith("  Java"); // true
texto.indexOf("es");        // 13
texto.slice(2, 12);         // "JavaScript"
texto.split(" ");           // ["", "", "JavaScript", "es", "genial", "", ""]
"ab".repeat(3);             // "ababab"
"5".padStart(3, "0");       // "005"  (ES2017)
"a-b-c".replaceAll("-", "/"); // "a/b/c" (ES2021)
```

### `at()` (ES2022): acceso con índices negativos

```js
const palabra = "Bilbao";
palabra[0];      // "B"
palabra.at(0);   // "B"
palabra.at(-1);  // "o" (último carácter)
palabra.at(-2);  // "a"
```

### Strings "bien formados" (ES2024)

Algunos caracteres (emojis, por ejemplo) ocupan dos "unidades" internas. Si cortas un string por la mitad de un emoji, queda roto:

```js
const roto = "😀".slice(0, 1);
roto.isWellFormed();  // false
roto.toWellFormed();  // "�" (lo repara con un carácter de sustitución)
```

Útil antes de enviar texto a APIs como `encodeURIComponent`, que fallan con strings rotos.

### Los strings son inmutables

```js
let s = "hola";
s[0] = "H";    // no hace nada
s = "H" + s.slice(1); // "Hola" → hay que crear uno nuevo
```

> **Ideas clave**: usa template literals. `at(-1)` para el último carácter. Los métodos devuelven strings nuevos.

## 10. Control de flujo

### `if / else`

```js
const nota = 7;

if (nota >= 9) {
  console.log("Sobresaliente");
} else if (nota >= 7) {
  console.log("Notable");
} else if (nota >= 5) {
  console.log("Aprobado");
} else {
  console.log("Suspenso");
}
```

### `switch`

Útil cuando comparas una variable con muchos valores concretos:

```js
const dia = "sábado";

switch (dia) {
  case "sábado":
  case "domingo":
    console.log("Fin de semana");
    break;          // ⚠️ sin break, sigue ejecutando el siguiente case
  case "lunes":
    console.log("Ánimo");
    break;
  default:
    console.log("Día laborable");
}
```

`switch` usa comparación estricta (`===`).

### Bucles

```js
// for clásico: cuando necesitas el índice
for (let i = 0; i < 5; i++) {
  console.log(i); // 0,1,2,3,4
}

// while: mientras se cumpla la condición
let intentos = 0;
while (intentos < 3) {
  intentos++;
}

// do...while: se ejecuta al menos una vez
do {
  console.log("Se ejecuta una vez");
} while (false);
```

### `for...of`: recorrer VALORES (arrays, strings, Map, Set…)

```js
const frutas = ["manzana", "pera", "kiwi"];
for (const fruta of frutas) {
  console.log(fruta);
}

for (const letra of "hola") {
  console.log(letra);
}

// Con índice:
for (const [i, fruta] of frutas.entries()) {
  console.log(i, fruta);
}
```

### `for...in`: recorrer CLAVES de un objeto

```js
const persona = { nombre: "Ana", edad: 30 };
for (const clave in persona) {
  console.log(clave, persona[clave]);
}
```

⚠️ **No uses `for...in` con arrays**: recorre claves como strings y puede incluir propiedades heredadas. Para objetos es más moderno `Object.entries` (cap. 18).

### `break` y `continue`

```js
for (let i = 0; i < 10; i++) {
  if (i === 3) continue; // salta esta vuelta
  if (i === 6) break;    // sale del bucle
  console.log(i);        // 0,1,2,4,5
}
```

> **Ideas clave**: `for...of` para arrays, `for...in` (o `Object.entries`) para objetos. No olvides `break` en `switch`.

## 11. (Ampliación) Strings, números y Math en la práctica

Este capítulo reúne utilidades que se usan a diario.

### Convertir texto a número

```js
Number("42");        // 42
Number("42abc");     // NaN
parseInt("42px");    // 42 (lee hasta donde puede)
parseFloat("3.5kg"); // 3.5
+"7";                // 7 (atajo con el + unario)
```

### Redondear y formatear

```js
Math.round(4.5);   // 5
Math.floor(4.9);   // 4
Math.ceil(4.1);    // 5
Math.trunc(-4.9);  // -4
(3.14159).toFixed(2); // "3.14" (devuelve string)

// Formateo según idioma (muy útil):
new Intl.NumberFormat("es-ES", { style: "currency", currency: "EUR" })
  .format(1234.5);   // "1234,50 €"
```

### Math

```js
Math.max(3, 8, 1);       // 8
Math.min(...[3, 8, 1]);  // 1
Math.abs(-5);            // 5
Math.sqrt(16);           // 4
Math.random();           // decimal entre 0 (incluido) y 1 (excluido)

// Entero aleatorio entre min y max (ambos incluidos):
const aleatorio = (min, max) => Math.floor(Math.random() * (max - min + 1)) + min;
aleatorio(1, 6); // como un dado
```

### Comprobaciones numéricas

```js
Number.isInteger(5);      // true
Number.isInteger(5.5);    // false
Number.isNaN("hola");     // false (la versión global isNaN("hola") da true: evítala)
Number.isFinite(1 / 0);   // false
```

> **Ideas clave**: `Number()` es estricto, `parseInt` es permisivo. `Intl.NumberFormat` para mostrar dinero.

## 12. Conversión de tipos, truthy y falsy

JS convierte tipos automáticamente (*coerción*). Entenderlo evita muchos bugs.

### Valores falsy (se comportan como `false`)

Solo hay **8**:

```js
false, 0, -0, 0n, "", null, undefined, NaN
```

**Todo lo demás es truthy**, incluso:

```js
"0"      // truthy (es un string no vacío)
"false"  // truthy
[]       // truthy (array vacío)
{}       // truthy (objeto vacío)
```

```js
if ([]) console.log("¡Un array vacío es truthy!");

// Para comprobar si un array está vacío:
if (lista.length === 0) { /* ... */ }
```

### Conversión explícita (la recomendable)

```js
String(123);     // "123"
Number("123");   // 123
Boolean("");     // false
Boolean("hola"); // true
!!"hola";        // true (doble negación: atajo para convertir a booleano)
```

### Coerciones sorprendentes (para reconocerlas, no para usarlas)

```js
[] + [];      // ""
[] + {};      // "[object Object]"
"3" * "4";    // 12
true + 1;     // 2
null + 1;     // 1
undefined + 1; // NaN
```

> **Ideas clave**: memoriza los 8 falsy. Convierte de forma explícita con `Number()`, `String()`, `Boolean()`.

## 🏋️ Ejercicios — Nivel 0–1 — Fundamentos y lenguaje básico

> 🟢 fácil · 🟡 medio · 🔴 difícil. Intenta cada ejercicio antes de abrir la solución.


### 1.1 🟢 Presentación (cap. 5, 9)
Declara las constantes `nombre`, `ciudad` y `añoNacimiento`, y muestra por consola con un template literal:
`Me llamo Ana, vivo en Bilbao y tengo 30 años.` (calcula la edad a partir del año actual con `new Date().getFullYear()`).

<details><summary>Solución</summary>

```js
const nombre = "Ana";
const ciudad = "Bilbao";
const añoNacimiento = 1996;
const edad = new Date().getFullYear() - añoNacimiento;

console.log(`Me llamo ${nombre}, vivo en ${ciudad} y tengo ${edad} años.`);
```
</details>

### 1.2 🟢 ¿Qué tipo es? (cap. 6, 12)
Sin ejecutarlo, escribe qué devuelve cada línea. Luego compruébalo.

```js
typeof null;
typeof [];
typeof NaN;
Boolean("0");
Boolean([]);
"5" + 3;
"5" - 3;
0 ?? 10;
0 || 10;
```

<details><summary>Solución</summary>

```js
typeof null;   // "object" (bug histórico)
typeof [];     // "object"
typeof NaN;    // "number"
Boolean("0");  // true (string no vacío)
Boolean([]);   // true (los objetos son truthy)
"5" + 3;       // "53"
"5" - 3;       // 2
0 ?? 10;       // 0
0 || 10;       // 10
```
</details>

### 1.3 🟢 Calificaciones (cap. 10)
Escribe una función `calificar(nota)` que devuelva `"Suspenso"` (<5), `"Aprobado"` (5–6.99), `"Notable"` (7–8.99) o `"Sobresaliente"` (9–10). Si la nota no es un número entre 0 y 10, devuelve `"Nota no válida"`.

<details><summary>Solución</summary>

```js
function calificar(nota) {
  if (typeof nota !== "number" || Number.isNaN(nota) || nota < 0 || nota > 10) {
    return "Nota no válida";
  }
  if (nota >= 9) return "Sobresaliente";
  if (nota >= 7) return "Notable";
  if (nota >= 5) return "Aprobado";
  return "Suspenso";
}

calificar(7.5); // "Notable"
calificar(11);  // "Nota no válida"
```
</details>

### 1.4 🟢 FizzBuzz (cap. 10)
Muestra los números del 1 al 30. Para múltiplos de 3 escribe `"Fizz"`, para múltiplos de 5 `"Buzz"` y para múltiplos de ambos `"FizzBuzz"`.

<details><summary>Solución</summary>

```js
for (let i = 1; i <= 30; i++) {
  let salida = "";
  if (i % 3 === 0) salida += "Fizz";
  if (i % 5 === 0) salida += "Buzz";
  console.log(salida || i);
}
```
</details>

### 1.5 🟡 Configuración segura (cap. 8)
Dado este objeto, obtén en una sola línea cada valor pedido usando `?.` y `??`:

```js
const config = {
  usuario: { nombre: "Ana", preferencias: { volumen: 0 } },
};
```

a) El volumen (si no existe, 50). b) El tema (si no existe, `"claro"`). c) La ciudad de `config.usuario.direccion` (si no existe, `"Desconocida"`).
d) ¿Por qué en (a) no sirve `||`?

<details><summary>Solución</summary>

```js
const volumen = config.usuario?.preferencias?.volumen ?? 50;         // 0
const tema = config.usuario?.preferencias?.tema ?? "claro";          // "claro"
const ciudad = config.usuario?.direccion?.ciudad ?? "Desconocida";   // "Desconocida"
```

d) Porque `0` es falsy: `0 || 50` daría 50, perdiendo el valor real. `??` solo sustituye `null` y `undefined`.
</details>

### 1.6 🟡 Palíndromo (cap. 9)
Escribe `esPalindromo(texto)` que ignore mayúsculas, espacios y signos de puntuación.
`esPalindromo("Anita lava la tina")` → `true`.

<details><summary>Solución</summary>

```js
function esPalindromo(texto) {
  const limpio = texto
    .toLowerCase()
    .normalize("NFD").replace(/\p{Diacritic}/gu, "") // quita acentos
    .replace(/[^a-z0-9ñ]/g, "");
  return limpio === [...limpio].reverse().join("");
}

esPalindromo("Anita lava la tina"); // true
esPalindromo("Hola");               // false
```
</details>


---

# NIVEL 2 — Funciones y estructuras de datos

## 13. Funciones

Una función es un bloque de código reutilizable con nombre. Recibe datos (**parámetros**) y puede devolver un resultado (**return**).

### Tres formas de crearlas

```js
// 1. Declaración de función
function sumar(a, b) {
  return a + b;
}

// 2. Expresión de función (se guarda en una variable)
const restar = function (a, b) {
  return a - b;
};

// 3. Arrow function (ES2015) — la más usada hoy
const multiplicar = (a, b) => a * b;
```

### Arrow functions en detalle

```js
// Con un solo parámetro, los paréntesis son opcionales
const doble = n => n * 2;

// Sin parámetros, paréntesis vacíos
const saludar = () => "¡Hola!";

// Con varias líneas, llaves y return explícito
const calcularIVA = (precio) => {
  const iva = precio * 0.21;
  return precio + iva;
};

// Para devolver un objeto directamente, envuélvelo en paréntesis
const crearUsuario = (nombre) => ({ nombre, activo: true });
```

Diferencia importante: las arrow functions **no tienen su propio `this`** (cap. 25). Por eso no se usan como métodos de objetos ni como constructores.

### Parámetros por defecto (ES2015)

```js
function saludar(nombre = "invitado", saludo = "Hola") {
  return `${saludo}, ${nombre}`;
}
saludar();            // "Hola, invitado"
saludar("Ana");       // "Hola, Ana"
saludar("Ana", "Hey"); // "Hey, Ana"
```

### Parámetros rest `...` (ES2015)

Recoge "el resto" de argumentos en un array:

```js
function sumarTodo(...numeros) {
  return numeros.reduce((total, n) => total + n, 0);
}
sumarTodo(1, 2, 3, 4); // 10
```

### Parámetros con desestructuración (muy usado)

```js
function crearBoton({ texto, color = "azul", tamaño = "mediano" }) {
  return `<button class="${color} ${tamaño}">${texto}</button>`;
}
crearBoton({ texto: "Enviar", color: "verde" });
```

Ventaja: el orden de los argumentos ya no importa y el código se lee solo.

### Funciones como valores

En JS, las funciones son valores: se pueden guardar en variables, pasar como argumento y devolver desde otra función.

```js
function ejecutarDosVeces(fn) {
  fn();
  fn();
}
ejecutarDosVeces(() => console.log("¡Hola!"));
```

A una función que recibe o devuelve funciones se le llama **función de orden superior**. `map`, `filter` o `setTimeout` lo son.

> **Ideas clave**: arrow functions para casi todo. Parámetros por defecto y desestructuración hacen el código más claro.

## 14. Ámbito (scope), hoisting y TDZ

### Scope: ¿dónde "vive" una variable?

```js
const global = "soy global";

function externa() {
  const deFuncion = "soy de la función";

  if (true) {
    const deBloque = "soy del bloque";
    console.log(global, deFuncion, deBloque); // ✅ ve las tres
  }

  console.log(deBloque); // ❌ ReferenceError
}
```

Regla: **el código de dentro ve lo de fuera, pero no al revés.** Esto se llama *scope léxico*: depende de dónde está escrito el código.

### Hoisting ("elevación")

JS "lee" las declaraciones antes de ejecutar el código.

```js
// Las declaraciones de función se pueden usar antes de escribirlas:
saludar(); // ✅ "Hola"
function saludar() { console.log("Hola"); }

// Las expresiones/arrow NO:
despedir(); // ❌ ReferenceError
const despedir = () => console.log("Adiós");
```

### Temporal Dead Zone (TDZ)

`let` y `const` también se elevan, pero no se pueden usar hasta su línea. Ese tramo es la **zona muerta temporal**:

```js
console.log(x); // ❌ ReferenceError: Cannot access 'x' before initialization
let x = 5;

console.log(y); // undefined (con var no da error, lo que es peor)
var y = 5;
```

La TDZ es buena: te avisa de un error en vez de darte un `undefined` silencioso.

> **Ideas clave**: el código interior ve el exterior. Declara siempre las variables antes de usarlas.

## 15. Closures (clausuras)

Un **closure** es una función que "recuerda" las variables del lugar donde se creó, aunque ese lugar ya haya terminado de ejecutarse.

```js
function crearContador() {
  let cuenta = 0; // variable "privada"

  return function () {
    cuenta++;
    return cuenta;
  };
}

const contador = crearContador();
contador(); // 1
contador(); // 2
contador(); // 3

const otro = crearContador();
otro(); // 1 (cada uno tiene su propia "cuenta")
```

`crearContador` ya terminó, pero la función devuelta **sigue teniendo acceso a `cuenta`**. Nadie más puede tocar esa variable: es privada.

### Usos reales

**1. Fábricas de funciones**:

```js
const multiplicarPor = (factor) => (n) => n * factor;

const doble = multiplicarPor(2);
const triple = multiplicarPor(3);
doble(5);  // 10
triple(5); // 15
```

**2. Datos privados**:

```js
function crearCuenta(saldoInicial) {
  let saldo = saldoInicial;
  return {
    ingresar: (cantidad) => (saldo += cantidad),
    retirar: (cantidad) => {
      if (cantidad > saldo) throw new Error("Saldo insuficiente");
      saldo -= cantidad;
      return saldo;
    },
    verSaldo: () => saldo,
  };
}

const cuenta = crearCuenta(100);
cuenta.ingresar(50);  // 150
cuenta.saldo;         // undefined (no se puede acceder directamente)
cuenta.verSaldo();    // 150
```

**3. Memoización** (guardar resultados ya calculados):

```js
function memoizar(fn) {
  const cache = new Map();
  return (n) => {
    if (cache.has(n)) return cache.get(n);
    const resultado = fn(n);
    cache.set(n, resultado);
    return resultado;
  };
}
```

> **Ideas clave**: una función recuerda el entorno donde nació. Sirve para estado privado y fábricas de funciones.

## 16. Arrays: los métodos esenciales

Un array es una lista ordenada de valores.

```js
const numeros = [5, 2, 8, 1, 9];
numeros.length;  // 5
numeros[0];      // 5
```

### Añadir y quitar (mutan el array original)

```js
const lista = ["a", "b"];
lista.push("c");     // al final → ["a","b","c"]
lista.pop();         // quita el último → ["a","b"]
lista.unshift("z");  // al principio → ["z","a","b"]
lista.shift();       // quita el primero → ["a","b"]
lista.splice(1, 1);  // desde índice 1, borra 1 → ["a"]
```

### Los 3 grandes: `map`, `filter`, `reduce`

No modifican el array original: **devuelven uno nuevo**.

```js
const productos = [
  { nombre: "Ratón", precio: 20, stock: 5 },
  { nombre: "Teclado", precio: 50, stock: 0 },
  { nombre: "Monitor", precio: 200, stock: 3 },
];

// map: transforma cada elemento → array del MISMO tamaño
const nombres = productos.map(p => p.nombre);
// ["Ratón", "Teclado", "Monitor"]

// filter: se queda con los que cumplen la condición
const disponibles = productos.filter(p => p.stock > 0);
// [Ratón, Monitor]

// reduce: reduce todo a UN valor
const valorTotal = productos.reduce((acumulado, p) => acumulado + p.precio * p.stock, 0);
// 20*5 + 50*0 + 200*3 = 700
```

Cómo funciona `reduce` paso a paso:

| Vuelta | acumulado | p | resultado |
|---|---|---|---|
| 1 | 0 (valor inicial) | Ratón | 100 |
| 2 | 100 | Teclado | 100 |
| 3 | 100 | Monitor | 700 |

**Encadenar** métodos es muy habitual:

```js
const totalDisponible = productos
  .filter(p => p.stock > 0)
  .map(p => p.precio)
  .reduce((a, b) => a + b, 0); // 220
```

### Buscar

```js
productos.find(p => p.precio > 30);       // {Teclado...} (el primero)
productos.findIndex(p => p.precio > 30);  // 1
[1, 2, 3].includes(2);                    // true
[1, 2, 3].indexOf(3);                     // 2
```

### Comprobar

```js
productos.some(p => p.stock === 0);  // true (¿alguno cumple?)
productos.every(p => p.precio > 10); // true (¿todos cumplen?)
```

### Recorrer

```js
productos.forEach((p, i) => console.log(i, p.nombre));
```

`forEach` no devuelve nada. Si quieres un resultado, usa `map`.

### Ordenar (⚠️ `sort` muta el array)

```js
const nums = [10, 1, 5, 100];
nums.sort();              // [1, 10, 100, 5] 😱 ordena como texto
nums.sort((a, b) => a - b); // [1, 5, 10, 100] ✅ numérico ascendente
nums.sort((a, b) => b - a); // descendente

// Strings con acentos correctamente:
["ñu", "nube", "árbol"].sort((a, b) => a.localeCompare(b, "es"));
```

### Otros útiles

```js
[1, 2, 3].join(" - ");      // "1 - 2 - 3"
[1, 2, 3, 4].slice(1, 3);   // [2, 3] (no muta)
[1, 2].concat([3, 4]);      // [1, 2, 3, 4]
Array.from("hola");         // ["h","o","l","a"]
Array.from({ length: 3 }, (_, i) => i * 10); // [0, 10, 20]
new Array(3).fill(0);       // [0, 0, 0]
```

> **Ideas clave**: `map` transforma, `filter` filtra, `reduce` acumula, `find` busca. `sort` necesita función comparadora para números.

## 17. Arrays modernos (ES2019 – ES2023)

### `flat` y `flatMap` (ES2019)

```js
[1, [2, 3], [4, [5]]].flat();         // [1, 2, 3, 4, [5]]
[1, [2, 3], [4, [5]]].flat(Infinity); // [1, 2, 3, 4, 5]

const frases = ["hola mundo", "adiós amigo"];
frases.flatMap(f => f.split(" ")); // ["hola", "mundo", "adiós", "amigo"]
```

### `at()` (ES2022)

```js
const arr = [10, 20, 30];
arr.at(-1);  // 30 (antes: arr[arr.length - 1])
```

### `findLast` y `findLastIndex` (ES2023)

Buscan empezando por el final:

```js
const temperaturas = [12, 25, 18, 30, 15];
temperaturas.findLast(t => t > 20);      // 30
temperaturas.findLastIndex(t => t > 20); // 3
```

### Métodos que NO mutan (ES2023) ⭐ muy importantes

Antes, `sort`, `reverse` y `splice` modificaban el array original, lo que daba muchos bugs (sobre todo en React o Angular). Ahora hay versiones que **devuelven una copia**:

| Muta (antiguo) | Copia (ES2023) |
|---|---|
| `sort()` | `toSorted()` |
| `reverse()` | `toReversed()` |
| `splice()` | `toSpliced()` |
| `arr[i] = x` | `with(i, x)` |

```js
const original = [3, 1, 2];

const ordenado = original.toSorted();  // [1, 2, 3]
const invertido = original.toReversed(); // [2, 1, 3]
const sinPrimero = original.toSpliced(0, 1); // [1, 2]
const cambiado = original.with(0, 99); // [99, 1, 2]

console.log(original); // [3, 1, 2] ✅ intacto
```

> **Ideas clave**: prefiere `toSorted`, `toReversed`, `toSpliced` y `with` para no modificar datos por accidente.

## 18. Objetos

Un objeto es una colección de pares **clave: valor**.

```js
const libro = {
  titulo: "El Quijote",
  autor: "Cervantes",
  año: 1605,
  "fecha-edicion": "2020", // claves con guiones, entre comillas
  leer() {                  // método (forma corta)
    return `Leyendo ${this.titulo}`;
  },
};

libro.titulo;            // acceso con punto
libro["fecha-edicion"];  // acceso con corchetes
libro.leer();
```

### Atajos modernos

```js
const nombre = "Ana";
const edad = 30;

// Shorthand: si la variable se llama igual que la clave
const persona = { nombre, edad }; // { nombre: "Ana", edad: 30 }

// Propiedades computadas
const campo = "email";
const datos = { [campo]: "ana@mail.com" }; // { email: "ana@mail.com" }
```

### Añadir, modificar, borrar

```js
persona.ciudad = "Bilbao";  // añadir
persona.edad = 31;          // modificar
delete persona.ciudad;      // borrar
"edad" in persona;          // true
```

### `Object.hasOwn` (ES2022)

La forma moderna de comprobar si un objeto tiene una propiedad **propia** (no heredada):

```js
Object.hasOwn(persona, "edad"); // true
// Antes: persona.hasOwnProperty("edad")
```

### Recorrer objetos

```js
const notas = { mates: 8, lengua: 6, ingles: 9 };

Object.keys(notas);    // ["mates", "lengua", "ingles"]
Object.values(notas);  // [8, 6, 9]
Object.entries(notas); // [["mates", 8], ["lengua", 6], ["ingles", 9]]

for (const [asignatura, nota] of Object.entries(notas)) {
  console.log(`${asignatura}: ${nota}`);
}

// Y al revés: de entradas a objeto (ES2019)
const aprobadas = Object.fromEntries(
  Object.entries(notas).filter(([, nota]) => nota >= 7)
); // { mates: 8, ingles: 9 }
```

### Agrupar: `Object.groupBy` y `Map.groupBy` (ES2024)

Antes había que hacerlo con `reduce`. Ahora es una línea:

```js
const alumnos = [
  { nombre: "Ana", curso: "1º" },
  { nombre: "Luis", curso: "2º" },
  { nombre: "Eva", curso: "1º" },
];

const porCurso = Object.groupBy(alumnos, a => a.curso);
// {
//   "1º": [{Ana}, {Eva}],
//   "2º": [{Luis}]
// }

const porNota = Object.groupBy([3, 7, 9, 4], n => (n >= 5 ? "aprobado" : "suspenso"));
// { suspenso: [3, 4], aprobado: [7, 9] }
```

`Map.groupBy` hace lo mismo pero devuelve un `Map` (útil si las claves son objetos).

### Copia por referencia ⚠️

```js
const a = { valor: 1 };
const b = a;      // b apunta al MISMO objeto
b.valor = 99;
console.log(a.valor); // 99 😱

// Copia superficial (un nivel):
const c = { ...a };

// Copia profunda (todos los niveles):
const d = structuredClone(a);
```

### Congelar objetos

```js
const CONFIG = Object.freeze({ api: "https://api.ejemplo.com" });
CONFIG.api = "otra"; // se ignora (en modo estricto: error)
```

> **Ideas clave**: `Object.entries` + `for...of` para recorrer. `Object.groupBy` para agrupar. `structuredClone` para copias profundas.

## 19. Desestructuración y spread

### Desestructurar arrays

```js
const colores = ["rojo", "verde", "azul"];
const [primero, segundo] = colores;   // "rojo", "verde"
const [, , tercero] = colores;        // saltar elementos → "azul"
const [cabeza, ...resto] = colores;   // "rojo", ["verde", "azul"]

// Intercambiar variables sin auxiliar
let x = 1, y = 2;
[x, y] = [y, x];
```

### Desestructurar objetos

```js
const usuario = {
  id: 7,
  nombre: "Ana",
  direccion: { ciudad: "Bilbao", cp: "48001" },
};

const { nombre, id } = usuario;
const { nombre: nombreUsuario } = usuario;    // renombrar
const { rol = "alumno" } = usuario;           // valor por defecto
const { direccion: { ciudad } } = usuario;    // anidada
const { id: _, ...sinId } = usuario;          // el resto
```

### Spread `...`: "desparramar"

```js
// Arrays
const a = [1, 2];
const b = [3, 4];
const todos = [...a, ...b, 5];       // [1, 2, 3, 4, 5]
const copia = [...a];
Math.max(...todos);                  // 5

// Objetos
const base = { tema: "claro", idioma: "es" };
const preferencias = { ...base, tema: "oscuro" }; // sobrescribe tema
// { tema: "oscuro", idioma: "es" }
```

El orden importa: lo que va después sobrescribe lo de antes.

### Patrón típico: actualizar sin mutar

```js
const estado = { usuario: "Ana", carrito: ["pan"] };

const nuevoEstado = {
  ...estado,
  carrito: [...estado.carrito, "leche"],
};
```

Este patrón es la base de React, Redux y Angular con signals.

> **Ideas clave**: desestructura para extraer, spread para combinar y copiar.

## 20. Map, Set, WeakMap, WeakSet y WeakRef

### `Map`: diccionario con claves de cualquier tipo

```js
const edades = new Map();
edades.set("Ana", 30);
edades.set("Luis", 25);

edades.get("Ana");     // 30
edades.has("Luis");    // true
edades.size;           // 2
edades.delete("Luis");

// Se puede crear con datos
const m = new Map([["a", 1], ["b", 2]]);

for (const [clave, valor] of m) {
  console.log(clave, valor);
}
```

**¿Map u objeto?**

| | Objeto `{}` | `Map` |
|---|---|---|
| Claves | Solo strings y symbols | Cualquier tipo (objetos, números…) |
| Orden | Casi siempre de inserción | Siempre de inserción |
| Tamaño | `Object.keys(o).length` | `map.size` |
| Rendimiento con muchas altas/bajas | Peor | Mejor |
| Convertir a JSON | Directo | Hay que convertir |

### `Set`: colección sin duplicados

```js
const etiquetas = new Set(["js", "css", "js", "html"]);
etiquetas.size;          // 3
etiquetas.add("node");
etiquetas.has("css");    // true

// Truco clásico: quitar duplicados de un array
const unicos = [...new Set([1, 2, 2, 3, 3, 3])]; // [1, 2, 3]
```

### Versiones "débiles": `WeakMap` y `WeakSet`

Solo aceptan **objetos como claves** y no impiden que el recolector de basura los borre. Útiles para asociar datos a objetos sin causar fugas de memoria:

```js
const metadatos = new WeakMap();

function procesar(elementoDOM) {
  metadatos.set(elementoDOM, { clicks: 0 });
}
// Si el elemento se borra de la página, su entrada desaparece sola.
```

No se pueden recorrer ni tienen `size`.

### `WeakRef` (ES2021)

Una referencia que no impide la recolección de basura. Uso avanzado y poco frecuente (cachés):

```js
const ref = new WeakRef(objetoGrande);
const obj = ref.deref(); // el objeto, o undefined si ya se borró
```

> **Ideas clave**: `Map` para diccionarios dinámicos, `Set` para valores únicos, `WeakMap` para asociar datos a objetos.

## 21. Métodos de conjuntos (ES2025)

Por fin `Set` tiene operaciones matemáticas de conjuntos:

```js
const frontend = new Set(["Ana", "Luis", "Eva"]);
const backend  = new Set(["Luis", "Marta", "Eva"]);

frontend.union(backend);
// Set {"Ana", "Luis", "Eva", "Marta"}  → están en alguno

frontend.intersection(backend);
// Set {"Luis", "Eva"}  → están en los dos

frontend.difference(backend);
// Set {"Ana"}  → solo en frontend

frontend.symmetricDifference(backend);
// Set {"Ana", "Marta"}  → en uno pero no en los dos

new Set(["Luis"]).isSubsetOf(frontend);   // true  (¿todos sus elementos están en frontend?)
frontend.isSupersetOf(new Set(["Eva"]));  // true
frontend.isDisjointFrom(new Set(["Zoe"])); // true (no comparten nada)
```

Ejemplo práctico: alumnos que han entregado la tarea.

```js
const matriculados = new Set(["Ana", "Luis", "Eva", "Iker"]);
const entregados = new Set(["Ana", "Eva"]);

const pendientes = matriculados.difference(entregados);
console.log([...pendientes]); // ["Luis", "Iker"]
```

> **Ideas clave**: `union`, `intersection`, `difference` y compañía sustituyen a los trucos con `filter`.

## 22. ⭐ `getOrInsert` y `getOrInsertComputed` en Map (ES2026)

Problema clásico: "si la clave existe, dame su valor; si no, créala con un valor inicial".

```js
// Antes:
const grupos = new Map();
for (const alumno of alumnos) {
  if (!grupos.has(alumno.curso)) {
    grupos.set(alumno.curso, []);
  }
  grupos.get(alumno.curso).push(alumno.nombre);
}
```

Con ES2026:

```js
const grupos = new Map();
for (const alumno of alumnos) {
  grupos.getOrInsert(alumno.curso, []).push(alumno.nombre);
}
```

- `getOrInsert(clave, valor)`: si no existe, inserta `valor` y lo devuelve.
- `getOrInsertComputed(clave, fn)`: igual, pero el valor se **calcula** solo si hace falta. Útil cuando crear el valor es costoso.

```js
const contador = new Map();
for (const palabra of "a b a c a b".split(" ")) {
  contador.set(palabra, contador.getOrInsert(palabra, 0) + 1);
}
// Map { "a" => 3, "b" => 2, "c" => 1 }

const cache = new Map();
const datos = cache.getOrInsertComputed("informe", (clave) => {
  console.log("Calculando", clave); // solo la primera vez
  return calcularInformeCaro();
});
```

También existe en `WeakMap`.

> 💡 **Compatibilidad**: es muy reciente. Comprueba en MDN/caniuse si tu navegador o versión de Node lo soporta. Si no, usa el patrón "antes".

> **Ideas clave**: `getOrInsert` elimina el `if (!map.has(...)) map.set(...)`.

## 23. JSON y ⭐ acceso al texto fuente en `JSON.parse` (ES2026)

**JSON** (JavaScript Object Notation) es el formato estándar para intercambiar datos entre aplicaciones.

```js
const alumno = { nombre: "Ana", notas: [8, 9], activo: true };

// De objeto a texto JSON
const texto = JSON.stringify(alumno);
// '{"nombre":"Ana","notas":[8,9],"activo":true}'

// Bonito, con sangría de 2 espacios
JSON.stringify(alumno, null, 2);

// De texto JSON a objeto
const copia = JSON.parse(texto);
```

Reglas de JSON: claves siempre entre comillas dobles, no admite funciones, `undefined`, comentarios ni comas finales.

### El "reviver": transformar al parsear

```js
const json = '{"fecha":"2026-11-19T10:00:00Z"}';
const obj = JSON.parse(json, (clave, valor) =>
  clave === "fecha" ? new Date(valor) : valor
);
```

### ⭐ El problema de los números grandes (ES2026)

```js
JSON.parse('{"id": 12345678901234567890}').id;
// 12345678901234567000  😱 se pierde precisión (más allá de MAX_SAFE_INTEGER)
```

En ES2026, el *reviver* recibe un tercer parámetro, `context`, con el **texto original** (`context.source`):

```js
const datos = JSON.parse(
  '{"id": 12345678901234567890, "precio": 9.99}',
  (clave, valor, context) => {
    if (clave === "id") return BigInt(context.source); // texto exacto → BigInt
    return valor;
  }
);
datos.id; // 12345678901234567890n ✅
```

Y para el camino contrario, `JSON.rawJSON` permite escribir números exactos al serializar:

```js
JSON.stringify({ id: JSON.rawJSON("12345678901234567890") });
// '{"id":12345678901234567890}'
```

> **Ideas clave**: `stringify` y `parse`. En ES2026, `context.source` permite leer números grandes sin perder precisión.

## 24. ⭐ `Math.sumPrecise` (ES2026) y la coma flotante

Ya vimos que `0.1 + 0.2 !== 0.3`. Al sumar muchos números, los errores se **acumulan**:

```js
const valores = [1e20, 0.1, -1e20];
valores.reduce((a, b) => a + b, 0); // 0  😱 (debería ser 0.1)

Math.sumPrecise(valores);           // 0.1 ✅
```

`Math.sumPrecise` recibe un **iterable** de números y hace la suma con el máximo de precisión posible:

```js
Math.sumPrecise([0.1, 0.2, 0.3]);        // 0.6
Math.sumPrecise(new Set([1, 2, 3]));     // 6
Math.sumPrecise([]);                     // -0
```

### ¿Y para dinero?

`sumPrecise` mejora la suma, pero **no** elimina los problemas de coma flotante en general. Para dinero, la recomendación sigue siendo trabajar en **céntimos (enteros)**:

```js
const precios = [19.99, 5.01];
const totalCentimos = precios
  .map(p => Math.round(p * 100))
  .reduce((a, b) => a + b, 0); // 2500
const total = totalCentimos / 100; // 25
```

> **Ideas clave**: usa `Math.sumPrecise` para sumar muchos decimales. Para dinero, trabaja en céntimos.

## 🏋️ Ejercicios — Nivel 2 — Funciones y estructuras de datos

> 🟢 fácil · 🟡 medio · 🔴 difícil. Intenta cada ejercicio antes de abrir la solución.


### 2.1 🟢 Arrow functions (cap. 13)
Convierte a arrow functions lo más cortas posible:

```js
function cuadrado(n) { return n * n; }
function saludo() { return "Hola"; }
function crearPunto(x, y) { return { x: x, y: y }; }
```

<details><summary>Solución</summary>

```js
const cuadrado = n => n * n;
const saludo = () => "Hola";
const crearPunto = (x, y) => ({ x, y });
```
</details>

### 2.2 🟡 Contador con closure (cap. 15)
Crea `crearContador(inicio = 0, paso = 1)` que devuelva un objeto con los métodos `incrementar()`, `decrementar()`, `reiniciar()` y `valor()`. El valor no debe ser accesible desde fuera.

<details><summary>Solución</summary>

```js
function crearContador(inicio = 0, paso = 1) {
  let actual = inicio;
  return {
    incrementar: () => (actual += paso),
    decrementar: () => (actual -= paso),
    reiniciar: () => (actual = inicio),
    valor: () => actual,
  };
}

const c = crearContador(10, 5);
c.incrementar(); // 15
c.incrementar(); // 20
c.reiniciar();   // 10
c.actual;        // undefined
```
</details>

### 2.3 🟡 Tienda (cap. 16, 17)
Con este array:

```js
const productos = [
  { nombre: "Ratón", precio: 20, categoria: "periféricos", stock: 5 },
  { nombre: "Teclado", precio: 50, categoria: "periféricos", stock: 0 },
  { nombre: "Monitor", precio: 200, categoria: "pantallas", stock: 3 },
  { nombre: "Portátil", precio: 900, categoria: "ordenadores", stock: 2 },
  { nombre: "Webcam", precio: 60, categoria: "periféricos", stock: 8 },
];
```

a) Array con los nombres en mayúsculas.
b) Productos con stock, ordenados por precio de mayor a menor **sin modificar** el original.
c) Valor total del inventario (precio × stock).
d) ¿Hay algún producto de más de 500 €? ¿Todos cuestan más de 10 €?
e) El último producto de la categoría "periféricos".

<details><summary>Solución</summary>

```js
// a
const nombres = productos.map(p => p.nombre.toUpperCase());

// b
const conStock = productos
  .filter(p => p.stock > 0)
  .toSorted((a, b) => b.precio - a.precio);

// c
const valorTotal = productos.reduce((total, p) => total + p.precio * p.stock, 0);
// 20*5 + 0 + 200*3 + 900*2 + 60*8 = 2980

// d
const hayCaro = productos.some(p => p.precio > 500);   // true
const todosMas10 = productos.every(p => p.precio > 10); // true

// e
const ultimoPeriferico = productos.findLast(p => p.categoria === "periféricos"); // Webcam
```
</details>

### 2.4 🟡 Agrupar alumnos (cap. 18)
Agrupa estos alumnos por curso con `Object.groupBy` y después crea un objeto con la **nota media** de cada curso usando `Object.entries` y `Object.fromEntries`.

```js
const alumnos = [
  { nombre: "Ana", curso: "1º", nota: 8 },
  { nombre: "Luis", curso: "2º", nota: 5 },
  { nombre: "Eva", curso: "1º", nota: 9 },
  { nombre: "Iker", curso: "2º", nota: 7 },
  { nombre: "June", curso: "1º", nota: 6 },
];
```

<details><summary>Solución</summary>

```js
const porCurso = Object.groupBy(alumnos, a => a.curso);

const medias = Object.fromEntries(
  Object.entries(porCurso).map(([curso, lista]) => [
    curso,
    lista.reduce((suma, a) => suma + a.nota, 0) / lista.length,
  ])
);
// { "1º": 7.666..., "2º": 6 }
```
</details>

### 2.5 🟢 Desestructuración (cap. 19)
Del siguiente objeto, extrae en **una sola línea**: el nombre renombrado como `alias`, la ciudad (anidada), el teléfono con valor por defecto `"sin teléfono"` y el resto de propiedades en `otros`.

```js
const perfil = { nombre: "Ana", edad: 30, direccion: { ciudad: "Bilbao" }, email: "ana@mail.com" };
```

<details><summary>Solución</summary>

```js
const { nombre: alias, direccion: { ciudad }, telefono = "sin teléfono", ...otros } = perfil;
// alias = "Ana", ciudad = "Bilbao", telefono = "sin teléfono"
// otros = { edad: 30, email: "ana@mail.com" }
// (direccion no aparece en otros porque se ha desestructurado)
```
</details>

### 2.6 🟡 Actualización inmutable (cap. 19)
Escribe `añadirAlCarrito(estado, producto)` que devuelva un **nuevo** estado sin modificar el original. Si el producto ya está (mismo `id`), aumenta su `cantidad`; si no, añádelo con `cantidad: 1`.

```js
const estado = { usuario: "Ana", carrito: [{ id: 1, nombre: "Pan", cantidad: 1 }] };
```

<details><summary>Solución</summary>

```js
function añadirAlCarrito(estado, producto) {
  const existe = estado.carrito.some(p => p.id === producto.id);
  const carrito = existe
    ? estado.carrito.map(p => (p.id === producto.id ? { ...p, cantidad: p.cantidad + 1 } : p))
    : [...estado.carrito, { ...producto, cantidad: 1 }];
  return { ...estado, carrito };
}

const nuevo = añadirAlCarrito(estado, { id: 1, nombre: "Pan" });
nuevo.carrito[0].cantidad;  // 2
estado.carrito[0].cantidad; // 1 (intacto)
```
</details>

### 2.7 🟡 Conjuntos (cap. 20, 21)
Dos grupos de alumnos se han apuntado a talleres:

```js
const robotica = new Set(["Ana", "Luis", "Eva", "Iker"]);
const impresion3D = new Set(["Eva", "June", "Luis", "Mikel"]);
```

a) ¿Quiénes están en los dos? b) ¿Quiénes están en alguno? c) ¿Quiénes solo en robótica? d) ¿Quiénes en uno solo?
e) Resuélvelo también **sin** los métodos de ES2025 (con spread y `filter`).

<details><summary>Solución</summary>

```js
// ES2025
robotica.intersection(impresion3D);        // Eva, Luis
robotica.union(impresion3D);               // Ana, Luis, Eva, Iker, June, Mikel
robotica.difference(impresion3D);          // Ana, Iker
robotica.symmetricDifference(impresion3D); // Ana, Iker, June, Mikel

// Sin ES2025
const ambos = [...robotica].filter(n => impresion3D.has(n));
const alguno = new Set([...robotica, ...impresion3D]);
const soloRobotica = [...robotica].filter(n => !impresion3D.has(n));
```
</details>

### 2.8 🟡 Contar palabras con Map (cap. 20, 22)
Escribe `contarPalabras(texto)` que devuelva un `Map` con cuántas veces aparece cada palabra (en minúsculas, sin signos de puntuación). Hazlo primero con `has`/`set` y luego con `getOrInsert` (ES2026).

<details><summary>Solución</summary>

```js
function contarPalabras(texto) {
  const palabras = texto.toLowerCase().match(/\p{L}+/gu) ?? [];
  const cuenta = new Map();
  for (const p of palabras) {
    cuenta.set(p, (cuenta.get(p) ?? 0) + 1);
  }
  return cuenta;
}

// Con ES2026
function contarPalabras2026(texto) {
  const cuenta = new Map();
  for (const p of texto.toLowerCase().match(/\p{L}+/gu) ?? []) {
    cuenta.set(p, cuenta.getOrInsert(p, 0) + 1);
  }
  return cuenta;
}

contarPalabras("El gato y el perro. ¡El gato!");
// Map { "el" => 3, "gato" => 2, "y" => 1, "perro" => 1 }
```
</details>

### 2.9 🔴 Memoización (cap. 15, 20)
Escribe `memoizar(fn)` que funcione con funciones de **cualquier número de argumentos** (pista: usa `JSON.stringify(args)` como clave). Pruébalo con una función de Fibonacci recursiva y mide la diferencia con `console.time`.

<details><summary>Solución</summary>

```js
function memoizar(fn) {
  const cache = new Map();
  return function (...args) {
    const clave = JSON.stringify(args);
    if (!cache.has(clave)) cache.set(clave, fn.apply(this, args));
    return cache.get(clave);
  };
}

const fibLento = n => (n < 2 ? n : fibLento(n - 1) + fibLento(n - 2));

const fibRapido = memoizar(n => (n < 2 ? n : fibRapido(n - 1) + fibRapido(n - 2)));

console.time("lento");  fibLento(32);  console.timeEnd("lento");   // cientos de ms
console.time("rápido"); fibRapido(32); console.timeEnd("rápido");  // < 1 ms
```

Fíjate en que `fibRapido` se llama a sí misma **a través de la versión memoizada**: así cada subproblema se calcula una sola vez.
</details>

### 2.10 🟡 Suma precisa y JSON (cap. 23, 24)
a) Explica por qué `[0.1, 0.2, 0.3].reduce((a, b) => a + b)` no da exactamente `0.6`, y calcula el resultado correcto con `Math.sumPrecise`.
b) Este JSON viene de una API: `'{"pedido": 98765432109876543210, "total": 15.5}'`. Léelo de forma que `pedido` no pierda precisión.

<details><summary>Solución</summary>

a) Los números decimales se guardan en binario y la mayoría no tiene representación exacta; los pequeños errores se acumulan al sumar.

```js
[0.1, 0.2, 0.3].reduce((a, b) => a + b); // 0.6000000000000001
Math.sumPrecise([0.1, 0.2, 0.3]);        // 0.6
```

b)

```js
const datos = JSON.parse(
  '{"pedido": 98765432109876543210, "total": 15.5}',
  (clave, valor, contexto) => (clave === "pedido" ? BigInt(contexto.source) : valor)
);
datos.pedido; // 98765432109876543210n
```
</details>


---

# NIVEL 3 — Programación orientada a objetos

## 25. `this`: qué es y cómo se decide

`this` es una referencia al **objeto que está ejecutando el código**. Su valor **depende de cómo se llama la función**, no de dónde se escribe. Es uno de los conceptos que más lía en JS.

### Las 4 reglas (de más a menos prioridad)

**1. Con `new`**: `this` es el objeto nuevo.

```js
function Persona(nombre) {
  this.nombre = nombre;
}
const p = new Persona("Ana"); // this → p
```

**2. Con `call`, `apply` o `bind`**: `this` es lo que tú digas.

```js
function presentar(saludo) {
  return `${saludo}, soy ${this.nombre}`;
}
const ana = { nombre: "Ana" };

presentar.call(ana, "Hola");      // argumentos sueltos
presentar.apply(ana, ["Hola"]);   // argumentos en array
const presentarAna = presentar.bind(ana); // crea una función nueva "atada"
presentarAna("Buenas");
```

**3. Como método (`objeto.metodo()`)**: `this` es el objeto antes del punto.

```js
const coche = {
  marca: "Seat",
  describir() {
    return `Soy un ${this.marca}`;
  },
};
coche.describir(); // "Soy un Seat"
```

**4. Llamada suelta**: `this` es `undefined` (en modo estricto y módulos).

```js
const describir = coche.describir;
describir(); // ❌ TypeError: Cannot read properties of undefined
```

### El problema clásico y la solución con arrow functions

Las arrow functions **no tienen `this` propio**: usan el `this` del lugar donde se escribieron.

```js
const temporizador = {
  segundos: 0,
  iniciar() {
    // ❌ function normal: this se pierde dentro de setInterval
    // setInterval(function () { this.segundos++; }, 1000);

    // ✅ arrow function: hereda el this de iniciar()
    setInterval(() => {
      this.segundos++;
    }, 1000);
  },
};
```

**Regla práctica**:
- Métodos de objetos y clases → sintaxis de método normal.
- Callbacks dentro de métodos → arrow functions.

> **Ideas clave**: `this` depende de cómo se llama la función. Las arrow functions heredan el `this` exterior.

## 26. Prototipos y la cadena de prototipos

JS no tiene "clases" de verdad por dentro: usa **prototipos**. Cada objeto tiene un enlace oculto a otro objeto (su *prototipo*). Si buscas una propiedad y no está en el objeto, JS la busca en su prototipo, y luego en el prototipo del prototipo… Esa es la **cadena de prototipos**.

```js
const animal = {
  respirar() {
    return "Respirando...";
  },
};

const perro = Object.create(animal); // el prototipo de perro es animal
perro.ladrar = () => "¡Guau!";

perro.ladrar();    // "¡Guau!" (propio)
perro.respirar();  // "Respirando..." (heredado de animal)

Object.getPrototypeOf(perro) === animal; // true
```

### Por eso los arrays tienen `map`

```js
const arr = [1, 2, 3];
// arr no tiene "map" propio; lo hereda de Array.prototype
Object.getPrototypeOf(arr) === Array.prototype; // true
// Y Array.prototype hereda de Object.prototype
```

Cadena: `arr` → `Array.prototype` → `Object.prototype` → `null`.

⚠️ **Nunca modifiques prototipos nativos** (`Array.prototype.miMetodo = ...`). Puede romper librerías y futuras versiones del lenguaje.

> **Ideas clave**: la herencia en JS se basa en prototipos. Las clases (siguiente capítulo) son una sintaxis más cómoda encima de esto.

## 27. Clases (ES2015)

Las clases son una forma clara de crear objetos con la misma estructura y comportamiento.

```js
class Alumno {
  constructor(nombre, curso) {
    this.nombre = nombre;
    this.curso = curso;
    this.notas = [];
  }

  añadirNota(nota) {
    this.notas.push(nota);
    return this; // permite encadenar
  }

  media() {
    if (this.notas.length === 0) return 0;
    return this.notas.reduce((a, b) => a + b) / this.notas.length;
  }

  toString() {
    return `${this.nombre} (${this.curso}) — media ${this.media().toFixed(2)}`;
  }
}

const ana = new Alumno("Ana", "1º Bach");
ana.añadirNota(8).añadirNota(9);
console.log(`${ana}`); // "Ana (1º Bach) — media 8.50"
```

### Herencia con `extends` y `super`

```js
class Persona {
  constructor(nombre) {
    this.nombre = nombre;
  }
  presentarse() {
    return `Hola, soy ${this.nombre}`;
  }
}

class Profesor extends Persona {
  constructor(nombre, asignatura) {
    super(nombre);                // llama al constructor de Persona (obligatorio antes de usar this)
    this.asignatura = asignatura;
  }

  presentarse() {
    // super.metodo() llama a la versión del padre
    return `${super.presentarse()} y enseño ${this.asignatura}`;
  }
}

const profe = new Profesor("Alberto", "TIC");
profe.presentarse(); // "Hola, soy Alberto y enseño TIC"
profe instanceof Profesor; // true
profe instanceof Persona;  // true
```

### Las clases no se elevan (hoisting)

```js
new Coche(); // ❌ ReferenceError
class Coche {}
```

> **Ideas clave**: `constructor` inicializa, `extends` hereda, `super` llama al padre.

## 28. Campos públicos, privados `#` y estáticos (ES2022)

### Campos de clase

Puedes declarar propiedades directamente en el cuerpo de la clase:

```js
class Contador {
  valor = 0;          // campo público con valor inicial
  #pasos = 0;         // campo PRIVADO (con #)

  incrementar() {
    this.valor++;
    this.#pasos++;
  }

  get pasos() {       // getter para leer el privado
    return this.#pasos;
  }

  #registrar() {      // método privado
    console.log("Paso", this.#pasos);
  }
}

const c = new Contador();
c.incrementar();
c.valor;     // 1
c.pasos;     // 1
c.#pasos;    // ❌ SyntaxError: privado de verdad
```

A diferencia del `_nombre` (convención), `#nombre` es **realmente privado**: es imposible acceder desde fuera.

### Miembros estáticos

Pertenecen a la **clase**, no a las instancias:

```js
class Matematicas {
  static PI = 3.14159;

  static areaCirculo(r) {
    return Matematicas.PI * r ** 2;
  }
}

Matematicas.areaCirculo(2); // 12.56636
new Matematicas().areaCirculo; // undefined
```

Uso típico: métodos de fábrica.

```js
class Usuario {
  #id;
  static #siguienteId = 1;

  constructor(nombre) {
    this.nombre = nombre;
    this.#id = Usuario.#siguienteId++;
  }

  static desdeJSON(json) {
    const datos = JSON.parse(json);
    return new Usuario(datos.nombre);
  }

  get id() { return this.#id; }
}

const u = Usuario.desdeJSON('{"nombre":"Ana"}');
```

> **Ideas clave**: `#` para privacidad real. `static` para cosas de la clase, no de cada objeto.

## 29. Bloques `static {}` y `#x in obj` (ES2022)

### Bloques de inicialización estática

Código que se ejecuta **una vez** cuando se define la clase. Útil para inicializaciones complejas:

```js
class Configuracion {
  static valores;

  static {
    // Se ejecuta al cargar la clase
    const entorno = globalThis.process?.env?.NODE_ENV ?? "desarrollo";
    Configuracion.valores = {
      entorno,
      debug: entorno !== "produccion",
    };
  }
}

Configuracion.valores; // { entorno: "desarrollo", debug: true }
```

### Comprobar campos privados con `#x in obj`

Permite saber si un objeto es una instancia "auténtica" de tu clase:

```js
class Punto {
  #x;
  #y;
  constructor(x, y) { this.#x = x; this.#y = y; }

  static esPunto(obj) {
    return #x in obj;
  }

  equals(otro) {
    if (!(#x in otro)) return false;
    return this.#x === otro.#x && this.#y === otro.#y;
  }
}

Punto.esPunto(new Punto(1, 2)); // true
Punto.esPunto({ x: 1, y: 2 });  // false
```

> **Ideas clave**: `static {}` inicializa la clase. `#campo in obj` comprueba instancias de forma segura.

## 30. Getters y setters

Permiten que una propiedad ejecute código al leerla o escribirla.

```js
class Temperatura {
  #celsius = 0;

  get celsius() {
    return this.#celsius;
  }

  set celsius(valor) {
    if (typeof valor !== "number") throw new TypeError("Debe ser un número");
    if (valor < -273.15) throw new RangeError("Por debajo del cero absoluto");
    this.#celsius = valor;
  }

  get fahrenheit() {        // propiedad calculada (solo lectura)
    return this.#celsius * 9 / 5 + 32;
  }

  set fahrenheit(f) {
    this.celsius = (f - 32) * 5 / 9; // reutiliza la validación
  }
}

const t = new Temperatura();
t.celsius = 25;     // llama al setter
t.fahrenheit;       // 77 (llama al getter; se usa SIN paréntesis)
t.celsius = -300;   // ❌ RangeError
```

También funcionan en objetos literales:

```js
const rectangulo = {
  ancho: 10,
  alto: 5,
  get area() {
    return this.ancho * this.alto;
  },
};
rectangulo.area; // 50
```

> **Ideas clave**: getters para propiedades calculadas, setters para validar.

## 31. Symbols y símbolos bien conocidos

Un `Symbol` es un valor **único e irrepetible**. Sirve como clave de propiedades que no chocan con ninguna otra.

```js
const id1 = Symbol("id");
const id2 = Symbol("id");
id1 === id2; // false (aunque tengan la misma descripción)

const usuario = {
  nombre: "Ana",
  [id1]: 12345,
};

usuario[id1];          // 12345
Object.keys(usuario);  // ["nombre"] → los symbols no aparecen
JSON.stringify(usuario); // '{"nombre":"Ana"}'
```

### Símbolos bien conocidos: "enganchar" tu objeto al lenguaje

JS tiene symbols predefinidos que permiten personalizar cómo se comporta un objeto.

**`Symbol.iterator`**: hace tu objeto recorrible con `for...of` (lo vemos a fondo en el cap. 40).

```js
class Rango {
  constructor(desde, hasta) {
    this.desde = desde;
    this.hasta = hasta;
  }

  *[Symbol.iterator]() {
    for (let i = this.desde; i <= this.hasta; i++) yield i;
  }
}

for (const n of new Rango(1, 5)) console.log(n); // 1 2 3 4 5
[...new Rango(1, 3)]; // [1, 2, 3]
```

**`Symbol.toPrimitive`**: controla cómo se convierte a número o texto.

```js
class Dinero {
  constructor(cantidad) { this.cantidad = cantidad; }
  [Symbol.toPrimitive](tipo) {
    return tipo === "number" ? this.cantidad : `${this.cantidad.toFixed(2)} €`;
  }
}
const precio = new Dinero(19.5);
`${precio}`;  // "19.50 €"
precio * 2;   // 39
```

**`Symbol.toStringTag`**: personaliza `Object.prototype.toString`.

### Symbols globales

```js
const s1 = Symbol.for("app.config");
const s2 = Symbol.for("app.config");
s1 === s2; // true (registro global compartido)
```

> **Ideas clave**: symbols = claves únicas. `Symbol.iterator` es el más importante: hace objetos iterables.

## 🏋️ Ejercicios — Nivel 3 — Programación orientada a objetos

> 🟢 fácil · 🟡 medio · 🔴 difícil. Intenta cada ejercicio antes de abrir la solución.


### 3.1 🟢 ¿Qué es `this`? (cap. 25)
¿Qué muestra cada `console.log`? Explica por qué.

```js
const obj = {
  nombre: "Ana",
  normal() { return this?.nombre; },
  flecha: () => this?.nombre,
  conTimeout() {
    setTimeout(function () { console.log("A:", this?.nombre); }, 0);
    setTimeout(() => console.log("B:", this.nombre), 0);
  },
};

console.log(obj.normal());
console.log(obj.flecha());
const suelta = obj.normal;
console.log(suelta());
obj.conTimeout();
```

<details><summary>Solución</summary>

- `obj.normal()` → `"Ana"`: se llama como método, `this` es `obj`.
- `obj.flecha()` → `undefined`: las arrow functions no tienen `this` propio; usan el del módulo (que es `undefined`).
- `suelta()` → `undefined`: llamada suelta, `this` es `undefined` en modo estricto.
- `A: undefined`: la función normal pasada a `setTimeout` pierde el `this`.
- `B: Ana`: la arrow function hereda el `this` de `conTimeout`, que es `obj`.
</details>

### 3.2 🟡 Clase CuentaBancaria (cap. 27, 28, 30)
Crea una clase `CuentaBancaria` con:
- Campo privado `#saldo` y `titular` público.
- Métodos `ingresar(cantidad)` y `retirar(cantidad)` que validen (cantidad positiva, saldo suficiente) y lancen errores adecuados.
- Getter `saldo` (solo lectura).
- Un historial privado de movimientos y un método `extracto()` que devuelva una copia.

<details><summary>Solución</summary>

```js
class CuentaBancaria {
  #saldo = 0;
  #movimientos = [];

  constructor(titular, saldoInicial = 0) {
    this.titular = titular;
    if (saldoInicial > 0) this.ingresar(saldoInicial);
  }

  get saldo() {
    return this.#saldo;
  }

  ingresar(cantidad) {
    this.#validar(cantidad);
    this.#saldo += cantidad;
    this.#registrar("ingreso", cantidad);
    return this;
  }

  retirar(cantidad) {
    this.#validar(cantidad);
    if (cantidad > this.#saldo) throw new RangeError("Saldo insuficiente");
    this.#saldo -= cantidad;
    this.#registrar("retirada", cantidad);
    return this;
  }

  extracto() {
    return this.#movimientos.map(m => ({ ...m }));
  }

  #validar(cantidad) {
    if (typeof cantidad !== "number" || !(cantidad > 0)) {
      throw new TypeError("La cantidad debe ser un número positivo");
    }
  }

  #registrar(tipo, cantidad) {
    this.#movimientos.push({ tipo, cantidad, fecha: new Date().toISOString() });
  }
}

const cuenta = new CuentaBancaria("Ana", 100);
cuenta.ingresar(50).retirar(30);
cuenta.saldo;      // 120
cuenta.saldo = 1e6; // se ignora (no hay setter); en modo estricto da TypeError
```
</details>

### 3.3 🟡 Herencia de figuras (cap. 27)
Crea una clase base `Figura` con un método `area()` que lance un error ("debe implementarse") y un `toString()` que use `area()`. Crea `Rectangulo`, `Circulo` y `Cuadrado` (que herede de `Rectangulo`). Ordena un array de figuras por área.

<details><summary>Solución</summary>

```js
class Figura {
  area() {
    throw new Error(`${this.constructor.name} debe implementar area()`);
  }
  toString() {
    return `${this.constructor.name} de área ${this.area().toFixed(2)}`;
  }
}

class Rectangulo extends Figura {
  constructor(ancho, alto) {
    super();
    this.ancho = ancho;
    this.alto = alto;
  }
  area() { return this.ancho * this.alto; }
}

class Cuadrado extends Rectangulo {
  constructor(lado) { super(lado, lado); }
}

class Circulo extends Figura {
  constructor(radio) {
    super();
    this.radio = radio;
  }
  area() { return Math.PI * this.radio ** 2; }
}

const figuras = [new Rectangulo(3, 4), new Circulo(2), new Cuadrado(3)];
figuras.toSorted((a, b) => a.area() - b.area()).forEach(f => console.log(`${f}`));
// Cuadrado de área 9.00
// Rectangulo de área 12.00
// Circulo de área 12.57
```
</details>

### 3.4 🔴 Objeto iterable (cap. 31, 40)
Crea una clase `Playlist` que guarde canciones y sea iterable con `for...of`. Añade un método `*aleatoria()` (generador) que recorra las canciones en orden aleatorio sin repetir.

<details><summary>Solución</summary>

```js
class Playlist {
  #canciones = [];

  añadir(...canciones) {
    this.#canciones.push(...canciones);
    return this;
  }

  *[Symbol.iterator]() {
    yield* this.#canciones;
  }

  *aleatoria() {
    const copia = [...this.#canciones];
    // Algoritmo de Fisher-Yates
    for (let i = copia.length - 1; i > 0; i--) {
      const j = Math.floor(Math.random() * (i + 1));
      [copia[i], copia[j]] = [copia[j], copia[i]];
    }
    yield* copia;
  }
}

const lista = new Playlist().añadir("Txoria txori", "Bizkaia maite", "Hegoak");
for (const c of lista) console.log(c);
console.log([...lista.aleatoria()]);
```
</details>


---

# NIVEL 4 — Asincronía

## 32. El event loop

JavaScript es **monohilo**: solo ejecuta una cosa a la vez. Entonces, ¿cómo puede descargar datos, esperar temporizadores y responder a clics "a la vez"? Gracias al **event loop**.

### Las piezas

1. **Call stack (pila de llamadas)**: lo que se está ejecutando ahora mismo.
2. **APIs del entorno**: el navegador o Node se encargan de las tareas lentas (temporizadores, red, archivos) **fuera** del hilo de JS.
3. **Cola de microtareas**: callbacks de promesas (`then`, `await`). **Prioridad alta**.
4. **Cola de macrotareas** (tareas): `setTimeout`, eventos, I/O. **Prioridad normal**.

### El algoritmo (simplificado)

```
repetir siempre:
  1. Ejecutar todo el código síncrono hasta vaciar la pila
  2. Ejecutar TODAS las microtareas pendientes
  3. (navegador) Repintar la pantalla si hace falta
  4. Coger UNA macrotarea y ejecutarla
```

### El examen clásico: ¿en qué orden se imprime?

```js
console.log("1");

setTimeout(() => console.log("2"), 0);

Promise.resolve().then(() => console.log("3"));

queueMicrotask(() => console.log("4"));

console.log("5");
```

Resultado: **1, 5, 3, 4, 2**

- `1` y `5`: código síncrono.
- `3` y `4`: microtareas (se vacían antes de pasar a las macrotareas).
- `2`: macrotarea, aunque el tiempo sea 0.

### Consecuencia práctica: no bloquees el hilo

```js
// ❌ Esto congela la página 5 segundos: ningún clic responde
const fin = Date.now() + 5000;
while (Date.now() < fin) {}
```

Para cálculos pesados usa **Web Workers** (cap. 53).

> **Ideas clave**: un solo hilo + event loop. Microtareas (promesas) antes que macrotareas (setTimeout).

## 33. Callbacks

Un **callback** es una función que pasas a otra para que la llame "cuando termine".

```js
setTimeout(() => {
  console.log("Han pasado 2 segundos");
}, 2000);

boton.addEventListener("click", () => {
  console.log("¡Clic!");
});
```

### El callback hell (la pirámide de la perdición)

Cuando encadenas operaciones asíncronas con callbacks, el código se vuelve ilegible:

```js
obtenerUsuario(1, (error, usuario) => {
  if (error) return manejar(error);
  obtenerPedidos(usuario.id, (error, pedidos) => {
    if (error) return manejar(error);
    obtenerDetalle(pedidos[0].id, (error, detalle) => {
      if (error) return manejar(error);
      console.log(detalle);
      // ...y sigue creciendo hacia la derecha
    });
  });
});
```

Problemas: difícil de leer, de manejar errores y de mantener. La solución son las **promesas**.

> **Ideas clave**: los callbacks son la base, pero anidados se vuelven inmanejables.

## 34. Promesas

Una **promesa** es un objeto que representa un valor que **llegará en el futuro** (o un error).

Tiene tres estados:
- **pending** (pendiente)
- **fulfilled** (cumplida, con un valor)
- **rejected** (rechazada, con un error)

### Crear una promesa

```js
function esperar(ms) {
  return new Promise((resolve) => {
    setTimeout(resolve, ms);
  });
}

function tirarDado() {
  return new Promise((resolve, reject) => {
    const n = Math.ceil(Math.random() * 6);
    if (n === 1) reject(new Error("Ha salido un 1"));
    else resolve(n);
  });
}
```

### Consumir una promesa

```js
tirarDado()
  .then(n => {
    console.log("Ha salido", n);
    return n * 2;               // lo que devuelves pasa al siguiente then
  })
  .then(doble => console.log("El doble es", doble))
  .catch(error => console.error("Error:", error.message))
  .finally(() => console.log("Fin de la tirada"));
```

El callback hell anterior, con promesas:

```js
obtenerUsuario(1)
  .then(usuario => obtenerPedidos(usuario.id))
  .then(pedidos => obtenerDetalle(pedidos[0].id))
  .then(detalle => console.log(detalle))
  .catch(manejar); // un solo catch para todos los errores
```

### Combinar promesas

```js
const p1 = fetch("/api/usuarios");
const p2 = fetch("/api/productos");
const p3 = fetch("/api/pedidos");
```

| Método | Resuelve cuando… | Rechaza cuando… |
|---|---|---|
| `Promise.all([...])` | **todas** se cumplen | **una** falla |
| `Promise.allSettled([...])` **(ES2020)** | todas terminan (bien o mal) | nunca |
| `Promise.race([...])` | la **primera** termina (bien o mal) | la primera falla |
| `Promise.any([...])` **(ES2021)** | la **primera** se cumple | **todas** fallan |

```js
// all: todo o nada
const [usuarios, productos] = await Promise.all([p1, p2]);

// allSettled: quiero saber qué ha ido bien y qué mal
const resultados = await Promise.allSettled([p1, p2, p3]);
resultados.forEach(r => {
  if (r.status === "fulfilled") console.log("OK", r.value);
  else console.log("Fallo", r.reason);
});

// any: el servidor que responda primero
const respuesta = await Promise.any([
  fetch("https://servidor1.com/datos"),
  fetch("https://servidor2.com/datos"),
]);

// race: timeout casero
const conTimeout = Promise.race([
  fetch("/api/lenta"),
  esperar(3000).then(() => { throw new Error("Timeout"); }),
]);
```

> **Ideas clave**: `then` encadena, `catch` captura, `finally` siempre se ejecuta. `all` / `allSettled` / `race` / `any` combinan.

## 35. `async` / `await`

`async/await` es una forma de escribir código con promesas que **parece síncrono**. Es la forma recomendada hoy.

```js
async function mostrarPedido() {
  try {
    const usuario = await obtenerUsuario(1);
    const pedidos = await obtenerPedidos(usuario.id);
    const detalle = await obtenerDetalle(pedidos[0].id);
    console.log(detalle);
  } catch (error) {
    console.error("Algo falló:", error);
  } finally {
    console.log("Terminado");
  }
}
```

Reglas:
- `await` "pausa" la función hasta que la promesa se resuelve (sin bloquear el resto del programa).
- Una función `async` **siempre devuelve una promesa**.
- Los errores se capturan con `try/catch` normal.

### Ejemplo real con `fetch`

```js
async function obtenerPokemon(nombre) {
  const respuesta = await fetch(`https://pokeapi.co/api/v2/pokemon/${nombre}`);

  // fetch NO lanza error con 404 o 500: hay que comprobarlo
  if (!respuesta.ok) {
    throw new Error(`HTTP ${respuesta.status}`);
  }

  const datos = await respuesta.json();
  return { nombre: datos.name, altura: datos.height };
}

obtenerPokemon("pikachu").then(console.log);
```

### ⚠️ Error común: `await` en serie cuando podrían ir en paralelo

```js
// ❌ Lento: espera a uno para empezar el otro (2 + 2 = 4 segundos)
const a = await tarea2s();
const b = await tarea2s();

// ✅ Rápido: los dos a la vez (2 segundos)
const [a2, b2] = await Promise.all([tarea2s(), tarea2s()]);
```

### ⚠️ `await` dentro de `forEach` no funciona como esperas

```js
// ❌ forEach no espera
ids.forEach(async id => await procesar(id));

// ✅ En serie
for (const id of ids) {
  await procesar(id);
}

// ✅ En paralelo
await Promise.all(ids.map(id => procesar(id)));
```

### Top-level await (ES2022)

En **módulos**, puedes usar `await` fuera de funciones:

```js
// config.mjs
const respuesta = await fetch("/config.json");
export const config = await respuesta.json();
```

> **Ideas clave**: `async/await` + `try/catch`. Usa `Promise.all` para paralelizar. Comprueba `respuesta.ok` con `fetch`.

## 36. `Promise.withResolvers` (ES2024) y `Promise.try` (ES2025)

### `Promise.withResolvers()`

A veces necesitas crear una promesa y resolverla **desde fuera**. Antes:

```js
let resolver, rechazar;
const promesa = new Promise((res, rej) => {
  resolver = res;
  rechazar = rej;
});
```

Ahora:

```js
const { promise, resolve, reject } = Promise.withResolvers();
```

Ejemplo: esperar a que el usuario pulse un botón.

```js
function esperarClic(boton) {
  const { promise, resolve } = Promise.withResolvers();
  boton.addEventListener("click", resolve, { once: true });
  return promise;
}

await esperarClic(document.querySelector("#continuar"));
console.log("¡El usuario ha pulsado!");
```

### `Promise.try(fn)` (ES2025)

Ejecuta una función que **puede ser síncrona o asíncrona** y siempre te da una promesa. Si la función lanza un error síncrono, se convierte en promesa rechazada:

```js
function leerConfig(ruta) {
  if (!ruta) throw new Error("Falta la ruta"); // error síncrono
  return fetch(ruta).then(r => r.json());      // o una promesa
}

Promise.try(() => leerConfig(""))
  .then(config => console.log(config))
  .catch(err => console.error("Capturado:", err.message)); // ✅ lo captura igual
```

Sin `Promise.try`, el error síncrono escaparía al `.catch`.

> **Ideas clave**: `withResolvers` para resolver desde fuera; `try` para unificar errores síncronos y asíncronos.

## 37. Iteración asíncrona: `for await...of`

Cuando los datos llegan **poco a poco** (páginas de una API, líneas de un archivo, mensajes de un socket), usamos iteradores asíncronos.

```js
// Generador asíncrono: produce valores con espera
async function* paginas(url) {
  let siguiente = url;
  while (siguiente) {
    const respuesta = await fetch(siguiente);
    const datos = await respuesta.json();
    yield datos.results;      // entrega una página
    siguiente = datos.next;   // URL de la siguiente (o null)
  }
}

for await (const pagina of paginas("https://pokeapi.co/api/v2/pokemon?limit=100")) {
  console.log(`Página con ${pagina.length} pokémon`);
}
```

### Leer un archivo línea a línea en Node

```js
import { createReadStream } from "node:fs";
import { createInterface } from "node:readline";

const lineas = createInterface({ input: createReadStream("datos.csv") });

for await (const linea of lineas) {
  console.log(linea);
}
```

`for await` también funciona con un array de promesas: espera a cada una en orden.

> **Ideas clave**: `async function*` produce datos asíncronos; `for await...of` los consume.

## 38. ⭐ `Array.fromAsync` (ES2026)

`Array.from` convierte iterables en arrays. `Array.fromAsync` hace lo mismo con **iterables asíncronos** y devuelve una promesa:

```js
async function* numerosLentos() {
  for (let i = 1; i <= 3; i++) {
    await new Promise(r => setTimeout(r, 500));
    yield i;
  }
}

const numeros = await Array.fromAsync(numerosLentos());
console.log(numeros); // [1, 2, 3] (tras 1,5 s)
```

Con función de transformación:

```js
const dobles = await Array.fromAsync(numerosLentos(), n => n * 2); // [2, 4, 6]
```

Con el generador de páginas del capítulo anterior:

```js
const todasLasPaginas = await Array.fromAsync(paginas(urlInicial));
const todos = todasLasPaginas.flat();
```

También acepta un array de promesas:

```js
const datos = await Array.fromAsync([fetchA(), fetchB()]);
```

**Diferencia con `Promise.all`**: `Array.fromAsync` procesa los elementos **de uno en uno, en orden**; `Promise.all` los lanza todos a la vez.

> **Ideas clave**: `Array.fromAsync` = "recoge todo lo que produzca este iterable asíncrono en un array".

## 39. Cancelación con `AbortController` y timeouts

¿Qué pasa si el usuario se va de la página o la petición tarda demasiado? Se puede **cancelar**.

```js
const controlador = new AbortController();

fetch("/api/datos", { signal: controlador.signal })
  .then(r => r.json())
  .then(console.log)
  .catch(err => {
    if (err.name === "AbortError") console.log("Petición cancelada");
    else throw err;
  });

// Más tarde, por ejemplo al pulsar "Cancelar":
controlador.abort();
```

### Timeout en una línea: `AbortSignal.timeout`

```js
try {
  const r = await fetch("/api/lenta", { signal: AbortSignal.timeout(5000) });
} catch (err) {
  if (err.name === "TimeoutError") console.log("Tardó más de 5 segundos");
}
```

### Combinar señales: `AbortSignal.any`

```js
const usuarioCancela = new AbortController();

const signal = AbortSignal.any([
  usuarioCancela.signal,
  AbortSignal.timeout(10_000),
]);

fetch("/api/informe", { signal }); // se cancela por lo que ocurra antes
```

### Hacer tus propias funciones cancelables

```js
function esperar(ms, { signal } = {}) {
  return new Promise((resolve, reject) => {
    signal?.throwIfAborted();
    const id = setTimeout(resolve, ms);
    signal?.addEventListener("abort", () => {
      clearTimeout(id);
      reject(signal.reason);
    }, { once: true });
  });
}
```

### Quitar event listeners de golpe

```js
const ctrl = new AbortController();
window.addEventListener("resize", onResize, { signal: ctrl.signal });
window.addEventListener("scroll", onScroll, { signal: ctrl.signal });

ctrl.abort(); // elimina los dos listeners
```

> **Ideas clave**: `AbortController` cancela; `AbortSignal.timeout` pone límite de tiempo; `AbortSignal.any` combina.

## 🏋️ Ejercicios — Nivel 4 — Asincronía

> 🟢 fácil · 🟡 medio · 🔴 difícil. Intenta cada ejercicio antes de abrir la solución.


### 4.1 🟢 El orden del event loop (cap. 32)
¿En qué orden se imprimen los números? Razónalo antes de ejecutarlo.

```js
console.log(1);
setTimeout(() => console.log(2), 0);
Promise.resolve().then(() => {
  console.log(3);
  setTimeout(() => console.log(4), 0);
});
queueMicrotask(() => console.log(5));
(async () => {
  console.log(6);
  await null;
  console.log(7);
})();
console.log(8);
```

<details><summary>Solución</summary>

**1, 6, 8, 3, 5, 7, 2, 4**

- Síncrono: `1`, `6` (el cuerpo de una función async se ejecuta síncronamente hasta el primer `await`), `8`.
- Microtareas en orden de registro: `3` (y programa el timeout 4), `5`, `7` (lo que va después de `await` es una microtarea).
- Macrotareas: `2` (registrado antes) y `4`.
</details>

### 4.2 🟢 Promesificar `setTimeout` (cap. 34)
Escribe `esperar(ms)` que devuelva una promesa, y úsala para mostrar "3", "2", "1", "¡Despegue!" con un segundo entre cada mensaje, usando `async/await`.

<details><summary>Solución</summary>

```js
const esperar = ms => new Promise(resolve => setTimeout(resolve, ms));

async function cuentaAtras(desde = 3) {
  for (let i = desde; i > 0; i--) {
    console.log(i);
    await esperar(1000);
  }
  console.log("¡Despegue!");
}

cuentaAtras();
```
</details>

### 4.3 🟡 Consumir una API (cap. 35)
Usando la API pública `https://jsonplaceholder.typicode.com`, escribe `resumenUsuario(id)` que:
1. Obtenga el usuario (`/users/{id}`) y sus posts (`/posts?userId={id}`) **en paralelo**.
2. Compruebe `respuesta.ok` y lance un error si falla.
3. Devuelva `{ nombre, email, totalPosts, primerTitulo }`.

<details><summary>Solución</summary>

```js
const BASE = "https://jsonplaceholder.typicode.com";

async function obtenerJSON(url) {
  const r = await fetch(url);
  if (!r.ok) throw new Error(`HTTP ${r.status} en ${url}`);
  return r.json();
}

async function resumenUsuario(id) {
  const [usuario, posts] = await Promise.all([
    obtenerJSON(`${BASE}/users/${id}`),
    obtenerJSON(`${BASE}/posts?userId=${id}`),
  ]);

  return {
    nombre: usuario.name,
    email: usuario.email,
    totalPosts: posts.length,
    primerTitulo: posts[0]?.title ?? "(sin posts)",
  };
}

try {
  console.log(await resumenUsuario(1));
} catch (e) {
  console.error("No se pudo obtener el resumen:", e.message);
}
```
</details>

### 4.4 🟡 Reintentos (cap. 35, 36)
Escribe `conReintentos(fn, intentos = 3, espera = 500)` que ejecute la función asíncrona `fn`; si falla, la reintente hasta `intentos` veces, esperando cada vez el doble (500, 1000, 2000 ms: *backoff exponencial*). Si falla todas, lanza un error con `cause` apuntando al último error.

<details><summary>Solución</summary>

```js
const esperar = ms => new Promise(r => setTimeout(r, ms));

async function conReintentos(fn, intentos = 3, espera = 500) {
  let ultimoError;
  for (let i = 1; i <= intentos; i++) {
    try {
      return await Promise.try(fn);
    } catch (error) {
      ultimoError = error;
      console.warn(`Intento ${i} fallido: ${error.message}`);
      if (i < intentos) await esperar(espera * 2 ** (i - 1));
    }
  }
  throw new Error(`Fallaron los ${intentos} intentos`, { cause: ultimoError });
}

// Prueba: falla 2 veces y a la tercera funciona
let llamadas = 0;
const inestable = async () => {
  if (++llamadas < 3) throw new Error("Servidor ocupado");
  return "¡Datos!";
};

console.log(await conReintentos(inestable)); // "¡Datos!"
```
</details>

### 4.5 🟡 Límite de tiempo (cap. 39)
Modifica `obtenerJSON` del ejercicio 4.3 para que acepte un tiempo máximo (por defecto 5 s) usando `AbortSignal.timeout`, y muestre un mensaje claro si se supera.

<details><summary>Solución</summary>

```js
async function obtenerJSON(url, { timeout = 5000 } = {}) {
  try {
    const r = await fetch(url, { signal: AbortSignal.timeout(timeout) });
    if (!r.ok) throw new Error(`HTTP ${r.status}`);
    return await r.json();
  } catch (error) {
    if (error.name === "TimeoutError") {
      throw new Error(`La petición a ${url} tardó más de ${timeout} ms`, { cause: error });
    }
    throw error;
  }
}
```
</details>

### 4.6 🔴 Paginación con generador asíncrono (cap. 37, 38)
La API `https://jsonplaceholder.typicode.com/posts?_page=N&_limit=10` devuelve 10 posts por página (100 en total). Escribe un generador asíncrono `paginas()` que vaya pidiendo páginas hasta recibir una vacía, y usa `Array.fromAsync` para recogerlas todas y contar los posts.

<details><summary>Solución</summary>

```js
async function* paginas(limite = 10) {
  for (let pagina = 1; ; pagina++) {
    const r = await fetch(
      `https://jsonplaceholder.typicode.com/posts?_page=${pagina}&_limit=${limite}`
    );
    const posts = await r.json();
    if (posts.length === 0) return; // fin del generador
    yield posts;
  }
}

// Consumir de una en una
for await (const p of paginas()) {
  console.log(`Página con ${p.length} posts`);
}

// Recoger todas (ES2026)
const todas = await Array.fromAsync(paginas());
console.log("Total:", todas.flat().length); // 100
```
</details>

### 4.7 🔴 Cola con concurrencia limitada (cap. 34–36)
Tienes 20 URLs y quieres descargarlas, pero **como máximo 3 a la vez**. Escribe `ejecutarConLimite(tareas, limite)` donde `tareas` es un array de funciones que devuelven promesas. Debe devolver los resultados en el mismo orden.

<details><summary>Solución</summary>

```js
async function ejecutarConLimite(tareas, limite = 3) {
  const resultados = new Array(tareas.length);
  let siguiente = 0;

  async function trabajador() {
    while (siguiente < tareas.length) {
      const indice = siguiente++; // cada trabajador coge la siguiente tarea libre
      resultados[indice] = await tareas[indice]();
    }
  }

  // Lanza "limite" trabajadores que van cogiendo tareas
  await Promise.all(Array.from({ length: limite }, trabajador));
  return resultados;
}

// Prueba
const esperar = ms => new Promise(r => setTimeout(r, ms));
const tareas = Array.from({ length: 10 }, (_, i) => async () => {
  console.log("Empieza", i);
  await esperar(300);
  return i * 10;
});

console.log(await ejecutarConLimite(tareas, 3));
```

Como JS es monohilo, `siguiente++` nunca se ejecuta a la vez en dos trabajadores: no hay condiciones de carrera.
</details>


---

# NIVEL 5 — Iteradores, generadores y metaprogramación

## 40. El protocolo iterable / iterador

¿Por qué `for...of` funciona con arrays, strings, `Map` y `Set`, pero no con objetos normales? Porque los primeros cumplen el **protocolo iterable**.

- Un **iterable** es un objeto con un método `[Symbol.iterator]()` que devuelve un iterador.
- Un **iterador** es un objeto con un método `next()` que devuelve `{ value, done }`.

```js
const arr = ["a", "b"];
const it = arr[Symbol.iterator]();

it.next(); // { value: "a", done: false }
it.next(); // { value: "b", done: false }
it.next(); // { value: undefined, done: true }
```

### Crear un iterable a mano

```js
const cuentaAtras = {
  desde: 3,
  [Symbol.iterator]() {
    let actual = this.desde;
    return {
      next() {
        if (actual >= 0) return { value: actual--, done: false };
        return { value: undefined, done: true };
      },
    };
  },
};

for (const n of cuentaAtras) console.log(n); // 3, 2, 1, 0
[...cuentaAtras];            // [3, 2, 1, 0]
const [a, b] = cuentaAtras;  // 3, 2
```

Todo lo que acepta iterables funciona con tu objeto: `for...of`, spread, desestructuración, `Array.from`, `new Set(...)`, `Promise.all`…

> **Ideas clave**: iterable = tiene `[Symbol.iterator]`. Iterador = tiene `next()`. Escribirlos a mano es tedioso: para eso están los generadores.

## 41. Generadores

Un **generador** es una función que puede **pausarse** con `yield` y continuar después. Se declara con `function*`.

```js
function* saludos() {
  console.log("Empiezo");
  yield "Hola";
  console.log("Sigo");
  yield "¿Qué tal?";
  console.log("Termino");
}

const gen = saludos();  // no se ejecuta nada todavía
gen.next(); // "Empiezo" → { value: "Hola", done: false }
gen.next(); // "Sigo"    → { value: "¿Qué tal?", done: false }
gen.next(); // "Termino" → { value: undefined, done: true }
```

Los generadores **son iterables** automáticamente:

```js
function* rango(desde, hasta, paso = 1) {
  for (let i = desde; i <= hasta; i += paso) yield i;
}

[...rango(0, 10, 2)]; // [0, 2, 4, 6, 8, 10]
```

### Secuencias infinitas (evaluación perezosa)

Un generador solo calcula el siguiente valor **cuando se lo pides**, así que puede ser infinito:

```js
function* fibonacci() {
  let [a, b] = [0, 1];
  while (true) {
    yield a;
    [a, b] = [b, a + b];
  }
}

const fib = fibonacci();
for (const n of fib) {
  if (n > 100) break;
  console.log(n); // 0 1 1 2 3 5 8 13 21 34 55 89
}
```

### Generador de IDs

```js
function* generadorIds(prefijo = "id") {
  let n = 1;
  while (true) yield `${prefijo}-${n++}`;
}

const ids = generadorIds("alumno");
ids.next().value; // "alumno-1"
ids.next().value; // "alumno-2"
```

### `yield*`: delegar en otro iterable

```js
function* todo() {
  yield* [1, 2];
  yield* "ab";
  yield 3;
}
[...todo()]; // [1, 2, "a", "b", 3]
```

> **Ideas clave**: `function*` + `yield` = funciones pausables. Perfectos para secuencias perezosas e infinitas.

## 42. Iterator helpers (ES2025)

Hasta ahora, `map`, `filter`… solo existían en arrays. Para usarlos con un generador había que convertirlo en array primero (y con uno infinito, imposible).

ES2025 añade estos métodos **directamente a los iteradores**, y además son **perezosos**: solo procesan lo necesario.

| Método | Qué hace |
|---|---|
| `.map(fn)` | Transforma cada valor |
| `.filter(fn)` | Filtra |
| `.take(n)` | Se queda con los primeros n |
| `.drop(n)` | Se salta los primeros n |
| `.flatMap(fn)` | Transforma y aplana |
| `.reduce(fn, inicial)` | Acumula |
| `.toArray()` | Convierte a array |
| `.forEach(fn)` | Recorre |
| `.some(fn)` / `.every(fn)` / `.find(fn)` | Comprueban / buscan |

```js
// Los 5 primeros números de Fibonacci pares
const pares = fibonacci()
  .filter(n => n % 2 === 0)
  .take(5)
  .toArray();
// [0, 2, 8, 34, 144]
```

Funciona con un generador **infinito** porque `take(5)` corta en cuanto tiene 5.

### Con Map y Set

```js
const notas = new Map([["Ana", 8], ["Luis", 4], ["Eva", 9]]);

const aprobados = notas.entries()
  .filter(([, nota]) => nota >= 5)
  .map(([nombre]) => nombre)
  .toArray();
// ["Ana", "Eva"]
```

### `Iterator.from`

Convierte cualquier iterable (o "iterador-like") en un iterador con todos los helpers:

```js
Iterator.from("hola mundo")
  .filter(c => c !== " ")
  .map(c => c.toUpperCase())
  .toArray(); // ["H","O","L","A","M","U","N","D","O"]
```

### ¿Por qué perezoso importa?

```js
// Con arrays: procesa 1.000.000 de elementos en cada paso
grandeArray.map(f).filter(g).slice(0, 3);

// Con iteradores: procesa solo hasta encontrar 3
grandeArray.values().map(f).filter(g).take(3).toArray();
```

> **Ideas clave**: los iteradores ya tienen `map`, `filter`, `take`… y solo trabajan lo justo.

## 43. ⭐ `Iterator.concat` (ES2026)

Une varios iterables en **uno solo, de forma perezosa**, sin crear arrays intermedios:

```js
const primeros = [1, 2, 3];
const segundos = new Set([4, 5]);
function* terceros() { yield 6; yield 7; }

const todos = Iterator.concat(primeros, segundos, terceros());

for (const n of todos) console.log(n); // 1 2 3 4 5 6 7
```

Diferencia con `[...a, ...b]`: el spread crea un array nuevo en memoria con todo; `Iterator.concat` va entregando los elementos de uno en uno.

Combina perfectamente con los helpers:

```js
const alumnosMañana = ["Ana", "Luis"];
const alumnosTarde = new Set(["Eva", "Iker"]);

Iterator.concat(alumnosMañana, alumnosTarde)
  .map(n => n.toUpperCase())
  .toArray(); // ["ANA", "LUIS", "EVA", "IKER"]
```

> **Ideas clave**: `Iterator.concat` encadena iterables sin copiarlos.

## 44. `Proxy` y `Reflect`

### `Proxy`: interceptar operaciones sobre un objeto

Un `Proxy` envuelve un objeto y permite **interceptar** lecturas, escrituras, borrados… Es *metaprogramación*: código que modifica el comportamiento de otro código.

```js
const usuario = { nombre: "Ana", edad: 30 };

const vigilado = new Proxy(usuario, {
  get(objetivo, propiedad) {
    console.log(`Leyendo ${String(propiedad)}`);
    return objetivo[propiedad];
  },
  set(objetivo, propiedad, valor) {
    console.log(`Cambiando ${String(propiedad)} a ${valor}`);
    objetivo[propiedad] = valor;
    return true; // indica que la asignación fue bien
  },
});

vigilado.nombre;     // "Leyendo nombre"
vigilado.edad = 31;  // "Cambiando edad a 31"
```

Las funciones `get`, `set`… se llaman **traps** (trampas).

### Usos prácticos

**Validación**:

```js
function crearValidado(objetivo, esquema) {
  return new Proxy(objetivo, {
    set(obj, prop, valor) {
      const validar = esquema[prop];
      if (validar && !validar(valor)) {
        throw new TypeError(`Valor no válido para ${prop}: ${valor}`);
      }
      obj[prop] = valor;
      return true;
    },
  });
}

const alumno = crearValidado({}, {
  edad: v => Number.isInteger(v) && v >= 0,
  email: v => /^[^@\s]+@[^@\s]+$/.test(v),
});

alumno.edad = 17;      // ✅
alumno.edad = -3;      // ❌ TypeError
```

**Valores por defecto**:

```js
const traducciones = new Proxy({ hola: "kaixo" }, {
  get: (obj, clave) => obj[clave] ?? `[${String(clave)} sin traducir]`,
});
traducciones.hola;   // "kaixo"
traducciones.adios;  // "[adios sin traducir]"
```

**Reactividad**: Vue.js usa `Proxy` para detectar cambios en los datos y repintar la interfaz automáticamente.

### `Reflect`: las operaciones "normales"

`Reflect` tiene un método por cada trap, que hace la operación por defecto. Se usa dentro de los proxies para no reinventar el comportamiento:

```js
const registro = new Proxy(objeto, {
  set(obj, prop, valor, receptor) {
    console.log(`set ${String(prop)}`);
    return Reflect.set(obj, prop, valor, receptor); // comportamiento normal
  },
});

Reflect.has({ a: 1 }, "a");       // true (como "a" in obj)
Reflect.ownKeys({ a: 1, [Symbol()]: 2 }); // ["a", Symbol()]
```

> **Ideas clave**: `Proxy` intercepta operaciones; `Reflect` ejecuta la operación estándar. Base de frameworks reactivos.

## 45. Decoradores (propuesta en Stage 3)

Los **decoradores** son funciones que modifican clases, métodos o campos con una sintaxis `@nombre`. **Todavía no forman parte del estándar** (están en Stage 3), pero ya los usas en TypeScript y en frameworks como **Angular** (`@Component`, `@Injectable`).

```js
function log(metodo, contexto) {
  return function (...args) {
    console.log(`→ ${contexto.name}(${args.join(", ")})`);
    const resultado = metodo.apply(this, args);
    console.log(`← ${contexto.name} = ${resultado}`);
    return resultado;
  };
}

class Calculadora {
  @log
  sumar(a, b) {
    return a + b;
  }
}

new Calculadora().sumar(2, 3);
// → sumar(2, 3)
// ← sumar = 5
```

Un decorador de método recibe:
- `metodo`: la función original.
- `contexto`: información (`name`, `kind`, `static`, `private`, `addInitializer`…).

Y devuelve la función que la sustituye.

### Decorador `accessor`

```js
function noNegativo(valor, contexto) {
  return {
    set(v) {
      if (v < 0) throw new RangeError(`${contexto.name} no puede ser negativo`);
      valor.set.call(this, v);
    },
  };
}

class Producto {
  @noNegativo accessor stock = 0;
}
```

> 💡 Para probar decoradores hoy necesitas **TypeScript 5+** o un transpilador como Babel. Los decoradores "experimentales" antiguos de TypeScript (`experimentalDecorators`) son **distintos** a los del estándar.

> **Ideas clave**: `@decorador` envuelve y modifica clases y métodos. Ya los usas en Angular; pronto serán estándar.

## 🏋️ Ejercicios — Nivel 5 — Iteradores, generadores y metaprogramación

> 🟢 fácil · 🟡 medio · 🔴 difícil. Intenta cada ejercicio antes de abrir la solución.


### 5.1 🟢 Generador de rangos (cap. 41)
Escribe un generador `rango(inicio, fin, paso = 1)` que también funcione hacia atrás si `paso` es negativo. `[...rango(10, 0, -3)]` → `[10, 7, 4, 1]`.

<details><summary>Solución</summary>

```js
function* rango(inicio, fin, paso = 1) {
  if (paso === 0) throw new RangeError("El paso no puede ser 0");
  if (paso > 0) {
    for (let i = inicio; i <= fin; i += paso) yield i;
  } else {
    for (let i = inicio; i >= fin; i += paso) yield i;
  }
}

[...rango(1, 5)];        // [1, 2, 3, 4, 5]
[...rango(10, 0, -3)];   // [10, 7, 4, 1]
```
</details>

### 5.2 🟡 Números primos perezosos (cap. 41, 42)
Escribe un generador infinito `primos()` y, usando iterator helpers, obtén:
a) Los 10 primeros primos.
b) Los 5 primeros primos mayores que 100.
c) La suma de los primos menores que 50 (pista: no puedes usar `filter` sobre un infinito para "parar"; busca otra forma).

<details><summary>Solución</summary>

```js
function esPrimo(n) {
  if (n < 2) return false;
  for (let d = 2; d * d <= n; d++) if (n % d === 0) return false;
  return true;
}

function* primos() {
  for (let n = 2; ; n++) if (esPrimo(n)) yield n;
}

// a
primos().take(10).toArray(); // [2, 3, 5, 7, 11, 13, 17, 19, 23, 29]

// b
primos().filter(p => p > 100).take(5).toArray(); // [101, 103, 107, 109, 113]

// c — se cuentan cuántos primos hay < 50 y se toman esos
// Más elegante: un generador que corte con una condición
function* mientras(iterable, condicion) {
  for (const x of iterable) {
    if (!condicion(x)) return;
    yield x;
  }
}
mientras(primos(), p => p < 50).reduce((a, b) => a + b, 0); // 328
```

En (c), `filter(p => p < 50)` sobre un iterador infinito **nunca terminaría**: seguiría buscando más elementos para siempre.
</details>

### 5.3 🟡 Concatenar fuentes (cap. 42, 43)
Tienes alumnos en tres fuentes: un array, un `Set` y un generador. Con `Iterator.concat`, obtén los nombres únicos, en mayúsculas y ordenados.

```js
const grupoA = ["ana", "luis"];
const grupoB = new Set(["eva", "ana"]);
function* grupoC() { yield "iker"; yield "luis"; }
```

<details><summary>Solución</summary>

```js
const resultado = [
  ...new Set(
    Iterator.concat(grupoA, grupoB, grupoC())
      .map(n => n.toUpperCase())
  ),
].toSorted();
// ["ANA", "EVA", "IKER", "LUIS"]
```
</details>

### 5.4 🔴 Objeto observable con Proxy (cap. 44)
Escribe `observable(objeto, alCambiar)` que devuelva un `Proxy`: cada vez que cambie una propiedad, llama a `alCambiar(propiedad, valorAnterior, valorNuevo)`. Si el valor no cambia, no avisa. Impide borrar propiedades que empiecen por `_`.

<details><summary>Solución</summary>

```js
function observable(objeto, alCambiar) {
  return new Proxy(objeto, {
    set(obj, prop, valor, receptor) {
      const anterior = obj[prop];
      const ok = Reflect.set(obj, prop, valor, receptor);
      if (ok && !Object.is(anterior, valor)) alCambiar(prop, anterior, valor);
      return ok;
    },
    deleteProperty(obj, prop) {
      if (typeof prop === "string" && prop.startsWith("_")) {
        throw new Error(`No se puede borrar la propiedad interna ${prop}`);
      }
      return Reflect.deleteProperty(obj, prop);
    },
  });
}

const estado = observable({ contador: 0, _id: 7 }, (p, antes, despues) =>
  console.log(`${String(p)}: ${antes} → ${despues}`)
);

estado.contador++;    // "contador: 0 → 1"
estado.contador = 1;  // (no avisa: no ha cambiado)
delete estado._id;    // ❌ Error
```
</details>


---

# NIVEL 6 — Errores, módulos y datos binarios

## 46. Manejo de errores

### `try / catch / finally`

```js
try {
  const datos = JSON.parse("{ esto no es JSON }");
} catch (error) {
  console.error("No se pudo leer:", error.message);
} finally {
  console.log("Esto se ejecuta siempre");
}
```

Desde ES2019 el parámetro del `catch` es opcional:

```js
try {
  localStorage.setItem("x", "1");
} catch {
  console.warn("localStorage no disponible");
}
```

### Lanzar errores con `throw`

```js
function dividir(a, b) {
  if (b === 0) throw new RangeError("No se puede dividir entre 0");
  return a / b;
}
```

**Lanza siempre objetos `Error`**, nunca strings (`throw "error"`): los `Error` incluyen la traza (`stack`) que indica dónde ocurrió.

### Tipos de error nativos

| Tipo | Cuándo |
|---|---|
| `Error` | Genérico |
| `TypeError` | Tipo incorrecto (`undefined.x`, llamar a algo que no es función) |
| `RangeError` | Valor fuera de rango |
| `ReferenceError` | Variable que no existe |
| `SyntaxError` | Código o JSON mal escrito |
| `AggregateError` | Varios errores juntos (`Promise.any`) |

### Errores personalizados

```js
class ErrorValidacion extends Error {
  constructor(campo, mensaje) {
    super(mensaje);
    this.name = "ErrorValidacion";
    this.campo = campo;
  }
}

try {
  throw new ErrorValidacion("email", "El email no es válido");
} catch (e) {
  if (e instanceof ErrorValidacion) {
    console.log(`Error en ${e.campo}: ${e.message}`);
  } else {
    throw e; // no es nuestro: relanzarlo
  }
}
```

### `cause`: encadenar errores (ES2022)

Permite envolver un error en otro sin perder el original:

```js
async function cargarPerfil(id) {
  try {
    const r = await fetch(`/api/usuarios/${id}`);
    return await r.json();
  } catch (error) {
    throw new Error(`No se pudo cargar el perfil ${id}`, { cause: error });
  }
}

try {
  await cargarPerfil(7);
} catch (e) {
  console.log(e.message);        // "No se pudo cargar el perfil 7"
  console.log(e.cause.message);  // el error original de red
}
```

### Errores no capturados

```js
// Navegador
window.addEventListener("error", e => console.log("Error global", e.error));
window.addEventListener("unhandledrejection", e => console.log("Promesa sin catch", e.reason));

// Node
process.on("unhandledRejection", (razon) => console.error(razon));
```

> **Ideas clave**: lanza objetos `Error`, crea subclases para tus errores y usa `cause` para no perder el error original.

## 47. ⭐ `Error.isError` (ES2026)

¿Cómo sabes si un valor es un error? `instanceof Error` parece suficiente, pero **falla** cuando el error viene de otro "realm" (otro iframe, un worker, un módulo `vm` de Node):

```js
const iframe = document.createElement("iframe");
document.body.append(iframe);
const ErrorDelIframe = iframe.contentWindow.Error;

const e = new ErrorDelIframe("hola");
e instanceof Error;  // false 😱 (es otro constructor Error)
Error.isError(e);    // true ✅
```

Además, `instanceof` se puede engañar:

```js
const falso = Object.create(Error.prototype);
falso instanceof Error; // true 😱 (no es un error real)
Error.isError(falso);   // false ✅
```

Uso típico, en código que recibe "cualquier cosa" en un `catch`:

```js
try {
  algoQuePuedeLanzarCualquierCosa();
} catch (valor) {
  const mensaje = Error.isError(valor) ? valor.message : String(valor);
  registrar(mensaje);
}
```

> **Ideas clave**: `Error.isError(x)` es la forma fiable de comprobar si algo es un error.

## 48. Módulos ES

Los **módulos** permiten dividir el código en archivos, cada uno con su propio ámbito.

### Exportar

```js
// matematicas.js

// Exportaciones con nombre (puede haber muchas)
export const PI = 3.14159;
export function sumar(a, b) { return a + b; }
export class Vector { /* ... */ }

// Exportación por defecto (solo una por archivo)
export default function multiplicar(a, b) { return a * b; }
```

### Importar

```js
// app.js
import multiplicar, { PI, sumar } from "./matematicas.js";
import { sumar as suma } from "./matematicas.js";   // renombrar
import * as mates from "./matematicas.js";          // todo en un objeto
mates.sumar(1, 2);
```

⚠️ En el navegador y en Node con módulos ES, **la extensión `.js` es obligatoria** en las rutas relativas.

### Reexportar (archivos "barril")

```js
// utils/index.js
export { sumar, PI } from "./matematicas.js";
export * from "./fechas.js";
export { default as Logger } from "./logger.js";
```

### `import()` dinámico: cargar bajo demanda

Devuelve una promesa. Ideal para cargar código pesado solo cuando se necesita:

```js
boton.addEventListener("click", async () => {
  const { generarPDF } = await import("./pdf.js");
  generarPDF();
});
```

### `import.meta`

Información sobre el módulo actual:

```js
import.meta.url;      // URL del archivo actual
import.meta.dirname;  // (Node) carpeta del archivo
import.meta.filename; // (Node) ruta completa del archivo

// Ruta relativa al módulo (funciona en navegador y Node)
const rutaDatos = new URL("./datos.json", import.meta.url);
```

### Características de los módulos

- Se ejecutan **una sola vez** aunque se importen muchas veces.
- Están siempre en **modo estricto**.
- Las variables de un módulo **no son globales**.
- Las importaciones son **en vivo**: si el módulo cambia el valor exportado, lo ves actualizado.

### CommonJS (lo antiguo de Node)

Lo verás en código antiguo:

```js
const fs = require("fs");
module.exports = { sumar };
```

Hoy se recomienda usar siempre módulos ES (`import`/`export`).

> **Ideas clave**: `export`/`import` con nombre por defecto; `import()` para cargar bajo demanda; extensión `.js` obligatoria.

## 49. Import attributes y módulos JSON (ES2025)

Puedes importar un JSON **directamente**, indicando su tipo con `with`:

```js
import config from "./config.json" with { type: "json" };

console.log(config.apiUrl);
```

¿Por qué hace falta `with { type: "json" }`? Por **seguridad**: si el servidor devolviera JavaScript en vez de JSON, el navegador se negaría a ejecutarlo. Así nunca ejecutas código creyendo que importas datos.

También funciona con `import()` dinámico:

```js
const { default: traducciones } = await import(`./i18n/${idioma}.json`, {
  with: { type: "json" },
});
```

> 💡 Verás código antiguo con `assert { type: "json" }`: es la sintaxis vieja y ya está obsoleta. Usa `with`.

> **Ideas clave**: `import datos from "./x.json" with { type: "json" }`.

## 50. Expresiones regulares modernas

Una **expresión regular** (regex) es un patrón para buscar texto.

### Lo básico

```js
const regex = /\d{5}/;          // 5 dígitos
regex.test("CP 48001");         // true
"CP 48001".match(/\d{5}/)[0];   // "48001"
"a1b2c3".replace(/\d/g, "#");   // "a#b#c#" (g = global, todas)
```

Chuleta rápida:

| Patrón | Significa |
|---|---|
| `\d` / `\w` / `\s` | dígito / letra-número-guion bajo / espacio |
| `.` | cualquier carácter |
| `*` / `+` / `?` | 0 o más / 1 o más / 0 o 1 |
| `{2,4}` | entre 2 y 4 veces |
| `[abc]` / `[^abc]` | uno de esos / ninguno de esos |
| `^` / `$` | inicio / fin |
| `( )` | grupo de captura |
| `a|b` | a o b |

Flags: `g` (global), `i` (sin distinguir mayúsculas), `m` (multilínea), `s` (el `.` incluye saltos de línea), `u`/`v` (Unicode).

### Grupos con nombre (ES2018)

```js
const fecha = /(?<dia>\d{2})\/(?<mes>\d{2})\/(?<año>\d{4})/;
const { dia, mes, año } = "19/11/2026".match(fecha).groups;
```

### Lookbehind (ES2018)

Buscar algo **precedido** de otra cosa:

```js
"Precio: 25€, Envío: 5€".match(/(?<=: )\d+/g); // ["25", "5"]
```

### `matchAll` (ES2020)

```js
const texto = "Ana: 8, Luis: 6, Eva: 9";
for (const m of texto.matchAll(/(?<nombre>\w+): (?<nota>\d)/g)) {
  console.log(m.groups.nombre, m.groups.nota);
}
```

### Flag `d`: índices de los grupos (ES2022)

```js
const m = /(?<año>\d{4})/d.exec("Curso 2026");
m.indices.groups.año; // [6, 10] → posición inicial y final
```

### Flag `v`: Unicode mejorado (ES2024)

Permite operaciones de conjuntos dentro de `[ ]` y propiedades de strings:

```js
// Letras griegas que NO sean la letra pi (resta de conjuntos)
/[\p{Script=Greek}--[π]]/v.test("α"); // true

// Detectar emojis completos (incluidos los compuestos)
/^\p{RGI_Emoji}$/v.test("👨‍👩‍👧"); // true
```

### Modificadores en línea (ES2025)

Activar un flag **solo en una parte** del patrón:

```js
// "hola" sin distinguir mayúsculas, pero "MUNDO" exacto
/(?i:hola) MUNDO/.test("HoLa MUNDO"); // true
/(?i:hola) MUNDO/.test("hola mundo"); // false
```

### Grupos con nombre duplicados (ES2025)

El mismo nombre en alternativas distintas:

```js
const fechaFlexible = /(?<año>\d{4})-\d{2}|\d{2}\/(?<año>\d{4})/;
"2026-11".match(fechaFlexible).groups.año;  // "2026"
"11/2026".match(fechaFlexible).groups.año;  // "2026"
```

### `RegExp.escape` (ES2025)

Escapa caracteres especiales para usar texto del usuario dentro de una regex con seguridad:

```js
const busqueda = "1+1=2 (fácil)";

new RegExp(busqueda);                  // ❌ el + y los paréntesis tienen significado especial
new RegExp(RegExp.escape(busqueda));   // ✅ busca el texto literal
```

> **Ideas clave**: grupos con nombre para legibilidad; `RegExp.escape` siempre que metas texto del usuario en una regex.

## 51. TypedArrays, ArrayBuffer y `Float16Array`

Para trabajar con **datos binarios** (imágenes, audio, archivos, protocolos de red, WebGL, sensores de un ESP32…) JS tiene estructuras especiales.

### `ArrayBuffer`: memoria en bruto

```js
const buffer = new ArrayBuffer(8); // 8 bytes, todo ceros
```

No se puede leer directamente: necesitas una **vista**.

### TypedArrays: vistas con tipo

| Tipo | Bytes por elemento | Rango |
|---|---|---|
| `Uint8Array` | 1 | 0 a 255 |
| `Int8Array` | 1 | -128 a 127 |
| `Uint16Array` / `Int16Array` | 2 | |
| `Uint32Array` / `Int32Array` | 4 | |
| `Float16Array` **(ES2025)** | 2 | decimales de media precisión |
| `Float32Array` / `Float64Array` | 4 / 8 | decimales |
| `BigInt64Array` / `BigUint64Array` | 8 | enteros enormes |

```js
const bytes = new Uint8Array([72, 111, 108, 97]);
new TextDecoder().decode(bytes); // "Hola"

new TextEncoder().encode("Kaixo"); // Uint8Array [75, 97, 105, 120, 111]

const pixeles = new Uint8ClampedArray(4); // valores limitados a 0-255
pixeles[0] = 300; // se queda en 255
```

Tienen casi todos los métodos de los arrays (`map`, `filter`, `at`, `toSorted`…), pero su tamaño es **fijo**.

### `DataView`: leer formatos binarios

```js
const vista = new DataView(buffer);
vista.setInt16(0, -500);
vista.setFloat32(2, 3.14);
vista.getInt16(0); // -500
```

### ArrayBuffer redimensionable (ES2024)

```js
const buf = new ArrayBuffer(4, { maxByteLength: 16 });
buf.resize(12);   // crece sin copiar los datos
buf.byteLength;   // 12

// Transferir la memoria (el original queda inutilizable, sin copia):
const nuevo = buf.transfer();
buf.detached; // true
```

### `Float16Array` y `Math.f16round` (ES2025)

Números decimales de 16 bits: la mitad de memoria que `Float32Array`. Muy usados en **gráficos (WebGPU)** y **modelos de IA**, donde importa más el tamaño que la precisión.

```js
const pesos = new Float16Array([0.1, 0.5, 1.0]);
pesos[0];              // 0.0999755859375 (menos precisión)
Math.f16round(0.1);    // 0.0999755859375
```

> **Ideas clave**: `ArrayBuffer` es memoria; los TypedArrays son vistas con tipo; `TextEncoder`/`TextDecoder` convierten texto ↔ bytes.

## 52. ⭐ Base64 y hexadecimal en `Uint8Array` (ES2026)

Convertir bytes a **Base64** o **hexadecimal** (y al revés) era sorprendentemente incómodo. `btoa`/`atob` solo funcionan con texto latino y con strings, no con bytes.

ES2026 añade métodos directos:

```js
const bytes = new TextEncoder().encode("¡Hola, Bilbao! 👋");

// Bytes → Base64
const b64 = bytes.toBase64();
// "wqFIb2xhLCBCaWxiYW8hIPCfkYs="

// Base64 → bytes
const deVuelta = Uint8Array.fromBase64(b64);
new TextDecoder().decode(deVuelta); // "¡Hola, Bilbao! 👋"

// Bytes → hexadecimal
new Uint8Array([255, 0, 128]).toHex(); // "ff0080"

// Hexadecimal → bytes
Uint8Array.fromHex("cafe"); // Uint8Array [202, 254]
```

### Opciones

```js
// Base64 "URL-safe" (usa - y _ en vez de + y /, típico en JWT)
bytes.toBase64({ alphabet: "base64url", omitPadding: true });

// Escribir en un array ya existente (sin crear uno nuevo)
const destino = new Uint8Array(16);
const { read, written } = destino.setFromBase64("SG9sYQ==");
```

### Ejemplo práctico: hash SHA-256 en hexadecimal

```js
async function sha256(texto) {
  const datos = new TextEncoder().encode(texto);
  const hash = await crypto.subtle.digest("SHA-256", datos);
  return new Uint8Array(hash).toHex();
}

await sha256("hola");
// "b221d9dbb083a7f33428d7c2a3c3198ae925614d70210e28716ccaa7cd4ddb79"
```

> **Ideas clave**: `toBase64`, `fromBase64`, `toHex`, `fromHex`: adiós a las funciones auxiliares caseras.

## 53. Concurrencia: Web Workers, `SharedArrayBuffer` y `Atomics`

Recuerda: JS es monohilo. Para tareas pesadas que congelarían la interfaz, se usan **Workers**: hilos aparte que ejecutan JS en paralelo.

### Web Worker básico

```js
// main.js
const worker = new Worker(new URL("./calculo.js", import.meta.url), { type: "module" });

worker.postMessage({ hasta: 50_000_000 });

worker.onmessage = (evento) => {
  console.log("Resultado:", evento.data);
};
```

```js
// calculo.js (se ejecuta en otro hilo)
self.onmessage = (evento) => {
  let suma = 0;
  for (let i = 0; i < evento.data.hasta; i++) suma += i;
  self.postMessage(suma);
};
```

Mientras el worker calcula, la página sigue respondiendo.

Características:
- Los workers **no tienen acceso al DOM**.
- Se comunican con **mensajes** (`postMessage`). Los datos se **copian** (con `structuredClone`).
- Para no copiar datos grandes, se pueden **transferir**: `worker.postMessage(buffer, [buffer])`.

En Node el equivalente es `node:worker_threads`.

### `SharedArrayBuffer`: memoria compartida

Memoria que **varios hilos ven a la vez** (sin copiar):

```js
const compartido = new SharedArrayBuffer(4);
const contador = new Int32Array(compartido);
worker.postMessage(compartido);
```

⚠️ En el navegador solo está disponible si la página tiene las cabeceras de aislamiento (`Cross-Origin-Opener-Policy` y `Cross-Origin-Embedder-Policy`).

### `Atomics`: operaciones seguras entre hilos

Si dos hilos hacen `contador[0]++` a la vez, pueden pisarse. `Atomics` garantiza que la operación es indivisible:

```js
Atomics.add(contador, 0, 1);   // suma 1 de forma segura
Atomics.load(contador, 0);     // lee de forma segura
Atomics.wait(contador, 0, 0);  // (en workers) espera hasta que cambie
Atomics.notify(contador, 0);   // despierta a quien espera
Atomics.waitAsync(contador, 0, 0); // versión con promesa (ES2024)
```

> En ES2027 llega `Atomics.pause()`, una pista al procesador para esperas activas muy cortas.

> **Ideas clave**: Workers para no congelar la UI; mensajes para comunicarse; `SharedArrayBuffer` + `Atomics` para memoria compartida.

## 🏋️ Ejercicios — Nivel 6 — Errores, módulos y datos binarios

> 🟢 fácil · 🟡 medio · 🔴 difícil. Intenta cada ejercicio antes de abrir la solución.


### 6.1 🟢 Errores personalizados (cap. 46, 47)
Crea una jerarquía `ErrorApp` → `ErrorValidacion` (con `campo`) y `ErrorRed` (con `estado` HTTP). Escribe una función `describirError(e)` que devuelva un mensaje distinto para cada tipo y que funcione incluso si `e` no es un error (por ejemplo, un string lanzado). Usa `Error.isError`.

<details><summary>Solución</summary>

```js
class ErrorApp extends Error {
  constructor(mensaje, opciones) {
    super(mensaje, opciones);
    this.name = this.constructor.name;
  }
}

class ErrorValidacion extends ErrorApp {
  constructor(campo, mensaje) {
    super(mensaje);
    this.campo = campo;
  }
}

class ErrorRed extends ErrorApp {
  constructor(estado, opciones) {
    super(`Error de red (HTTP ${estado})`, opciones);
    this.estado = estado;
  }
}

function describirError(e) {
  if (!Error.isError(e)) return `Valor lanzado que no es un error: ${String(e)}`;
  if (e instanceof ErrorValidacion) return `Revisa el campo "${e.campo}": ${e.message}`;
  if (e instanceof ErrorRed) return e.estado >= 500 ? "El servidor falla" : "Petición incorrecta";
  return `Error inesperado: ${e.message}`;
}

describirError(new ErrorValidacion("email", "formato incorrecto"));
describirError(new ErrorRed(503));
describirError("ups");
```
</details>

### 6.2 🟡 Organizar en módulos (cap. 48, 49)
Reorganiza la clase `CuentaBancaria` (ejercicio 3.2) en módulos:
- `errores.js` exporta los errores.
- `cuenta.js` exporta la clase por defecto.
- `config.json` con `{ "moneda": "EUR", "limiteRetirada": 600 }`, importado con import attributes y usado para limitar `retirar`.
- `main.js` lo usa todo.

Ejecuta `main.js` con Node.

<details><summary>Solución</summary>

```js
// errores.js
export class SaldoInsuficiente extends RangeError {}
export class LimiteSuperado extends RangeError {}
```

```json
// config.json
{ "moneda": "EUR", "limiteRetirada": 600 }
```

```js
// cuenta.js
import config from "./config.json" with { type: "json" };
import { SaldoInsuficiente, LimiteSuperado } from "./errores.js";

export default class CuentaBancaria {
  #saldo = 0;
  constructor(titular) { this.titular = titular; }
  get saldo() { return `${this.#saldo} ${config.moneda}`; }
  ingresar(c) { this.#saldo += c; return this; }
  retirar(c) {
    if (c > config.limiteRetirada) throw new LimiteSuperado(`Máximo ${config.limiteRetirada}`);
    if (c > this.#saldo) throw new SaldoInsuficiente("Saldo insuficiente");
    this.#saldo -= c;
    return this;
  }
}
```

```js
// main.js
import CuentaBancaria from "./cuenta.js";
import { LimiteSuperado } from "./errores.js";

const cuenta = new CuentaBancaria("Ana").ingresar(1000);
try {
  cuenta.retirar(700);
} catch (e) {
  if (e instanceof LimiteSuperado) console.log("Límite:", e.message);
}
console.log(cuenta.saldo); // "1000 EUR"
```

```bash
# Ejecuta el programa principal (el package.json debe tener "type": "module")
node main.js
```
</details>

### 6.3 🟡 Validar con expresiones regulares (cap. 50)
Escribe funciones que validen:
a) Un DNI español (8 dígitos + letra) **y** que la letra sea correcta (la letra es `"TRWAGMYFPDXBNJZSQVHLCKE"[número % 23]`).
b) Una matrícula española moderna (`1234 BCD`, sin vocales).
c) Extrae con grupos con nombre el día, mes y año de fechas `dd/mm/aaaa` dentro de un texto largo, usando `matchAll`.

<details><summary>Solución</summary>

```js
// a
function dniValido(dni) {
  const m = /^(?<num>\d{8})(?<letra>[A-Z])$/i.exec(dni.trim());
  if (!m) return false;
  const { num, letra } = m.groups;
  return "TRWAGMYFPDXBNJZSQVHLCKE"[Number(num) % 23] === letra.toUpperCase();
}
dniValido("12345678Z"); // true

// b
const matriculaValida = m => /^\d{4} ?[BCDFGHJKLMNPRSTVWXYZ]{3}$/i.test(m);
matriculaValida("1234 BCD"); // true
matriculaValida("1234 ABC"); // false (lleva vocal)

// c
const texto = "Exámenes: 15/12/2026 y recuperación 12/01/2027.";
for (const { groups } of texto.matchAll(/(?<dia>\d{2})\/(?<mes>\d{2})\/(?<año>\d{4})/g)) {
  console.log(groups.dia, groups.mes, groups.año);
}
```
</details>

### 6.4 🟡 Buscador seguro (cap. 50)
Escribe `resaltar(texto, busqueda)` que envuelva cada aparición de `busqueda` (sin distinguir mayúsculas) en `<mark>…</mark>`. Debe funcionar aunque la búsqueda contenga caracteres especiales como `(`, `+` o `.`.

<details><summary>Solución</summary>

```js
function resaltar(texto, busqueda) {
  if (!busqueda) return texto;
  const patron = new RegExp(RegExp.escape(busqueda), "gi");
  return texto.replace(patron, coincidencia => `<mark>${coincidencia}</mark>`);
}

resaltar("Precio (IVA incl.): 10€. precio (iva incl.)", "precio (iva");
// "<mark>Precio (IVA</mark> incl.): 10€. <mark>precio (iva</mark> incl.)"
```

⚠️ Si el texto viene del usuario y vas a meter el resultado en `innerHTML`, escapa antes el propio texto para evitar XSS (cap. 64).
</details>

### 6.5 🟡 Bytes, Base64 y hash (cap. 51, 52)
a) Convierte el texto `"Kaixo, mundua! 🌍"` a bytes, muestra cuántos bytes ocupa y por qué no coincide con `.length`.
b) Pásalo a Base64 y a hexadecimal, y recupera el texto original desde Base64.
c) Calcula su hash SHA-256 en hexadecimal.

<details><summary>Solución</summary>

```js
const texto = "Kaixo, mundua! 🌍";

// a
const bytes = new TextEncoder().encode(texto);
console.log(texto.length, bytes.length); // 17 y 19
// El emoji ocupa 2 "unidades" en el string (length) pero 4 bytes en UTF-8.

// b
const b64 = bytes.toBase64();
const hex = bytes.toHex();
const recuperado = new TextDecoder().decode(Uint8Array.fromBase64(b64));
console.log(recuperado === texto); // true

// c
const hash = await crypto.subtle.digest("SHA-256", bytes);
console.log(new Uint8Array(hash).toHex());
```
</details>

### 6.6 🔴 Cálculo en un Worker (cap. 53)
Crea una página con un botón "Calcular primos" que cuente los primos menores que 5 000 000 en un **Web Worker**, y un contador que se actualice cada 100 ms para demostrar que la página no se congela.

<details><summary>Solución</summary>

```html
<!-- index.html -->
<button id="calcular">Calcular primos</button>
<p>Contador: <span id="contador">0</span></p>
<p id="resultado"></p>
<script type="module">
  let n = 0;
  setInterval(() => (document.querySelector("#contador").textContent = ++n), 100);

  const worker = new Worker(new URL("./primos-worker.js", import.meta.url), { type: "module" });

  document.querySelector("#calcular").addEventListener("click", () => {
    document.querySelector("#resultado").textContent = "Calculando…";
    worker.postMessage(5_000_000);
  });

  worker.onmessage = (e) => {
    document.querySelector("#resultado").textContent = `Hay ${e.data} primos`;
  };
</script>
```

```js
// primos-worker.js
self.onmessage = ({ data: limite }) => {
  // Criba de Eratóstenes
  const esCompuesto = new Uint8Array(limite);
  let cuenta = 0;
  for (let i = 2; i < limite; i++) {
    if (esCompuesto[i]) continue;
    cuenta++;
    for (let j = i * i; j < limite; j += i) esCompuesto[j] = 1;
  }
  self.postMessage(cuenta);
};
```

Ábrelo con un servidor local (los workers no funcionan abriendo el archivo directamente):

```bash
# Sirve la carpeta actual en http://localhost:3000 sin instalar nada de forma permanente
npx serve .
```
</details>


---

# NIVEL 7 — Lo que llega en ES2027 (y ya se puede usar)

Estas funcionalidades ya están **terminadas** (Stage 4) y empiezan a estar disponibles en navegadores y Node, pero entrarán oficialmente en la edición **ES2027** (junio de 2027).

## 54. Temporal: fechas y horas por fin bien hechas

El objeto `Date` (de 1995) tiene muchos problemas:

```js
new Date(2026, 0, 31);  // los meses empiezan en 0 😱 (0 = enero)

const d = new Date("2026-01-31");
d.setMonth(1);          // "31 de febrero" → salta a 3 de marzo 😱

new Date("2026-04-13"); // medianoche UTC
new Date("04/13/2026"); // medianoche hora local 😱 (inconsistente)

// Además es mutable: cualquier función puede cambiarte la fecha
```

**Temporal** es una API nueva, completa e **inmutable** que lo resuelve. Tiene un tipo para cada necesidad:

| Tipo | Representa | Ejemplo |
|---|---|---|
| `Temporal.PlainDate` | Una fecha de calendario | Un cumpleaños: 2026-11-19 |
| `Temporal.PlainTime` | Una hora de reloj | Hora de entrada: 08:30 |
| `Temporal.PlainDateTime` | Fecha + hora, sin zona | Un evento "local" |
| `Temporal.ZonedDateTime` | Fecha + hora + zona horaria | Una reunión en Madrid y Nueva York |
| `Temporal.Instant` | Un instante exacto (UTC) | Un registro de log |
| `Temporal.Duration` | Una duración | 2 horas y 30 minutos |
| `Temporal.PlainYearMonth` / `PlainMonthDay` | Año-mes / mes-día | Una nómina / una fiesta anual |
| `Temporal.Now` | El momento actual | |

### Fechas de calendario

```js
const hoy = Temporal.Now.plainDateISO();
const examen = Temporal.PlainDate.from("2026-12-15");

examen.month;     // 12 (¡los meses empiezan en 1!)
examen.dayOfWeek; // 2 (martes; lunes = 1)

// Inmutable: add devuelve una fecha NUEVA
const recuperacion = examen.add({ weeks: 2 });

// Diferencia entre fechas
const falta = hoy.until(examen, { largestUnit: "day" });
console.log(`Quedan ${falta.days} días`);

// Comparar
Temporal.PlainDate.compare(hoy, examen); // -1, 0 o 1
hoy.equals(examen);                      // false
```

### Sumar meses sin sorpresas

```js
Temporal.PlainDate.from("2026-01-31").add({ months: 1 });
// 2026-02-28 ✅ (se ajusta al último día del mes)
```

### Zonas horarias

```js
const reunion = Temporal.ZonedDateTime.from(
  "2026-11-20T10:00[Europe/Madrid]"
);

reunion.withTimeZone("America/New_York").toString();
// "2026-11-20T04:00:00-05:00[America/New_York]"

// Los cambios de horario de verano se gestionan solos
```

### Duraciones

```js
const clase = Temporal.Duration.from({ minutes: 55 });

// Tres clases seguidas (las duraciones se suman con add)
const total = clase.add(clase).add(clase);       // PT165M
total.round({ largestUnit: "hour" }).toString(); // "PT2H45M"

// Duración entre dos horas
const entrada = Temporal.PlainTime.from("08:30");
const salida = Temporal.PlainTime.from("14:25");
entrada.until(salida).toString(); // "PT5H55M"
```

### Formatear

```js
examen.toLocaleString("es-ES", { dateStyle: "full" });
// "martes, 15 de diciembre de 2026"
```

### Compatibilidad

Temporal ya está llegando a los navegadores y Node. Mientras tanto puedes usar el polyfill:

```bash
# Instala el polyfill oficial de Temporal en tu proyecto
npm install @js-temporal/polyfill
```

```js
import { Temporal } from "@js-temporal/polyfill";
```

> **Ideas clave**: Temporal sustituye a `Date`. Es inmutable, los meses empiezan en 1 y cada tipo representa un concepto distinto.

## 55. Gestión explícita de recursos: `using` y `await using`

Muchos recursos hay que **cerrarlos** al terminar: archivos, conexiones a bases de datos, locks… Si se te olvida o salta un error a mitad, quedan abiertos.

### Antes: `try / finally`

```js
const archivo = await abrir("datos.txt");
try {
  await procesar(archivo);
} finally {
  await archivo.close(); // hay que acordarse siempre
}
```

### Con `using`

```js
{
  await using archivo = await abrir("datos.txt");
  await procesar(archivo);
} // ← al salir del bloque, se cierra SOLO, aunque haya un error
```

- `using` → para recursos con limpieza **síncrona** (`[Symbol.dispose]()`).
- `await using` → para limpieza **asíncrona** (`[Symbol.asyncDispose]()`).

### Hacer tus objetos "desechables"

```js
class Conexion {
  constructor(nombre) {
    this.nombre = nombre;
    console.log(`Abriendo ${nombre}`);
  }

  [Symbol.dispose]() {
    console.log(`Cerrando ${this.nombre}`);
  }
}

function trabajar() {
  using a = new Conexion("BD");
  using b = new Conexion("Caché");
  console.log("Trabajando...");
}

trabajar();
// Abriendo BD
// Abriendo Caché
// Trabajando...
// Cerrando Caché   ← en orden inverso, como una pila
// Cerrando BD
```

### `DisposableStack`

Para agrupar varias limpiezas, o recursos que no tienen `Symbol.dispose`:

```js
function preparar() {
  using pila = new DisposableStack();
  const timer = setInterval(tick, 1000);
  pila.defer(() => clearInterval(timer)); // registra una limpieza
  // ...
} // se ejecutan todas las limpiezas registradas
```

También existe `AsyncDisposableStack`.

> 💡 **Compatibilidad**: soportado en versiones recientes de Chrome, Node y TypeScript (5.2+). Comprueba en MDN antes de usarlo en producción.

> **Ideas clave**: `using` cierra recursos automáticamente al salir del bloque. Implementa `[Symbol.dispose]` en tus clases.

## 56. Cómo comprobar la compatibilidad

No todas las novedades funcionan en todas partes. Antes de usar algo nuevo:

### 1. Consulta MDN

Cada página de MDN Web Docs tiene al final una tabla de **compatibilidad con navegadores** (y Node).

### 2. caniuse.com

Escribe la funcionalidad (por ejemplo, "Iterator helpers") y verás qué porcentaje de usuarios la soporta.

### 3. Detecta la funcionalidad en el código

```js
if (typeof Map.prototype.getOrInsert === "function") {
  mapa.getOrInsert(clave, []);
} else {
  if (!mapa.has(clave)) mapa.set(clave, []);
}

const tieneTemporal = typeof globalThis.Temporal !== "undefined";
```

### 4. Usa polyfills

Un **polyfill** es código que implementa una funcionalidad nueva en entornos antiguos.

```bash
# core-js: polyfills de casi todas las novedades del estándar
npm install core-js
```

```js
// Importa solo lo que necesites
import "core-js/actual/math/sum-precise";
import "core-js/actual/iterator";
```

### 5. Transpila (para sintaxis nueva)

Los polyfills sirven para **funciones** nuevas. Para **sintaxis** nueva (como `using` o decoradores) necesitas un transpilador como **TypeScript**, **Babel** o **esbuild**, que reescriba el código a una versión más antigua.

### 6. Baseline

En MDN verás la etiqueta **Baseline**: indica que la funcionalidad funciona en todos los navegadores principales. *Baseline "Widely available"* significa que lleva al menos 30 meses en todos ellos: es la más segura.

> **Ideas clave**: MDN + caniuse para consultar; detección de funcionalidad + polyfills para usar novedades con seguridad.

## 🏋️ Ejercicios — Nivel 7 — ES2027: Temporal y `using`

> 🟢 fácil · 🟡 medio · 🔴 difícil. Intenta cada ejercicio antes de abrir la solución.


### 7.1 🟡 Calendario escolar con Temporal (cap. 54)
Usando Temporal (o su polyfill):
a) ¿Cuántos días faltan desde hoy hasta el 23 de diciembre de 2026?
b) ¿Qué día de la semana cae el 1 de enero de 2027? Muéstralo en español.
c) Una evaluación dura 12 semanas desde el 8 de enero de 2027. ¿Qué fecha termina?
d) Una videollamada es el 20/11/2026 a las 17:00 en Madrid. ¿Qué hora es en Ciudad de México y en Tokio?

<details><summary>Solución</summary>

```js
// Si tu entorno no tiene Temporal:
// import { Temporal } from "@js-temporal/polyfill";

// a
const hoy = Temporal.Now.plainDateISO();
const vacaciones = Temporal.PlainDate.from("2026-12-23");
console.log(hoy.until(vacaciones).days, "días");

// b
const añoNuevo = Temporal.PlainDate.from("2027-01-01");
añoNuevo.toLocaleString("es-ES", { weekday: "long" }); // "viernes"

// c
Temporal.PlainDate.from("2027-01-08").add({ weeks: 12 }).toString(); // "2027-04-02"

// d
const llamada = Temporal.ZonedDateTime.from("2026-11-20T17:00[Europe/Madrid]");
llamada.withTimeZone("America/Mexico_City").toPlainTime().toString(); // "10:00:00"
llamada.withTimeZone("Asia/Tokyo").toPlainTime().toString();          // "01:00:00" (del día 21)
```
</details>

### 7.2 🟡 Recursos desechables (cap. 55)
Crea una clase `Temporizador` que mida el tiempo de un bloque y lo muestre automáticamente al salir de él usando `using`:

```js
{
  using t = new Temporizador("Ordenar");
  // ...código a medir
} // → "Ordenar: 12.3 ms"
```

<details><summary>Solución</summary>

```js
class Temporizador {
  #inicio = performance.now();

  constructor(etiqueta) {
    this.etiqueta = etiqueta;
  }

  [Symbol.dispose]() {
    const ms = performance.now() - this.#inicio;
    console.log(`${this.etiqueta}: ${ms.toFixed(1)} ms`);
  }
}

{
  using t = new Temporizador("Ordenar");
  Array.from({ length: 1e6 }, Math.random).toSorted();
}
```

Si tu entorno no soporta `using`, el equivalente es:

```js
const t = new Temporizador("Ordenar");
try {
  // ...
} finally {
  t[Symbol.dispose]();
}
```
</details>


---

# NIVEL 8 — JavaScript profesional

## 57. El DOM, los eventos y las Web APIs

El **DOM** (Document Object Model) es la representación del HTML como un árbol de objetos que JS puede leer y modificar.

### Seleccionar elementos

```js
const titulo = document.querySelector("h1");          // el primero que coincida
const botones = document.querySelectorAll(".btn");    // todos (NodeList)
const form = document.getElementById("formulario");

botones.forEach(b => console.log(b.textContent));
```

### Modificar

```js
titulo.textContent = "Nuevo título";           // texto (seguro)
titulo.classList.add("destacado");             // clases CSS
titulo.classList.toggle("oculto");
titulo.style.color = "tomato";                 // estilos en línea
titulo.dataset.id = "42";                      // atributo data-id="42"
titulo.setAttribute("aria-label", "Título");
```

### Crear y eliminar

```js
const li = document.createElement("li");
li.textContent = "Nuevo elemento";
document.querySelector("ul").append(li);

li.remove();
```

Para muchos elementos, construye primero y añade al final (más rápido):

```js
const fragmento = document.createDocumentFragment();
for (const nombre of ["Ana", "Luis", "Eva"]) {
  const li = document.createElement("li");
  li.textContent = nombre;
  fragmento.append(li);
}
lista.append(fragmento);
```

### Eventos

```js
const boton = document.querySelector("#guardar");

boton.addEventListener("click", (evento) => {
  console.log("Clic en", evento.target);
});

form.addEventListener("submit", (e) => {
  e.preventDefault();                    // evita que la página se recargue
  const datos = new FormData(form);
  const objeto = Object.fromEntries(datos);
  console.log(objeto);
});
```

### Delegación de eventos

En vez de poner un listener en cada elemento, pon **uno solo en el padre**:

```js
document.querySelector("#lista").addEventListener("click", (e) => {
  const boton = e.target.closest("button[data-borrar]");
  if (!boton) return;
  boton.closest("li").remove();
});
```

Ventajas: menos memoria y funciona con elementos añadidos después.

### `fetch`: hablar con servidores

```js
// GET
const r = await fetch("/api/alumnos");
const alumnos = await r.json();

// POST con JSON
await fetch("/api/alumnos", {
  method: "POST",
  headers: { "Content-Type": "application/json" },
  body: JSON.stringify({ nombre: "Ana", curso: "1º" }),
});
```

### Otras Web APIs útiles

```js
// Guardar datos en el navegador
localStorage.setItem("tema", "oscuro");
localStorage.getItem("tema");

// Copiar al portapapeles
await navigator.clipboard.writeText("Texto copiado");

// Observar cuándo un elemento entra en pantalla (lazy loading, animaciones)
const observador = new IntersectionObserver((entradas) => {
  for (const e of entradas) {
    if (e.isIntersecting) e.target.classList.add("visible");
  }
});
document.querySelectorAll(".animar").forEach(el => observador.observe(el));

// Generar IDs únicos
crypto.randomUUID(); // "3b241101-e2bb-4255-8caf-4136c566a962"

// URLs
const url = new URL("https://ejemplo.com/buscar?q=js&page=2");
url.searchParams.get("q"); // "js"
```

> **Ideas clave**: `querySelector`, `addEventListener`, delegación de eventos y `fetch` cubren el 90 % del trabajo con el DOM.

## 58. Node.js moderno

### Iniciar un proyecto

```bash
# Crea un package.json con valores por defecto (-y responde "sí" a todo)
npm init -y
```

En `package.json`, añade `"type": "module"` para usar `import`/`export`.

### Módulos nativos (con prefijo `node:`)

```js
import { readFile, writeFile, mkdir } from "node:fs/promises";
import path from "node:path";

const texto = await readFile("entrada.txt", "utf-8");
await mkdir("salida", { recursive: true });
await writeFile(path.join("salida", "resultado.txt"), texto.toUpperCase());
```

El prefijo `node:` deja claro que es un módulo del sistema y no un paquete de npm.

### Un servidor HTTP mínimo

```js
import { createServer } from "node:http";

const servidor = createServer((req, res) => {
  res.writeHead(200, { "Content-Type": "application/json; charset=utf-8" });
  res.end(JSON.stringify({ mensaje: "Hola desde Node" }));
});

servidor.listen(3000, () => console.log("Escuchando en http://localhost:3000"));
```

### Funcionalidades integradas en Node moderno

```bash
# Ejecuta app.js y lo reinicia automáticamente al guardar cambios (sustituye a nodemon)
node --watch app.js

# Carga las variables del archivo .env en process.env (sustituye a dotenv)
node --env-file=.env app.js

# Ejecuta los tests del proyecto con el test runner integrado
node --test
```

- `fetch` está disponible de forma global (sin instalar nada).
- `process.loadEnvFile()` carga un `.env` desde el código.
- Node ejecuta archivos **TypeScript** sencillos directamente (eliminando los tipos), en versiones recientes.

### Argumentos de línea de comandos

```js
import { parseArgs } from "node:util";

const { values } = parseArgs({
  options: {
    nombre: { type: "string", short: "n" },
    verbose: { type: "boolean", short: "v" },
  },
});

console.log(`Hola, ${values.nombre}`);
```

```bash
# Ejecuta saludo.js pasándole el argumento --nombre con el valor Ana
node saludo.js --nombre Ana
```

> **Ideas clave**: `"type": "module"`, prefijo `node:`, `fs/promises`. Node ya trae `--watch`, `--env-file`, `fetch` y test runner.

## 59. Herramientas: npm, Vite, ESLint y Prettier

### npm: el gestor de paquetes

```bash
# Instala una librería que tu app necesita para funcionar (va a "dependencies")
npm install zod

# Instala una herramienta que solo se usa al desarrollar (va a "devDependencies")
npm install -D vitest

# Instala todo lo que aparece en package.json (al clonar un proyecto)
npm install

# Ejecuta el script llamado "dev" definido en package.json
npm run dev

# Ejecuta una herramienta sin instalarla de forma permanente
npx serve .
```

- `package.json`: lista de dependencias y scripts.
- `package-lock.json`: versiones exactas instaladas. **Súbelo a Git.**
- `node_modules/`: las librerías descargadas. **Nunca lo subas a Git** (añádelo a `.gitignore`).

Alternativas a npm: **pnpm** (más rápido y ahorra disco) y **yarn**.

### Versionado semántico

`"zod": "^3.23.8"` → `MAYOR.MENOR.PARCHE`

- **MAYOR**: cambios que rompen compatibilidad.
- **MENOR**: funcionalidades nuevas compatibles.
- **PARCHE**: correcciones.
- `^` permite actualizar MENOR y PARCHE; `~` solo PARCHE.

### Vite: entorno de desarrollo web

```bash
# Crea un proyecto nuevo con Vite (te pregunta el nombre y la plantilla: vanilla, React, Vue…)
npm create vite@latest mi-proyecto

# Entra en la carpeta del proyecto
cd mi-proyecto

# Instala las dependencias del proyecto
npm install

# Arranca el servidor de desarrollo con recarga instantánea
npm run dev

# Genera la versión optimizada para producción en la carpeta dist/
npm run build
```

### ESLint: detecta errores y malas prácticas

```bash
# Crea la configuración de ESLint de forma guiada
npm init @eslint/config@latest

# Revisa todos los archivos del proyecto y muestra los problemas encontrados
npx eslint .
```

### Prettier: formatea el código automáticamente

```bash
# Instala Prettier como herramienta de desarrollo
npm install -D prettier

# Formatea todos los archivos del proyecto y guarda los cambios
npx prettier . --write
```

Consejo: instala las extensiones de ESLint y Prettier en VS Code y activa "formatear al guardar".

> **Ideas clave**: `npm install -D` para herramientas, Vite para proyectos web, ESLint para calidad y Prettier para formato.

## 60. Testing

Los **tests** son código que comprueba que tu código funciona. Te permiten cambiar cosas sin miedo a romper otras.

### Con el test runner de Node (sin instalar nada)

```js
// suma.js
export const sumar = (a, b) => a + b;
```

```js
// suma.test.js
import { test, describe } from "node:test";
import assert from "node:assert/strict";
import { sumar } from "./suma.js";

describe("sumar", () => {
  test("suma dos positivos", () => {
    assert.equal(sumar(2, 3), 5);
  });

  test("funciona con negativos", () => {
    assert.equal(sumar(-2, -3), -5);
  });
});
```

```bash
# Busca y ejecuta todos los archivos de test (*.test.js) del proyecto
node --test
```

### Con Vitest (el más usado en proyectos con Vite)

```bash
# Instala Vitest como herramienta de desarrollo
npm install -D vitest

# Ejecuta los tests y los repite automáticamente al guardar cambios
npx vitest
```

```js
import { describe, it, expect } from "vitest";
import { sumar } from "./suma.js";

describe("sumar", () => {
  it("suma dos números", () => {
    expect(sumar(2, 3)).toBe(5);
  });

  it("compara objetos por contenido", () => {
    expect({ a: 1, b: [2] }).toEqual({ a: 1, b: [2] });
  });

  it("detecta errores", () => {
    expect(() => dividir(1, 0)).toThrow(RangeError);
  });

  it("funciona con async", async () => {
    await expect(cargarDatos()).resolves.toHaveLength(3);
  });
});
```

### Tipos de tests

- **Unitarios**: prueban una función aislada. Rápidos y muchos.
- **De integración**: prueban varias piezas juntas.
- **End-to-end (E2E)**: prueban la app completa como un usuario (con **Playwright**).

### Patrón AAA

```js
test("aplica descuento del 10 %", () => {
  // Arrange (preparar)
  const carrito = new Carrito([{ precio: 100 }]);
  // Act (actuar)
  carrito.aplicarDescuento(10);
  // Assert (comprobar)
  assert.equal(carrito.total(), 90);
});
```

> **Ideas clave**: `node --test` para empezar, Vitest para proyectos web. Prepara, actúa, comprueba.

## 61. TypeScript: el siguiente paso

**TypeScript** es JavaScript con **tipos**. Detecta errores antes de ejecutar el código y mejora muchísimo el autocompletado.

```ts
interface Alumno {
  nombre: string;
  edad: number;
  email?: string;            // opcional
}

function saludar(alumno: Alumno): string {
  return `Hola, ${alumno.nombre}`;
}

saludar({ nombre: "Ana", edad: 17 });   // ✅
saludar({ nombre: "Ana" });             // ❌ error: falta "edad"
```

Lo más útil para empezar:

```ts
// Uniones: uno de varios valores
type Estado = "pendiente" | "aprobado" | "suspenso";

// Genéricos: funciones que trabajan con cualquier tipo
function primero<T>(lista: T[]): T | undefined {
  return lista[0];
}

// Inferencia: muchas veces no hace falta escribir el tipo
const notas = [8, 9, 7]; // TypeScript sabe que es number[]
```

Todo lo de esta guía es válido en TypeScript: TS es un **superconjunto** de JS.

```bash
# Instala el compilador de TypeScript en el proyecto
npm install -D typescript

# Crea el archivo de configuración tsconfig.json
npx tsc --init

# Comprueba los tipos de todo el proyecto sin generar archivos
npx tsc --noEmit
```

> **Ideas clave**: TypeScript = JS + tipos. Es el estándar en proyectos profesionales (Angular lo usa por defecto).

## 62. Rendimiento y memoria

### Medir antes de optimizar

```js
performance.mark("inicio");
operacionPesada();
performance.mark("fin");
performance.measure("operación", "inicio", "fin");
console.log(performance.getEntriesByName("operación")[0].duration, "ms");
```

En DevTools, la pestaña **Performance** graba lo que ocurre y muestra qué funciones tardan más.

### El recolector de basura (garbage collector)

JS libera memoria automáticamente cuando un objeto **ya no es alcanzable** desde ninguna variable. Una **fuga de memoria** ocurre cuando mantienes referencias sin querer:

```js
// ❌ Fugas típicas
const cache = {};                       // crece sin límite
setInterval(() => { /* ... */ }, 1000); // nunca se limpia
elemento.addEventListener("scroll", fn); // el elemento se borra pero el listener sigue

// ✅ Soluciones
const cache2 = new Map(); // con límite de tamaño, o WeakMap
const id = setInterval(tick, 1000); clearInterval(id);
el.addEventListener("scroll", fn, { signal: controlador.signal });
```

En DevTools, la pestaña **Memory** permite hacer "heap snapshots" y comparar.

### Técnicas habituales

**Debounce**: ejecutar solo cuando el usuario deja de escribir.

```js
function debounce(fn, ms) {
  let id;
  return (...args) => {
    clearTimeout(id);
    id = setTimeout(() => fn(...args), ms);
  };
}

buscador.addEventListener("input", debounce(e => buscar(e.target.value), 300));
```

**Throttle**: ejecutar como máximo una vez cada X ms (scroll, resize).

```js
function throttle(fn, ms) {
  let ultimo = 0;
  return (...args) => {
    const ahora = Date.now();
    if (ahora - ultimo >= ms) {
      ultimo = ahora;
      fn(...args);
    }
  };
}
```

**Otras**:
- Usa `Map`/`Set` para búsquedas frecuentes (`has` es mucho más rápido que `includes` en arrays grandes).
- Carga código bajo demanda con `import()`.
- Mueve cálculos pesados a un Worker.
- Agrupa cambios en el DOM (fragmentos, `requestAnimationFrame`).

> **Ideas clave**: mide primero. Evita fugas limpiando timers y listeners. Debounce para inputs, throttle para scroll.

## 63. Patrones y programación funcional

### Funciones puras

Una función **pura** siempre devuelve lo mismo con los mismos argumentos y **no modifica nada de fuera**.

```js
// ❌ Impura: modifica el array original
function añadir(lista, x) {
  lista.push(x);
  return lista;
}

// ✅ Pura
const añadirPuro = (lista, x) => [...lista, x];
```

Son fáciles de testear, de razonar y de reutilizar.

### Inmutabilidad

No modifiques datos: crea copias nuevas. Herramientas que ya conoces: spread, `toSorted`, `with`, `structuredClone`, `Object.freeze`.

### Composición

Construir funciones complejas uniendo funciones sencillas:

```js
const pipe = (...fns) => (valor) => fns.reduce((acc, fn) => fn(acc), valor);

const limpiar = s => s.trim();
const minusculas = s => s.toLowerCase();
const sinAcentos = s => s.normalize("NFD").replace(/\p{Diacritic}/gu, "");
const aSlug = s => s.replace(/\s+/g, "-");

const crearSlug = pipe(limpiar, minusculas, sinAcentos, aSlug);
crearSlug("  Programación en JavaScript "); // "programacion-en-javascript"
```

### Currying

Transformar `f(a, b)` en `f(a)(b)`:

```js
const filtrarPor = campo => valor => lista => lista.filter(x => x[campo] === valor);
const deBilbao = filtrarPor("ciudad")("Bilbao");
deBilbao(personas);
```

### Patrones de diseño frecuentes en JS

**Módulo** (encapsular con módulos ES o closures): ya lo has visto.

**Observer / Pub-Sub**: avisar a varios "suscriptores" cuando pasa algo.

```js
class Emisor {
  #oyentes = new Map();

  on(evento, fn) {
    if (!this.#oyentes.has(evento)) this.#oyentes.set(evento, []);
    this.#oyentes.get(evento).push(fn);
    // Con ES2026 bastaría: this.#oyentes.getOrInsert(evento, []).push(fn);
    return () => this.off(evento, fn); // devuelve una función para desuscribirse
  }

  off(evento, fn) {
    const lista = this.#oyentes.get(evento) ?? [];
    this.#oyentes.set(evento, lista.filter(f => f !== fn));
  }

  emit(evento, datos) {
    for (const fn of this.#oyentes.get(evento) ?? []) fn(datos);
  }
}

const tienda = new Emisor();
const cancelar = tienda.on("compra", p => console.log("Comprado:", p));
tienda.emit("compra", "Teclado");
cancelar();
```

`EventTarget` (nativo) hace algo parecido en navegador y Node.

**Factory**: funciones que crean objetos (como `crearCuenta` del cap. 15).

**Singleton**: con módulos ES es automático: un módulo se ejecuta una sola vez, así que lo que exporta es único.

> **Ideas clave**: funciones puras + inmutabilidad + composición = código predecible y fácil de testear.

## 64. Seguridad

### XSS (Cross-Site Scripting)

Ocurre cuando insertas texto del usuario como **HTML**:

```js
const comentario = '<img src=x onerror="robarCookies()">';

elemento.innerHTML = comentario;   // ❌ ejecuta el código malicioso
elemento.textContent = comentario; // ✅ lo muestra como texto
```

Reglas:
- Usa `textContent` siempre que sea posible.
- Si necesitas HTML de usuarios, límpialo con una librería como **DOMPurify**.
- Los frameworks (React, Angular, Vue) escapan el texto por defecto: no te saltes esa protección (`dangerouslySetInnerHTML`, `bypassSecurityTrust…`) sin una razón muy clara.
- Configura una **Content Security Policy (CSP)** en el servidor.

### Nunca uses `eval` ni `new Function` con datos externos

```js
eval(textoDelUsuario); // ❌ ejecuta cualquier código
JSON.parse(texto);     // ✅ para leer datos
```

### Prototype pollution

Si fusionas objetos que vienen del exterior sin cuidado, alguien puede modificar `Object.prototype` y afectar a toda la aplicación:

```js
const malicioso = JSON.parse('{"__proto__": {"esAdmin": true}}');

function fusionarMal(destino, origen) {
  for (const clave in origen) {
    if (typeof origen[clave] === "object") {
      destino[clave] ??= {};
      fusionarMal(destino[clave], origen[clave]);
    } else {
      destino[clave] = origen[clave];
    }
  }
}

fusionarMal({}, malicioso);
({}).esAdmin; // true 😱 ¡todos los objetos son admin!
```

Defensas:
- Ignora las claves `__proto__`, `constructor` y `prototype` al fusionar.
- Usa `Map` para datos con claves externas, u objetos sin prototipo: `Object.create(null)`.
- Valida los datos de entrada con una librería como **Zod**.

### Otros consejos

- **No guardes secretos** (claves de API, contraseñas) en el código del frontend: cualquiera puede verlos.
- Revisa las dependencias:

```bash
# Busca vulnerabilidades conocidas en las dependencias instaladas
npm audit
```

- Usa `crypto.getRandomValues()` o `crypto.randomUUID()` para valores aleatorios de seguridad, **nunca** `Math.random()`.

> **Ideas clave**: `textContent` en vez de `innerHTML`, nada de `eval`, valida todo lo que viene de fuera.

## 65. Proyecto final integrador: Gestor de tareas

Para consolidar todo, construye una **aplicación de tareas** que use lo aprendido. Requisitos sugeridos por niveles:

### Requisitos básicos (niveles 1–2)
- Añadir, completar y borrar tareas.
- Cada tarea: `id` (`crypto.randomUUID()`), `titulo`, `completada`, `prioridad`, `fecha`.
- Filtrar (todas / pendientes / completadas) y ordenar con `toSorted`.
- Agrupar por prioridad con `Object.groupBy`.

### Orientación a objetos (nivel 3)
- Clase `Tarea` con campos privados y validación en setters.
- Clase `GestorTareas` con métodos `añadir`, `completar`, `eliminar`, `filtrar`.

### Asincronía y persistencia (niveles 4–6)
- Guardar en `localStorage` (o en un archivo JSON con Node).
- Cargar tareas de ejemplo desde una API con `fetch`, con timeout (`AbortSignal.timeout`).
- Módulos ES: `tarea.js`, `gestor.js`, `ui.js`, `main.js`.
- Errores personalizados (`ErrorValidacion`) con `cause`.

### Interfaz (nivel 8)
- DOM con delegación de eventos.
- Buscador con `debounce`.
- Escapar todo el texto del usuario con `textContent`.

### Extras de experto
- Fechas con **Temporal**: "vence en 3 días".
- Iterator helpers para estadísticas.
- Emisor de eventos (patrón Observer) para actualizar la UI.
- Tests con `node --test` o Vitest.
- Pasarlo a TypeScript.

### Estructura propuesta

```
gestor-tareas/
├── index.html
├── package.json
├── src/
│   ├── main.js
│   ├── modelo/
│   │   ├── tarea.js
│   │   └── gestor.js
│   ├── ui/
│   │   └── vista.js
│   └── utils/
│       ├── debounce.js
│       └── errores.js
└── tests/
    └── gestor.test.js
```

### Esqueleto de partida

```js
// src/modelo/tarea.js
export class Tarea {
  #titulo;

  constructor({ titulo, prioridad = "media" }) {
    this.id = crypto.randomUUID();
    this.titulo = titulo;          // pasa por el setter
    this.prioridad = prioridad;
    this.completada = false;
    this.creada = new Date().toISOString();
  }

  get titulo() { return this.#titulo; }

  set titulo(valor) {
    const limpio = String(valor ?? "").trim();
    if (!limpio) throw new Error("El título no puede estar vacío");
    this.#titulo = limpio;
  }

  alternar() {
    this.completada = !this.completada;
  }

  toJSON() {
    return { id: this.id, titulo: this.#titulo, prioridad: this.prioridad,
             completada: this.completada, creada: this.creada };
  }
}
```

```js
// src/modelo/gestor.js
import { Tarea } from "./tarea.js";

export class GestorTareas extends EventTarget {
  #tareas = new Map();

  añadir(datos) {
    const tarea = new Tarea(datos);
    this.#tareas.set(tarea.id, tarea);
    this.#avisar();
    return tarea;
  }

  alternar(id) {
    this.#tareas.get(id)?.alternar();
    this.#avisar();
  }

  eliminar(id) {
    this.#tareas.delete(id);
    this.#avisar();
  }

  listar(filtro = "todas") {
    const todas = this.#tareas.values();
    const filtradas =
      filtro === "pendientes" ? todas.filter(t => !t.completada) :
      filtro === "completadas" ? todas.filter(t => t.completada) :
      todas;
    return filtradas.toArray().toSorted((a, b) => a.creada.localeCompare(b.creada));
  }

  estadisticas() {
    const lista = [...this.#tareas.values()];
    return {
      total: lista.length,
      completadas: lista.filter(t => t.completada).length,
      porPrioridad: Object.groupBy(lista, t => t.prioridad),
    };
  }

  #avisar() {
    this.dispatchEvent(new Event("cambio"));
  }
}
```

¡A partir de aquí, el resto lo construyes tú!

## 🏋️ Ejercicios — Nivel 8 — JavaScript profesional

> 🟢 fácil · 🟡 medio · 🔴 difícil. Intenta cada ejercicio antes de abrir la solución.


### 8.1 🟡 Lista de la compra en el DOM (cap. 57)
Crea una página con un formulario (input + botón) que añada elementos a una lista `<ul>`. Cada elemento tiene un botón "✕" para borrarlo. Requisitos: delegación de eventos (un solo listener en el `<ul>`), `textContent` (nunca `innerHTML` con datos del usuario) y guardado en `localStorage`.

<details><summary>Solución</summary>

```html
<form id="form">
  <input name="producto" placeholder="Producto" required>
  <button>Añadir</button>
</form>
<ul id="lista"></ul>

<script type="module">
  const form = document.querySelector("#form");
  const lista = document.querySelector("#lista");

  let productos = cargar();
  pintar();

  form.addEventListener("submit", (e) => {
    e.preventDefault();
    const producto = new FormData(form).get("producto").trim();
    if (!producto) return;
    productos = [...productos, { id: crypto.randomUUID(), nombre: producto }];
    guardarYPintar();
    form.reset();
  });

  lista.addEventListener("click", (e) => {
    const boton = e.target.closest("button[data-id]");
    if (!boton) return;
    productos = productos.filter(p => p.id !== boton.dataset.id);
    guardarYPintar();
  });

  function pintar() {
    lista.replaceChildren(
      ...productos.map(({ id, nombre }) => {
        const li = document.createElement("li");
        li.textContent = nombre + " ";
        const borrar = document.createElement("button");
        borrar.textContent = "✕";
        borrar.dataset.id = id;
        borrar.setAttribute("aria-label", `Borrar ${nombre}`);
        li.append(borrar);
        return li;
      })
    );
  }

  function guardarYPintar() {
    localStorage.setItem("compra", JSON.stringify(productos));
    pintar();
  }

  function cargar() {
    try {
      return JSON.parse(localStorage.getItem("compra")) ?? [];
    } catch {
      return [];
    }
  }
</script>
```
</details>

### 8.2 🟡 Script de Node: informe de notas (cap. 58)
Escribe un script de Node que lea un archivo `notas.csv` (`nombre,nota` en cada línea, con cabecera), calcule la media, la nota máxima y la lista de suspensos, y escriba el resultado en `informe.json`.

<details><summary>Solución</summary>

```csv
nombre,nota
Ana,8
Luis,4.5
Eva,9.5
Iker,3
```

```js
// informe.js
import { readFile, writeFile } from "node:fs/promises";

const csv = await readFile("notas.csv", "utf-8");

const alumnos = csv
  .trim()
  .split("\n")
  .slice(1) // quita la cabecera
  .map(linea => {
    const [nombre, nota] = linea.split(",");
    return { nombre: nombre.trim(), nota: Number(nota) };
  });

const notas = alumnos.map(a => a.nota);

const informe = {
  total: alumnos.length,
  media: Number((notas.reduce((a, b) => a + b, 0) / notas.length).toFixed(2)),
  maxima: Math.max(...notas),
  suspensos: alumnos.filter(a => a.nota < 5).map(a => a.nombre),
};

await writeFile("informe.json", JSON.stringify(informe, null, 2));
console.log("Informe generado:", informe);
```

```bash
# Ejecuta el script que lee notas.csv y genera informe.json
node informe.js
```
</details>

### 8.3 🟡 Tests (cap. 60)
Escribe tests con `node:test` para las funciones `calificar` (1.3), `esPalindromo` (1.6) y `contarPalabras` (2.8). Incluye al menos un caso límite para cada una.

<details><summary>Solución</summary>

```js
// funciones.test.js
import { test, describe } from "node:test";
import assert from "node:assert/strict";
import { calificar, esPalindromo, contarPalabras } from "./funciones.js";

describe("calificar", () => {
  test("rangos normales", () => {
    assert.equal(calificar(4.99), "Suspenso");
    assert.equal(calificar(5), "Aprobado");
    assert.equal(calificar(9), "Sobresaliente");
  });
  test("valores no válidos", () => {
    assert.equal(calificar(-1), "Nota no válida");
    assert.equal(calificar("7"), "Nota no válida");
    assert.equal(calificar(NaN), "Nota no válida");
  });
});

describe("esPalindromo", () => {
  test("frase con espacios y mayúsculas", () => {
    assert.ok(esPalindromo("Anita lava la tina"));
  });
  test("texto vacío", () => {
    assert.ok(esPalindromo(""));
  });
});

describe("contarPalabras", () => {
  test("cuenta sin distinguir mayúsculas", () => {
    const r = contarPalabras("Hola hola HOLA adiós");
    assert.equal(r.get("hola"), 3);
    assert.equal(r.get("adiós"), 1);
  });
  test("texto sin palabras", () => {
    assert.equal(contarPalabras("123 !!").size, 0);
  });
});
```

```bash
# Ejecuta todos los archivos *.test.js del proyecto
node --test
```
</details>

### 8.4 🟡 Debounce en un buscador (cap. 62)
Crea un input que filtre una lista de 1000 nombres generados. El filtrado debe ejecutarse solo cuando el usuario deje de escribir durante 300 ms. Muestra por consola cuántas veces se ejecuta el filtrado con y sin debounce.

<details><summary>Solución</summary>

```html
<input id="buscar" placeholder="Buscar…">
<p id="info"></p>
<ul id="resultados"></ul>

<script type="module">
  const nombres = Array.from({ length: 1000 }, (_, i) => `Alumno ${i + 1}`);
  let ejecuciones = 0;

  function debounce(fn, ms) {
    let id;
    return (...args) => {
      clearTimeout(id);
      id = setTimeout(() => fn(...args), ms);
    };
  }

  function filtrar(texto) {
    ejecuciones++;
    const t = texto.toLowerCase();
    const encontrados = nombres.filter(n => n.toLowerCase().includes(t)).slice(0, 20);
    document.querySelector("#resultados").replaceChildren(
      ...encontrados.map(n => Object.assign(document.createElement("li"), { textContent: n }))
    );
    document.querySelector("#info").textContent = `Filtrado ejecutado ${ejecuciones} veces`;
  }

  document.querySelector("#buscar")
    .addEventListener("input", debounce(e => filtrar(e.target.value), 300));
</script>
```

Sin debounce, escribir "Alumno 15" ejecutaría el filtrado 9 veces; con debounce, normalmente 1.
</details>

### 8.5 🔴 Fusión segura de objetos (cap. 63, 64)
Escribe `fusionProfunda(destino, origen)` que fusione objetos anidados **sin mutar** ninguno de los dos y que sea **inmune a prototype pollution**. Demuestra que el ataque del capítulo 64 no funciona con tu versión.

<details><summary>Solución</summary>

```js
const CLAVES_PELIGROSAS = new Set(["__proto__", "constructor", "prototype"]);

const esObjetoPlano = v =>
  v !== null && typeof v === "object" && !Array.isArray(v);

function fusionProfunda(destino, origen) {
  const resultado = { ...destino };
  for (const [clave, valor] of Object.entries(origen)) {
    if (CLAVES_PELIGROSAS.has(clave)) continue;
    resultado[clave] =
      esObjetoPlano(valor) && esObjetoPlano(resultado[clave])
        ? fusionProfunda(resultado[clave], valor)
        : esObjetoPlano(valor)
          ? fusionProfunda({}, valor)
          : valor;
  }
  return resultado;
}

const malicioso = JSON.parse('{"__proto__": {"esAdmin": true}, "tema": {"color": "azul"}}');
const config = fusionProfunda({ tema: { color: "rojo", tamaño: 12 } }, malicioso);

config;          // { tema: { color: "azul", tamaño: 12 } }
({}).esAdmin;    // undefined ✅
```
</details>

### 8.6 🔴 Proyecto final (cap. 65)
Completa el **Gestor de tareas** del capítulo 65 con todos los requisitos de los distintos niveles. Criterios de evaluación sugeridos:

| Criterio | Peso |
|---|---|
| Funcionalidad básica (añadir, completar, borrar, filtrar) | 25 % |
| Clases con encapsulación y validación | 15 % |
| Persistencia y carga asíncrona con gestión de errores | 15 % |
| Organización en módulos | 10 % |
| DOM: delegación de eventos y seguridad (`textContent`) | 15 % |
| Uso de novedades (iterator helpers, `groupBy`, `toSorted`, Temporal…) | 10 % |
| Tests | 10 % |

---

# ANEXO — Novedades por edición de ECMAScript

| Edición | Principales novedades |
|---|---|
| **ES2015 (ES6)** | `let`/`const`, arrow functions, clases, template literals, desestructuración, spread/rest, parámetros por defecto, promesas, módulos, `Map`/`Set`, symbols, iteradores, generadores, `Proxy`/`Reflect` |
| **ES2016** | `**`, `Array.prototype.includes` |
| **ES2017** | `async`/`await`, `Object.entries`/`values`, `padStart`/`padEnd`, `SharedArrayBuffer`, `Atomics` |
| **ES2018** | Rest/spread en objetos, `for await...of`, `Promise.finally`, grupos con nombre y lookbehind en regex |
| **ES2019** | `flat`/`flatMap`, `Object.fromEntries`, `trimStart`/`trimEnd`, `catch` sin parámetro |
| **ES2020** | `?.`, `??`, `BigInt`, `Promise.allSettled`, `globalThis`, `import()`, `matchAll` |
| **ES2021** | `??=`, `||=`, `&&=`, `replaceAll`, `Promise.any`, separadores numéricos, `WeakRef` |
| **ES2022** | Campos privados `#`, `static {}`, `#x in obj`, `at()`, `Object.hasOwn`, top-level await, `Error.cause`, flag `d` |
| **ES2023** | `toSorted`, `toReversed`, `toSpliced`, `with`, `findLast`, `findLastIndex`, hashbang `#!` |
| **ES2024** | `Object.groupBy`, `Map.groupBy`, `Promise.withResolvers`, flag `v`, ArrayBuffer redimensionable, `isWellFormed`, `Atomics.waitAsync` |
| **ES2025** | Iterator helpers, métodos de `Set`, `Promise.try`, `RegExp.escape`, modificadores regex, grupos con nombre duplicados, import attributes y módulos JSON, `Float16Array` |
| **ES2026** ⭐ | `Array.fromAsync`, `Error.isError`, `Math.sumPrecise`, Base64/hex en `Uint8Array`, `Iterator.concat`, `JSON.parse` con texto fuente, `Map`/`WeakMap` `getOrInsert` |
| **ES2027** (prevista) | Temporal, `using`/`await using`, `Atomics.pause`, Joint Iteration (`Iterator.zip`)… |

## Recursos recomendados

- **MDN Web Docs** (developer.mozilla.org): la referencia de cabecera.
- **javascript.info**: tutorial muy completo y bien explicado.
- **Repositorio de propuestas de TC39** (github.com/tc39/proposals): para seguir lo que viene.
- **Node.js docs** (nodejs.org/docs).
- **caniuse.com**: compatibilidad de navegadores.
