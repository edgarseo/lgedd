
# 1. CREA UNA LISTA VACÍA EN TU PÁGINA HTML UL> /UL>. AL CARGAR LA PÁGINA, A TRAVÉS DEL DOM, AGREGA AUTOMÁTICAMENTE TRES ELEMENTOS DE LISTA (LI>…/LI>) CON LOS TEXTOS "ELEMENTO 1", "ELEMENTO 2" Y "ELEMENTO 3" RESPECTIVAMENTE.


```html
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Manipulación del DOM Modular</title>
</head>
<body>

    <!-- Lista vacía requerida -->
    <ul id="miLista"></ul>

    <!-- Vinculación del script externo -->
    <script src="script.js" defer></script>

</body>
</html>

```


```js
document.addEventListener("DOMContentLoaded", () => {
    // 1. Obtener la referencia de la lista vacía
    const lista = document.getElementById("miLista");
    
    // 2. Colección de datos a renderizar
    const textos = ["Elemento 1", "Elemento 2", "Elemento 3"];

    // 3. Crear elementos en memoria y añadirlos al DOM
    textos.forEach(texto => {
        const nuevoItem = document.createElement("li");
        nuevoItem.textContent = texto;
        lista.appendChild(nuevoItem);
    });
});
```


# 2. CREA UNA PÁGINA HTML CON TRES PÁRRAFOS (PUEDEN CONTENER TEXTO O NO). AL CARGAR LA PÁGINA, A TRAVÉS DEL DOM, CAMBIA EL TEXTO DE TODOS LOS PÁRRAFOS A "TEXTO ACTUALIZADO AUTOMÁTICAMENTE"


```html
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Actualización Masiva de Párrafos</title>
</head>
<body>

    <!-- Los tres párrafos iniciales (en este caso con texto genérico) -->
    <p>Texto original 1</p>
    <p>Texto original 2</p>
    <p>Texto original 3</p>

    <!-- Vinculación del script externo -->
    <script src="script.js" defer></script>

</body>
</html>

```


```js
document.addEventListener("DOMContentLoaded", () => {
    // 1. Seleccionar todos los elementos <p> del documento
    const parrafos = document.querySelectorAll("p");

    // 2. Iterar sobre la colección obtenida y actualizar su contenido
    parrafos.forEach(parrafo => {
        parrafo.textContent = "Texto actualizado automáticamente";
    });
});
```



# CREA UNA PÁGINA HTML CON VARIOS ELEMENTOS LOS QUE TÚ ELIJAS PERO UN MÍNIMO DE 4 ELEMENTOS ej articule, section, p, span... SE PERMITE REPETIR ELEMENTOS) QUE TENGAN UNA CLASE LLAMADA “DESTACADO” (EJ:HOLA). DESDE EL DOM, HACIENDO REFERENCIA A LA CLASE “DESTACADO”, CAMBIA SU COLOR DE TEXTO A ROJO Y SU FONDO A AMARILLO AL CARGAR LA PÁGINA.

```html
<!DOCTYPE html>

<html lang="es">

<head>

    <meta charset="UTF-8">

    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <title>Estilos Dinámicos Modulares</title>

</head>

<body>

  

    <!-- Elementos con la clase "destacado" -->

    <article class="destacado">Este es un artículo destacado.</article>

    <section class="destacado">Esta es una sección destacada.</section>

    <p class="destacado">Este es un párrafo destacado.</p>

    <span class="destacado">Este es un texto span destacado.</span>

  

    <!-- Elemento de control sin la clase -->

    <p>Este es un párrafo normal (no cambia).</p>

  

    <!-- Vinculación del script externo al final del body -->

    <script src="script.js"></script>

  

</body>

</html>
```


```js
// 1. Seleccionar todos los elementos con la clase "destacado" usando var

var elementosDestacados = document.querySelectorAll(".destacado");

  

// 2. Recorrer la colección y aplicar estilos CSS individuales

elementosDestacados.forEach(function(elemento) {

    elemento.style.color = "red";             // Texto a rojo

    elemento.style.backgroundColor = "yellow"; // Fondo a amarillo

});
```


# Por clases

```html
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Estilos por Clases Dinámicas</title>
    <!-- Vinculación del CSS -->
    <link rel="stylesheet" href="estilos.css">
</head>
<body>

    <!-- Elementos con la clase "destacado" -->
    <article class="destacado">Este es un artículo destacado.</article>
    <section class="destacado">Esta es una sección destacada.</section>
    <p class="destacado">Este es un párrafo destacado.</p>
    <span class="destacado">Este es un texto span destacado.</span>

    <p>Este es un párrafo normal (no cambia).</p>

    <!-- Vinculación del JS -->
    <script src="script.js"></script>

</body>
</html>

```


```js 
window.onload = function() {
    // 1. Seleccionar los elementos por su clase (sin punto)
    var elementosDestacados = document.getElementsByClassName("destacado");

    // 2. Recorrer la colección con un bucle for tradicional usando var
    for (var i = 0; i < elementosDestacados.length; i++) {
        elementosDestacados[i].style.color = "red";
        elementosDestacados[i].style.backgroundColor = "yellow";
    }
};

```


# Por id

```html

<!DOCTYPE html>

<html lang="es">

<head>

    <meta charset="UTF-8">

    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <title>Modificación por ID Únicos</title>

</head>

<body>

  

    <!-- Elementos con IDs únicos -->

    <article id="item1">Este es un artículo destacado.</article>

    <section id="item2">Esta es una sección destacada.</section>

    <p id="item3">Este es un párrafo destacado.</p>

    <span id="item4">Este es un texto span destacado.</span>

  

    <p>Este es un párrafo normal.</p>

  

    <!-- Vinculación limpia -->

    <script src="script.js"></script>

  

</body>

</html>
```


```js
<!DOCTYPE html>

<html lang="es">

<head>

    <meta charset="UTF-8">

    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <title>Modificación por ID Únicos</title>

</head>

<body>

  

    <!-- Elementos con IDs únicos -->

    <article id="item1">Este es un artículo destacado.</article>

    <section id="item2">Esta es una sección destacada.</section>

    <p id="item3">Este es un párrafo destacado.</p>

    <span id="item4">Este es un texto span destacado.</span>

  

    <p>Este es un párrafo normal.</p>

  

    <!-- Vinculación limpia -->

    <script src="script.js"></script>

  

</body>

</html>
```



# Cambiar color h1 y background

```html
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Cambio de Fondo y Título</title>
</head>
<body>

    <h1>Este es el título principal</h1>
    <p>Contenido de la página...</p>

    <!-- Cargamos el JS al final del todo -->
    <script src="script.js"></script>

</body>
</html>

```


```js

// 1. Cambiar el fondo de todo el HTML (body)
document.body.style.backgroundColor = "lightblue";

// 2. Seleccionar el h1 y cambiar su color de texto
document.querySelector("h1").style.color = "darkblue";

```


# Click color

```html
<!DOCTYPE html>

<html lang="es">

<head>

    <meta charset="UTF-8">

    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <title>Cambio de Fondo y Título</title>

</head>

<body>

  

    <h1>Este es el título principal</h1>

    <p>Contenido de la página...</p>

  

    <!-- Cargamos el JS al final del todo -->

    <script src="script.js"></script>

  

</body>

</html>
```


```js
// Escucha el clic en la ventana completa del navegador (toda la pantalla)
window.onclick = function() {
    document.body.style.backgroundColor = "red";
};

```


# Alert

```html
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Petición de Edad</title>
</head>
<body>

    <h1>Bienvenido a la página</h1>
    <p>El fondo cambiará a rojo si haces clic en cualquier lado después de introducir tu edad.</p>

    <!-- Vinculación del JS externo -->
    <script src="script.js"></script>

</body>
</html>

```


```js
// 1. Pide la edad al usuario y la guarda en la variable

var edad = prompt("Por favor, introduce tu edad:");

  

// 2. Muestra una ventana flotante con la edad introducida

alert("Tu edad es: " + edad);
```

