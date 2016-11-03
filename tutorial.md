# Semana de la Ciencia 2016 @ INIA

## Explorable Explanations

***Explorable Explanations*** es un término acuñado por el ingeniero y diseñador Bret Victor para referirse a un documento interactivo, de carácter científico-técnico, que explica determinado concepto dando la oportunidad al lector de explorar los cambios que ocurren en el sistema o proceso cuando se modifican algunas de las variables que lo controlan.

Las páginas web y las aplicaciones para móvil o para tablet son el lugar ideal para estas Explicaciones Explorables, pero no significa que sea el único medio en el que se pueden construir. Una alternativa podrían ser los libros interactivos, con mecanismos simples de papel.

En este taller vamos a ver como podemos construir una sencilla web que nos ayude a explicar la relación que hay en un incendio forestal entre el material inflamado, la velocidad de propagación del fuego, el tamaño de la llama, y los medios de extinción más adecuados en cada caso.

Para ello construiremos progresivamente una página web interactiva con Javascript.

## Estructura básica de una página web

Como algunos sabréis las páginas web están escritas en lenguaje HTML. La estructura más básica que podemos construir es:

```html
<html lang="es">
  <head>
    <meta charset="utf-8">
    <title>¡Hola, mundo!</title>
  </head>

  <body>
    <p>¡Hola, mundo!</p>
  </body>
</html>
```

Antes de seguir creemos un fichero llamado `index.html` en una carpeta adecuada de nuestro ordenador, y copiemos o mejor, escribamos en él, el código de ejemplo. Después podemos abrir dicho fichero con nuestro navegador, y podremos ver el resultado de la página web.

![Página web *Hola mundo*](img/helloWorld.png)

**HTML** es un lenguaje de etiquetas. Cada sección del documento está comprendida entre una etiqueta de apertura `<tag>` y su correspondiente etiqueta de cierre `</tag>`.

Las etiquetas `<html>` y `</html>` limitan el princpio y el final del documento. También podemos ver que el documento se divide en dos secciones principales, una limitada por la etiqueta `<head>` donde se indican aspectos de configuración de la página web; y otra limitada por la etiqueta `<body>` donde está el contenido de la página propiamente dicho.

En este taller pasaremos de puntillas sobre muchos aspectos de **HTML**. Los interesados en profundizar en esta materia pueden seguir la documentación de **MDN** (Mozilla Developer Network): https://developer.mozilla.org/es/docs/Learn/HTML

## Introducción a Javascript

Desde que el navegador Netscape incluyera por primera vez la posibilidad de ejecutar código Javascript en 1995, este lenguaje se han convertido en el estándar para desarrollo en el lado del cliente de la web.

Javascript tiene una sintáxis de la familia de C, similar a la de muchos lenguajes populares como C, C++, Java o PHP. Para incluir código Javascript en nuestra página web hacemos uso de la etiqueta `<script>`.

```html
<html lang="es">
  <head>
    <meta charset="utf-8">
    <title>INIA - Semana de la Ciencia 2016 ::: Explicaciones Explorables</title>
  </head>

  <body>
    <p>¡Hola, mundo!</p>
    <script>
      alert('Hola, mundo!');
    </script>
  </body>
</html>
```

La etiqueta `<script>` puede ser incluida tanto en la sección `head` como en la sección `body`. Puesto que los ficheros HTML se ejecutan conforme son leídos, colocar el bloque `script` al final de la sección `body`, da ciertas garantías que el contenido completo de la página web ha sido cargado antes de ejecutar el código.

Este ejemplo ejecuta la función `alert()` que indica al navegador que queremos mostrar un aviso, que requiere la aprobación ('Aceptar') del usuario antes de continuar.

![Página web `alert()`](img/alert.png)

## Busquemos un aliado: Firebug

**Firebug** es un plugin de Firefox que facilita el desarrollo de páginas web y aplicaciones. Se instala fácilmente desde el gestor de complementos de Firefox. Una vez instalado, Firebug aparece con el icono de un pequeño insecto en la barra de herramientas del navegador.

![Firebug en la barra de herramientas](img/iconoFirebug.png)

La suite de Firebug tiene distintas herramientas que nos facilitan el trabajo de desarrollo: Consola, HTML, CSS, Script, DOM, Red y Cookies.

![Suite Firebug](img/firebug.png)

La herramienta *Console* nos mostrará los mensajes de error que genere nuestro código Javascript, pero también podemos acceder a ella haciendo uso del comando `console.log()`.

```html
<script>
  console.log('Hola, mundo!');
</script>
```

![Ejemplo console.log](img/console_log.png)

También es posible escribir código Javascript directamente en la consola, lo que la hace una manera ideal de realizar pruebas y aprender interactivamente.

![Ejemplo de código en la consola](img/codigoConsola.png)

## Un viaje rápido por Javascript

Este taller, por su brevedad, solo pretende mostrar algunas características generales de Javascript, y unos pocos de los detalles que lo diferencian de otros lenguajes de programación.

Podemos hacer el siguiente recorrido directamente en la consola que abrimos en la sección anterior:

```javascript
// Javascript admite comentarios de línea

/*
  y comentarios de bloque
*/

var a; // declaramos una variable
a = 2; // y le podemos asignar un valor
var b;
b = "2"; // no es necesario declarar tipos
a == b; // y a veces no le importa demasiado
a === b; // pero le podemos pedir que tenga cuidado

// de todos modos casi siempre debemos tener cuidado nosotros

alert('Llamando la atención'); //podemos llamar a funciones
// y declarar nuestras propias funciones
function suma(sumando1, sumando2) { return sumando1 + sumando2; }

suma(a, a); // podemos llamar a nuestra propias funciones

var o = { parametro1: 1, parametro2: 22}; // esto es un objeto Javascript
o.parametro1; // accedemos a su interior con el operador .
o.parametro1 = o.parametro1 + o.parametro2;

var f = suma; // una función es un valor más que se puede guardar en una función
f(a, a);
o.fn = suma; // incluso en el parámetro de un objeto
o.fn(a, o.parametro1);

console.log('Llamada a la función log() del objeto console');

var log_original = console.log; // Javascript es muy perro
console.log = function(texto) { return log_original.call(this, 'Consola en huelga')};
console.log('texto de ejemplo');

```

Javascript tiene detalles bastante avanzados. Si os habéis fijado, las funciones son objetos que tienen algunas funciones incluídas por defecto, como `call()`. Por ejemplo, podéis hacer también `suma.call(null, 2, 2);`. Estas características hacen que sea un lenguaje realmente muy flexible.

# Una Explicación Explorable

Vamos a crear una sencilla página web, que muestre la fórmula de Byram y permita explorar su evolución con algunos valores para la velocidad de propagación y los materiales del incendio.

En primer lugar creamos una sencilla web con las fórmulas, los datos y un ejemplo de la parte explorable.

```html
<html lang="es">
  <head>
    <meta charset="utf-8">
    <title>INIA - Semana de la Ciencia 2016 ::: Explicaciones Explorables</title>
  </head>

  <body>
    <h1>Tamaño de la llama en incendios forestales</h1>
    <p>El tamaño de la llama en un incendio forestal puede ser calculado a partir de la velocidad de propagación, la cantidad de material y sus características según la fórmula:</p>

    <img alt="" src="img/eqIntensidad.gif"><br/>
    <img alt="" src="img/eqLongitud.gif"><br/>
    <img alt="Fórmula de Byram" src="img/eqByram.gif">

    <p>Conocemos algunos valores estándares de características de los materiales para distintos tipos
      de vegetación:
    </p>

    <table>
      <tr>
        <th>Vegetación</th>
        <th>Densidad (kg/m<sup>2</sup>)</th>
      </tr>
      <tr>
        <td>Pasto</td>
        <td>0.1</td>
      </tr>
      <tr>
        <td>Monte bajo</td>
        <td>0.8</td>
      </tr>
      <tr>
        <td>Bosque</td>
        <td>3.5</td>
      </tr>
    </table>

    <p> Nos encontramos ante un incendio de <em>pasto</em> que se mueve a una velocidad de <em>10</em> m/min.
      El valor de longitud de la llama esperado es <em>&lt;valor calculado&gt;</em>m.
    </p>

    <script>
      console.log('Hola, mundo!');
    </script>
  </body>
</html>
```

Hemos introducido un par de etiquetas nuevas, como <table> para construir la tabla de datos, o `<em>` para dar enfásis. Además hemos creado añadido las ecuaciones en forma de gráficos GIF (usando la herramienta online https://www.codecogs.com/latex/eqneditor.php).

Para añadir las imágenes podéis descargarlas del sitio web (https://github.com/inia-es/semanaCiencia16_iiff_src/tree/master/img). Este sitio web tiene todo el código de este ejemplo, pero si lo descargáis ahora arruinareis parte de la diversión.

# Haciendo un sitio interactivo

Para esta parte del tutorial vamos a hacer uso de la librería Tangle. Podemos descargar los ficheros en http://worrydream.com/Tangle/download.html, y ponerlo en una carpeta `js` de nuestro proyecto.

Ahora lo añadimos a nuestra web añadiendo:
```html
<script src="js/Tangle.js"></script>
<link rel="stylesheet" href="css/TangleKit.css" type="text/css">
<script type="text/javascript" src="js/mootools.js"></script>
<script type="text/javascript" src="js/sprintf.js"></script>
<script type="text/javascript" src="js/BVTouchable.js"></script>
<script type="text/javascript" src="js/TangleKit.js"></script>
```
a la sección `head` de nuestra página web.

Ahora vamos a identificar la velocidad de propagación como un parámetro de entrada. Para ello vamos a modificar el texto `<em>10</em> m/min` por el siguiente código.
```html
<span var-data="velocidad" class="TKAdjustableNumber"> m/min</span>
```

Y en la sección `<script>` incializamos dicha variable:
```js
var tangle = new Tangle(document, {
  initialize: function () { this.velocidad = 10; },
  update:     function () { }
});
 ```

 # Generando valores de salida

 Ahora vamos a hacer que el valor de longitud de la llama varie con la velocidad.
 Primero, identificamos la longitud de la llama como una variable del modelo, sustituimos ```<em>&lt;valor calculado&gt;</em> m``` por algo como:
 ```html
 <span data-var="longitudLlama"> m</span>
 ```

 Añadimos una función que calcule el valor de la llama. Vamos a usar una función de prueba, que nos permite probar el sistema interactivo. En el siguiente bloque usaremos la fórmula de Byram correctamente.
 ```js
 var calcularLongitud = function(velocidad) {
   return velocidad * 13;
 }
 ```

 Y usamos esa función para actualizar el valor de `longitudLlama` en el modelo de Tangle:
 ```js
 var tangle = new Tangle(document, {
   initialize: function () { this.velocidad = 10; },
   update:     function () { this.longitudLlama = calcularLongitud(this.velocidad); }
 });
  ```

# Matemáticas en Javascript

Vamos a crear una función en Javascript para la fórmula de Byram. Es más fácil de lo que parece:
```js
function formulaByram(biomasa, velocidad) {
  // biomasa: kg/m^2
  // velocidad: m/min
  return 0.37 * Math.pow((15000 * biomasa * velocidad)/60, 0.46);
}
```
Ahora usaremos esta fórmula en nuestra función `calcularLongitud()`
```js
var calcularLongitud = function(velocidad) {
  var biomasa_pasto = 0.8;
  return formulaByram(biomasa_pasto, velocidad);
};
```

# Mejora estética

Vamos a mejorar un poco el aspecto de nuestro proyecto. En primer vamos a mejorar el aspecto de nuestra interfaz. Añadiremos parámetros a nuestro modelo para que admita decimales en la entrada y podamos darle un rango mínimo y máximo de valores, lo haremos con las etiquetas `data-min`, `data-max` y `data-step`:
```html
<span data-min="0" data-max="10" data-step="0.5" data-var="velocidad" class="TKAdjustableNumber"> m/min</span>
```
En segundo lugar vamos a dar formato a la salida, para poder ignorar los decimales que no necesitemos. Lo haremos con la etiqueta `data-format`. Esta etiqueta formatea la salida haciendo uso de la descripción de formatos de la librería estándar de C  (`print()`, `sprintf()`, ...). Ver http://www.manpages.info/linux/sprintf.3.html
```html
<span data-format="%.2f" data-var="longitud"> m</span>
```

# Sofisticando el modelo

Hasta ahora hemos trabajado siempre con el mismo tipo de incendio, uno de pasto. Vamos a introducir ahora los otros tipos de incencios: monte bajo y bosque.

Modificaremos `<em>pasto</em>` para que sea una variable de entrada:
```html
<span data-var="combustible" data-min="1" data-max="3" class="TKAdjustableNumber TKSwitch">
  <span>pasto</span>
  <span>monte bajo</span>
  <span>bosque</span>
</span>
```
`TKAdjustableNumber` funciona como un selector horizontal como el que usamos para la velocidad. `TKSwitch` muestra solo uno de los valores contenidos según el valor que adopte la variable `combustible`.

Ahora añadiremos la información de biomasa a Javascript, para poder usarla en la fórmula. Para ello usaremos un array:
```js
var biomasa = [
  null, // valor nulo para evitar el error por 1
  0.1, // pastos
  0.8, // monte bajo
  3.5, // boque, ojo a la coma
];
```
Ahora solo nos queda introducirlo en la fórmula de Byram:
```js

  update: function () { this.longitud = formulaByram(biomasa[this.combustible], this.velocidad) },
```

**¡¡Enhorabuena!!**, habéis construido vuestra primera Explicación Explorable.

# Buenas prácticas
Vamos a evitar replicar los valores de biomasa en el código y en el HTML. Para ello tomaremos los valores de la tabla como origen de datos, y los utilizaremos en Javascript.

En primer lugar anotaremos los valores de la tabla con microdatos. Los microdatos describen más precisamente la información de una web, y permiten que sea explorada por buscadores con más información o utilizada por aplicaciones de terceros.

Usar microdatos es muy sencillo:
```html
<td itemscope itemtype="http://schema.org/Mass" id="biomasa_pasto">0.1 kg</td>
```

Para acceder a los valores usaremos la función `document.getElementById()` que nos devuelve un elemento HTML. Para acceder a su contenido usamos su propiedad `innerHTML`. Por último creamos una función que elimina la unidad de kg y nos devuelve un valor numérico.

```js
function valorMasa(texto) {
  return parseFloat(texto.slice(0,-3));
}

var biomasa = [
  null, // valor nulo para evitar el error por 1
  valorMasa(document.getElementById('biomasa_pasto').innerHTML), // pastos
  valorMasa(document.getElementById('biomasa_monte_bajo').innerHTML), // monte bajo
  valorMasa(document.getElementById('biomasa_bosque').innerHTML), // bosque
];
```
