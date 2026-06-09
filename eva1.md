


# EJER 1


Instrucciones: Está permitido tener todo tipo de material y acceso a internet con la limitación de acceso a cualquier herramienta que utilice  
IA. En caso de que se detecte a algún alumno haciendo uso de alguna de estas herramientas, durante o al corregir el examen, la calificación de la prueba será automáticamente de 0.  
Esta parte tiene un peso de 8 puntos.  
Ejercicio 1 
Crea una tabla como la que se adjunta en la imagen "solucion_ejl.png". Solo tienes que crear la tabla y vincular el archivo de estilos "style.css" a tu archivo html. Para que tu tabla se ajuste al estilo de la solución, debes seguir las siguientes indicaciones:  
﻿﻿El título "Ejercicio 1" será un elemento h1.  
﻿﻿Las celdas "Días laborales de la semana" ocuparán un total de 6 columnas y tendrán una clase llamada "laborales".  
﻿﻿La celda "Mes de enero" ocupará un total de 6 filas y tendrá una clase llamada  
"ene".  
﻿﻿Todas las celdas correspondientes a cada día de la semana tendrán una clase compuesta por las primeras tres letras de cada día: "lun" para lunes, "mar" para martes, "mie" para miércoles, "jue" para jueves y "vie" para viernes.  
﻿﻿La celda 9:00 del martes ocupará un total de 3 filas.  
﻿﻿La celda 9:00 del miércoles ocupará un total de 2 filas.  
﻿﻿La celda 10:35 del viernes ocupará un total de 2 filas y 2 columnas.
﻿﻿

```html
<!DOCTYPE html>

<html lang="es">

<head>

    <meta charset="UTF-8">

    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <title>Horario Laboral Semanal</title>

    <link rel="stylesheet" href="style.css">

</head>

<body>

  

        <h1>Ejercicio 1</h1>

  

        <h2>Horario Laboral Semanal</h2>

  
  
  

    <table>

        <!-- Barra superior amarilla -->

        <tr>

            <td colspan="6" class="laborales">Días laborales de la semana</td>

        </tr>

  

        <!-- Fila de Cabeceras de los Días -->

        <tr>

            <td rowspan="6" id="ene">Mes de enero</td>

            <td class="lun">Lunes</td>

            <td class="mar">Martes</td>

            <td class="mie">Miércoles</td>

            <td class="jue">Jueves</td>

            <td class="vie">Viernes</td>

        </tr>

  

        <!-- Fila 1 de horarios -->

        <tr>

            <td class="lun">8:30</td>

            <td rowspan="3" class="mar">9:00</td>

            <td class="mie">8:45</td>

            <td class="jue">10:00</td>

            <td class="vie">9:45</td>

        </tr>

  

        <!-- Fila 2 de horarios -->

        <tr>

            <td class="lun">9:00</td>

            <td rowspan="2" class="mie">9:00</td>

            <td class="jue">10:15</td>

            <td class="vie">10:15</td>

        </tr>

  

        <!-- Fila 3 de horarios -->

        <tr>

            <td class="lun">9:30</td>

            <td colspan="2" rowspan="2" class="vie">10:35</td>

        </tr>

  

        <!-- Fila 4 de horarios -->

        <tr>

            <td class="lun">10:00</td>

            <td class="mar">9:30</td>

            <td class="mie">9:15</td>

        </tr>

  

        <!-- Fila de Pies de los Días -->

        <tr>

            <td class="lun">Lunes</td>

            <td class="mar">Martes</td>

            <td class="mie">Miércoles</td>

            <td class="jue">Jueves</td>

            <td class="vie">Viernes</td>

        </tr>

  

        <!-- Barra inferior amarilla -->

        <tr>

            <td colspan="6" class="laborales">Días laborales de la semana</td>

        </tr>

    </table>

  

</body>

</html>
```


# CSS


```css
table {

    width: 100%;

    border: 1px solid #000;

}

  

caption {

    font-size: 20px;

    font-weight: bold;

}

  

th,

td {

    border: 1px solid #000;

    text-align: center;

}

  

.laborales {

    background-color: yellow;

}

  

#ene {

    background-color: rgb(238, 178, 68);

}

  

.lun,

.mar {

    background-color: #51e237;

}

  

.mie {

    background-color: rgb(23, 211, 211);

}

  

.jue,

.vie {

    background-color: #686565;

    color: white;

}

  

h2 {

    text-align: center;

    margin-bottom: 0;

}

```


# Ejer 2


Condiciones: Solo se puede editar el archivo style.css:  
﻿﻿No se permite modificar el HTML proporcionado.  
No se permite usar calcO, Grid ni frameworks CSS.  
Es obligatorio el uso de Flexbox, flex-wrap, gap y media queries.  
﻿﻿Estilos generales:  
﻿﻿Aplica box-sizing: border-box a todos los elementos.  
Elimina el margen por defecto del body.  
Usa la fuente Arial, sans-serif.  
Establece fondo blanco para la página.  
﻿﻿Encabezado:  
﻿﻿Fondo #0b2757.  
﻿﻿Texto blanco.  
﻿﻿Texto centrado.  
﻿﻿Padding de 20px.  
﻿﻿Contenedor principal (.contenedor):  
﻿﻿Activa Flexbox.  
﻿﻿Permite salto de línea con flex-wrap.  
﻿﻿Añade separación entre tarjetas con gap: 20px.  
﻿﻿Añade padding interior de 20px.  
﻿﻿Limita el ancho máximo a 1100px y céntralo.  
﻿﻿Tarjetas (-tarjeta):  
﻿﻿Fondo #f4f4f4.  
﻿﻿Bordes redondeados (12px).  
﻿﻿Padding de 20px.  
﻿﻿Convierte la tarjeta en Flexbox en columna.  
﻿﻿En escritorio, muestra 3 tarjetas por fila usando flex: 1 1 30%.  
﻿﻿Botón:  
﻿﻿Alinea el botón abajo usando margin-top: auto.  
﻿﻿Padding de 10px, sin borde, borde redondeado (10px).  
﻿﻿Fondo #e85810, texto blanco y cursor pointer.  
﻿﻿Hover: cambia el fondo a rgb(42, 38, 38).  
﻿﻿Media queries:  
﻿﻿Pantallas pequeñas (<768px):  
﻿﻿El contenedor pasa a columna.  
﻿﻿Las tarjetas ocupan el 100% y centran el texto.  
﻿﻿El botón ocupa el 100% del ancho


```html
<!DOCTYPE html>

<html lang="es">

  

<head>

    <meta charset="UTF-8" />

    <meta name="viewport" content="width=device-width, initial-scale=1.0" />

    <title>Ejercicio 2</title>

    <link rel="stylesheet" href="style.css" />

</head>

  

<body>

  

    <header>

        <h1>Nuestros Servicios</h1>

    </header>

  

    <main>

        <section class="contenedor">

            <article class="tarjeta">

                <h2>Servicio 1</h2>

                <p>Descripción del servicio ofrecido. Texto de ejemplo para simular que ofrecemos algo para el primer servicio.</p>

                <button>Más info</button>

            </article>

  

            <article class="tarjeta">

                <h2>Servicio 2</h2>

                <p>Descripción del servicio ofrecido. Texto de ejemplo para simular que ofrecemos algo para el segundo servicio.</p>

                <button>Más info</button>

            </article>

  

            <article class="tarjeta">

                <h2>Servicio 3</h2>

                <p>Descripción del servicio ofrecido. Texto de ejemplo para simular que ofrecemos algo para el tercer servicio.</p>

                <button>Más info</button>

            </article>

  

            <article class="tarjeta">

                <h2>Servicio 4</h2>

                <p>Descripción del servicio ofrecido. Texto de ejemplo para simular que ofrecemos algo para el cuarto servicio.</p>

                <button>Más info</button>

            </article>

  

            <article class="tarjeta">

                <h2>Servicio 5</h2>

                <p>Descripción del servicio ofrecido. Texto de ejemplo para simular que ofrecemos algo para el quinto servicio.</p>

                <button>Más info</button>

            </article>

  

            <article class="tarjeta">

                <h2>Servicio 6</h2>

                <p>Descripción del servicio ofrecido. Texto de ejemplo para simular que ofrecemos algo para el sexto servicio.</p>

                <button>Más info</button>

            </article>

        </section>

    </main>

  

</body>

  

</html>

```


```css

/* --- Estilos generales --- */

* {

    box-sizing: border-box;

}

  

body {

    margin: 0;

    font-family: Arial, sans-serif;

    background-color: white;

}

  

/* --- Encabezado --- */

header {

    background-color: #0b2757;

    color: white;

    text-align: center;

    padding: 20px;

}

  

/* --- Contenedor principal --- */

.contenedor {

    display: flex;

    flex-wrap: wrap;

    justify-content: space-between; /* Distribuye el espacio entre columnas */

    gap: 20px;

    padding: 20px;

    max-width: 1100px;

    margin: 0 auto;

}

  

/* --- Tarjetas (Por defecto en Escritorio: 3 columnas) --- */

.tarjeta {

    background-color: #f4f4f4;

    border-radius: 12px;

    padding: 20px;

    display: flex;

    flex-direction: column;

    flex: 0 1 31%; /* 3 columnas por fila */

}

  

/* --- Botón --- */

.tarjeta button {

    margin-top: auto;

    padding: 10px;

    border: none;

    border-radius: 10px;

    background-color: #e85810;

    color: white;

    cursor: pointer;

}

  

.tarjeta button:hover {

    background-color: rgb(42, 38, 38);

}

  

/* --- MEDIA QUERIES --- */

  

/* 1. Pantallas Medianas (Mid Screen: entre 768px y 1024px) */

@media (min-width: 768px) and (max-width: 1024px) {

    .tarjeta {

        flex: 0 1 48%; /* Cambia exactamente a 2 columnas por fila */

    }

}

  

/* 2. Pantallas Pequeñas (Lit Screen: menos de 768px) */

@media (max-width: 767px) {

    .contenedor {

        flex-direction: column;

    }

  

    .tarjeta {

        flex: 1 1 100%; /* 1 columna por fila */

        text-align: center;

    }

  

    .tarjeta button {

        width: 100%;

    }

}
```


# Ejer 3

Para validar una biblioteca digital en XML, se proporciona el documento   "Ejercicio3 xml". Se requiere realizar una estructura que permita representar no solo libros, sino también información adicional sobre autores, editoriales y disponibilidad mediante un archivo DTD. Para ello, debes de tener en cuenta las siguientes consideraciones y plasmarlas en un nuevo fichero llamado "Ejercicio3.dtd":  
﻿﻿﻿El archivo XMIL representará una biblioteca que contiene múltiples libros.  
﻿﻿﻿Cada libro debe tener:  
﻿﻿Un atributo obligatorio isbn  
﻿﻿Un elemento titulo  
﻿﻿Un elemento autor, que a su vez contiene:  
﻿﻿nombre  
﻿﻿apellido  
﻿﻿nacionalidad (opcional)  
﻿﻿Un elemento editorial con:  
﻿﻿nombre  
﻿﻿pais  
﻿﻿Un elemento año_publicacion  
﻿﻿Un elemento generos que contenga uno o más elementos genero  
﻿﻿Un elemento disponibilidad, con atributo formato (ej. "digital' o  
"impreso") y texto "sí" o "no"


```xml
<?xml version="1.0" encoding="UTF-8"?>

<!DOCTYPE biblioteca SYSTEM "Ejercicio3.dtd">



<biblioteca>

    <libro isbn="978-1234567890">

        <titulo>Introducción a XML</titulo>

        <autor>

            <nombre>Ana</nombre>

            <apellido>Pérez</apellido>

            <nacionalidad>España</nacionalidad>

        </autor>

        <editorial>

            <nombre>TecnoLibros</nombre>

            <pais>España</pais>

        </editorial>

        <anio_publicacion>2020</anio_publicacion>

        <generos>

            <genero>Tecnología</genero>

            <genero>Programación</genero>

        </generos>

        <disponibilidad formato="digital">sí</disponibilidad>

    </libro>

  

    <libro isbn="978-0987654321">

        <titulo>La Historia del Arte</titulo>

        <autor>

            <nombre>Lucas</nombre>

            <apellido>Gómez</apellido>

        </autor>

        <editorial>

            <nombre>ArteMundo</nombre>

            <pais>Argentina</pais>

        </editorial>

        <anio_publicacion>2015</anio_publicacion>

        <generos>

            <genero>Arte</genero>

            <genero>Historia</genero>

        </generos>

        <disponibilidad formato="impreso">no</disponibilidad>

    </libro>

</biblioteca>

```


```dtd
<!-- EMPIEZA A ESCRIBIR AQUÍ TU CÓDIGO -->

<!-- Elemento raíz: La biblioteca contiene uno o múltiples libros -->

<!ELEMENT biblioteca (libro+)>

  

<!-- Estructura de cada libro: Orden obligatorio de sus elementos hijos -->

<!ELEMENT libro (titulo, autor, editorial, anio_publicacion, generos, disponibilidad)>

<!-- Atributo obligatorio 'isbn' para el libro -->

<!ATTLIST libro isbn CDATA #REQUIRED>

  

<!-- Elemento titulo -->

<!ELEMENT titulo (#PCDATA)>

  

<!-- Elemento autor: nombre y apellido obligatorios; nacionalidad opcional (?) -->

<!ELEMENT autor (nombre, apellido, nacionalidad?)>

<!ELEMENT nombre (#PCDATA)>

<!ELEMENT apellido (#PCDATA)>

<!ELEMENT nacionalidad (#PCDATA)>

  

<!-- Elemento editorial: nombre y pais obligatorios -->

<!ELEMENT editorial (nombre, pais)>

<!ELEMENT pais (#PCDATA)>

  

<!-- Elemento anio_publicacion (Nota: adaptado de tu XML previo 'anio_publicacion') -->

<!ELEMENT anio_publicacion (#PCDATA)>

  

<!-- Elemento generos: Debe contener uno o más (+) elementos genero -->

<!ELEMENT generos (genero+)>

<!ELEMENT genero (#PCDATA)>

  

<!-- Elemento disponibilidad: Contiene texto (#PCDATA) como "sí" o "no" -->

<!ELEMENT disponibilidad (#PCDATA)>

<!-- Atributo obligatorio 'formato' restringido a los valores específicos requeridos -->

<!ATTLIST disponibilidad formato (digital | impreso) #REQUIRED>
```
