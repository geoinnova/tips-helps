[ASPECTOS BÁSICOS DE UN TEMA](#ASPECTOS-B%C3%81SICOS-DE-UN-TEMA)
- [ASPECTOS BÁSICOS DE UN TEMA](#ASPECTOS-B%C3%81SICOS-DE-UN-TEMA)
    - [Diferencia entre un tema y un plugin](#Diferencia-entre-un-tema-y-un-plugin)
  - [Index.php y styles.css](#Indexphp-y-stylescss)
  - [Jerarquía de plantillas](#Jerarqu%C3%ADa-de-plantillas)
    - [Usando las plantillas](#Usando-las-plantillas)
  - [The loop](#The-loop)
    - [Usando el loop](#Usando-el-loop)
  - [Functions.php](#Functionsphp)
    - [Un plugin](#Un-plugin)
    - [Functions.php](#Functionsphp-1)
  - [Incluyendo CSS y JS a nuestro tema](#Incluyendo-CSS-y-JS-a-nuestro-tema)
    - [Enqueuing Scripts y hojas de estilos](#Enqueuing-Scripts-y-hojas-de-estilos)
    - [Hojas de estilos](#Hojas-de-estilos)
    - [Scripts](#Scripts)
  - [Tipos de contenido](#Tipos-de-contenido)
    - [Tipos de contenido por defecto](#Tipos-de-contenido-por-defecto)

# ASPECTOS BÁSICOS DE UN TEMA  
### Diferencia entre un tema y un plugin
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

### Usando las plantillas
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

## The loop
El loop (o bucle)  es el mecanismo por defecto que WordPress usa para mostrar las entradas a través del tema. La cantidad de entradas mostradas es determinada por el Número máximo de entradas a mostrar en el sitio definido en los ajustes de lectura.

El loop extrae la información de cada entrada desde la base de datos e inserta la información apropiada en el lugar de cada etiqueta de plantilla (Template Tag). El código HTML o PHP que esté dentro del loop será procesado para cada entrada.

El loop puede ser usado para varias cosas, por ejemplo:

- Mostrar títulos de entradas y extractos en la página de inicio.
- Mostrar el contenido y los comentarios de una entrada único.
- Mostrar el contenido en una página individual usando etiquetas de plantillas.
- Mostrar información de tipo de contenido personalizado (Custom Post Types) y campos personalizados (Custom Fields).

El loop básico es:

        <?php
        if ( have_posts() ) : while ( have_posts() ) : the_post();
                the_content();
        endwhile;
        else :
                _e( 'Sorry, no posts matched your criteria.', 'textdomain' );
        endif;
        ?>

Este bloque de código nos dice que mientras existan entradas, recorra el bucle mostrándolas. La función have_posts() comrpueba si hay alguna entrada. Si las hubiera, el bucle while sigue ejecutándose mientras la condición sea entre paréntesis sea cierta. Es decir, mientras entradas, el bucle seguirá ejecutándose.

### Usando el loop
El loop debe estar ubicado en el archivo **index.php, y en cualquier otra plantilla que vaya ser usada para mostrar información de las entradas**. Para no duplicar la cabecera una y otra vez, el loop debe estar después de la función get_header(). 

[Lista detallada de todas las etiquetas de plantilla (Template tags)](https://developer.wordpress.org/themes/basics/the-loop/#what-the-loop-can-display)

## Functions.php
El archivo **functions.php** es donde añadiremos las funcionalidades propias de nuestro tema. Este archivo se comporta como un plugin, añadiendo características y funcionalidad a un sitio WordPress. 

Podemos usarlo para llamar a funciones propias de WordPress o crear nuestras propias funciones.

Hay una serie de ventajas y desventajas de usar un plugin o functions.php.

### Un plugin
- Requiere un texto de cabecera específico y único.
- Es almacenado en la carpeta wp-content/plugins, normalmente en un subdirectorio.
- Solo se ejecuta cuando está activo.
- Aplica para todos los temas.
- Debe tener un propósito único.


### Functions.php
- No requiere un texto de cabecera único.
- Es almacenado en el subdirectorio del tema.
- Se ejecuta solo cuando el tema está activo.
- Aplica solo al tema (si se cambia de tema, las características definidas en él no podrán ser usadas).
- Puede tener números bloques de código para diferentes propósitos.


Con **functions.php** podemos:

- Usar los WordPress hooks (ganchos de WordPress).
- Habilitar características de WordPress con la función add_theme_support().
- Definir las funciones que deseemos para usarlas en las plantillas del tema.
  
[Ejemplos de código en functions.php.](https://developer.wordpress.org/themes/basics/theme-functions/#examples)

## Incluyendo CSS y JS a nuestro tema

Añadir estilos y scripts a un tema WordPress es un proceso realmente fácil. Básicamente, tienes que crear una función que añada todos tus scripts y estilos. Añadiéndolos de esta forma, WordPress creará una ruta accesible para que puedas encontrar el archivo y cualquier dependencia necesaria (como jQuery) y así podrás usar un gancho que insertará tus scripts y hojas de estilos.

### Enqueuing Scripts y hojas de estilos
La manera correcta de añadir nuestros scripts y hojas de estilos al tema es añadirlo (enqueue en inglés) en el archivo **functions.php.**

Las funciones básicas son:

- Añadir el script o estilo usando wp_enqueue_script() o wp_enqueue_style().


### Hojas de estilos
En vez de cargar las hojas de estilo en nuestro archivo header.php, tenemos que cargarla usando la **función wp_enqueue_style.**

Para añadir (enqueue) el archivo **styles.css:**

        wp_enqueue_style( 'style', get_stylesheet_uri() );


Para más detalles sobre la función wp_enqueue_style, visita la página del Codex que la detalla. Función [wp_enqueue_style](https://developer.wordpress.org/reference/functions/wp_enqueue_style/)].

### Scripts
Cualquier archivo JavaScript adicional requerido por el tema tiene que ser cargado usando la función **wp_enqueue_script**. Esto asegura la carga y caché correcta, y permite el uso de etiquetas condicionales para usarlas en páginas específicas.

**wp_enqueue_script tiene una síntaxis similar a wp_enqueue_style.**

Para añadir (enqueue) un script en **functions.php**:

        wp_enqueue_script( 'script', get_template_directory_uri() . '/js/script.js', array ( 'jquery' ), 1.1, true);


Para más detalles sobre la función wp_enqueue_script, visita la página del Codex que la detalla. Función [wp_enqueue_script](https://developer.wordpress.org/reference/functions/wp_enqueue_script/)

## Tipos de contenido
Hay varios tipos de contenido en WordPress. Estos tipos de contenidos se describen normalmente como **Post Types**, lo cual puede ser un poco confuso, porque las entradas (posts en inglés) son un tipo de contenido en sí. Para evitar confusiones llamaremos a los Post Types, Tipos de Contenido; y a los Posts, Entradas. Estas son las convecciones que se usan en la comunidad hispana de WordPress.

Internamente, todos los tipos de contenido de WordPress están almacenados en el mismo lugar - en la tabla **wp_posts** de la base de datos - pero están diferenciados por una columna llamada **post_type**.

Adicionalmente a los tipos de contenido por defecto, podmeos crear **Custom Post Types o tipos de contenido personalizados**. Esta característica de WordPress es muy potente, y veremos algún ejemplo durante el curso.

### Tipos de contenido por defecto
Existen cinco tipos de contenido por defecto:

- Entradas (Post Type: ‘post’).
- Páginas (Post Type: ‘page’).
- Medios (Post Type: ‘attachment’).
- Revisión (Post Type: ‘revision’).
- Menú de navegación (Post Type: ‘nav_menu_item’).