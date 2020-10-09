- [¿Qué es un tema?](#%C2%BFQu%C3%A9-es-un-tema)
  - [Qué puede hacer un tema](#Qu%C3%A9-puede-hacer-un-tema)
  - [Cuál es la diferencia entre un tema y un plugin](#Cu%C3%A1l-es-la-diferencia-entre-un-tema-y-un-plugin)
- [Index.php y styles.css](#Indexphp-y-stylescss)
- [Jerarquía de plantillas](#Jerarqu%C3%ADa-de-plantillas)
- [The loop](#The-loop)

### Creación de temas


## ¿Qué es un tema?
Un tema para WordPress (WordPress theme en inglés) cambia el diseño de un sitio web. Podríamos decir que un tema es el front-end de WordPress, mientras que lo que ves en el Escritorio de WordPress es el back-end.


### Qué puede hacer un tema
Los temas toman el contenido y los datos almacenados por WordPress y lo muestran en el navegador. Cuando creas un tema para WordPress, eres tú quien decide cómo se verá el contenido.

### Cuál es la diferencia entre un tema y un plugin
Es normal encontrar características cruzadas en temas y plugins. Sin embargo, las mejores prácticas son:

* un tema controla la presentación del contenido; mientras que
* un plugin controla el comportamiento y las características de un sitio WordPress.

## Index.php y styles.css
El archivo más importante en un tema WordPress es el style.css. En él se definen la información básica del tema. Nombre, Autor, Licencia, Versión de desarrollo, etc. Cada tema ha de ser único en cada instalación de WordPress. La información básica es el nombre del tema. Pero podemos añadir todos estos atributos:

        /*
        Theme Name: Twenty Thirteen
        Theme URI: http://wordpress.org/themes/twentythirteen
        Author: the WordPress team
        Author URI: http://wordpress.org/
        Description: The 2013 theme for WordPress takes us back to the blog, featuring a full range of post formats, each displayed beautifully in their own unique way. Design details abound, starting with a vibrant color scheme and matching header images, beautiful typography and icons, and a flexible layout that looks great on any device, big or small.
        Version: 1.0
        License: GNU General Public License v2 or later
        License URI: http://www.gnu.org/licenses/gpl-2.0.html
        Tags: black, brown, orange, tan, white, yellow, light, one-column, two-columns, right-sidebar, flexible-width, custom-header, custom-menu, editor-style, featured-images, microformats, post-formats, rtl-language-support, sticky-post, translation-ready
        Text Domain: twentythirteen

        This theme, like WordPress, is licensed under the GPL.
        Use it to make something cool, have fun, and share what you've learned with others.
        */
        
Y por supuesto, como su nombre indica, en este fichero escribimos nuestros estilos.

El segundo archivo más importante e imprescindible para un theme es el **index.php**. Es la plantilla principal y en él vamos a empezar a escribir el código de nuestro tema. Este archivo soporta código HTML común siempre y cuando esté fuera de las etiquetas **<?php ?>**.

Es cierto que con estos dos temas podríamos tener nuestro tema completo, pero no es así como WordPress trabaja. Para aprovechar todo el potencial de WordPress vamos a usar todas las plantillas que tenemos disponibles.

## Jerarquía de plantillas
En WordPress las plantillas son los archivos que muestran el aspecto del sitio. Podemos tener tantas plantillas como queramos pero la jerarquía de plantillas básica de WordPress puedes verla en esta imagen:

<a href="https://openwebinars.net/media/django-summernote/2016-02-15/e210735c-43de-4976-b47d-c5d83c9f42f4.png"><img src="https://openwebinars.net/media/django-summernote/2016-02-15/e210735c-43de-4976-b47d-c5d83c9f42f4.png" height="250px"/></a>

Las plantillas parciales básicas son:

- header.php.
- footer.php.
- sidebar.php.
  
El archivo **header.php** incluye el código desde la primera línea hasta la apertura de la etiqueta body. Por su parte, el archivo footer.php incluye el código desde la etiqueta de de cierre del body hasta el final del código html. De la plantilla sidebar.php hablaremos más adelante.

###Usando las plantillas
Dentro de una plantilla WordPress puedes usar las etiquetas de plantillas (Template Tags) para mostrar información dinámicamente, incluir otras plantillas, o personalizar tu sitio.

Al dividir el header y el footer en dos plantillas, podemos incluirlas en la plantilla index.php con las funciones <?php get_header ?> y <?php get_footer ?>, las cuales cargan el contenido de las plantillas parciales en la plantilla principal.

Ejemplo de index.php:

        <?php
        get_header();
        <div class="container">
        <h1>Hola Mundo!</h1>
        </div>
        get_footer();
        ?>

[Más sobre Jerarquía de plantillas]([#%C2%BFQu%C3%A9-es-un-tema](https://developer.wordpress.org/themes/basics/template-hierarchy/))
- [¿Qué es un tema?](#%C2%BFQu%C3%A9-es-un-tema)
  - [Qué puede hacer un tema](#Qu%C3%A9-puede-hacer-un-tema)
  - [Cuál es la diferencia entre un tema y un plugin](#Cu%C3%A1l-es-la-diferencia-entre-un-tema-y-un-plugin)
- [Index.php y styles.css](#Indexphp-y-stylescss)
- [Jerarquía de plantillas](#Jerarqu%C3%ADa-de-plantillas)
- [The loop](#The-loop)
## The loop