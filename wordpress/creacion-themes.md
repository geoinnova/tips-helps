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
- [Plantillas y funcionalidades extra](#Plantillas-y-funcionalidades-extra)
  - [Plantillas para entradas, páginas y medios](#Plantillas-para-entradas-p%C3%A1ginas-y-medios)
    - [Feed y página individual de entradas](#Feed-y-p%C3%A1gina-individual-de-entradas)
    - [Etiquetas de plantilla](#Etiquetas-de-plantilla)
    - [Enlazando plantillas y directorios](#Enlazando-plantillas-y-directorios)
      - [Enlazando a plantillas del tema](#Enlazando-a-plantillas-del-tema)
      - [Enlazando a directorios del tema](#Enlazando-a-directorios-del-tema)
    - [Etiquetas condicionales](#Etiquetas-condicionales)
    - [Dónde usar etiquetas condicionales](#D%C3%B3nde-usar-etiquetas-condicionales)
  - [SIDEBAR](#SIDEBAR)
    - [Registar una Sidebar](#Registar-una-Sidebar)
    - [Mostrar sidebars en nuestro tema](#Mostrar-sidebars-en-nuestro-tema)
    - [Crear la plantilla sidebar.php](#Crear-la-plantilla-sidebarphp)
  - [Widgets](#Widgets)
  - [Menus de navegación](#Menus-de-navegaci%C3%B3n)
    - [Mostrar el Menú](#Mostrar-el-Men%C3%BA)
  - [Paginación y comentarios](#Paginaci%C3%B3n-y-comentarios)
  - [Imágenes destacadas y miniaturas](#Im%C3%A1genes-destacadas-y-miniaturas)
    - [Dar soporte a imágenes destacadas](#Dar-soporte-a-im%C3%A1genes-destacadas)
    - [Establecer una imagen destacada](#Establecer-una-imagen-destacada)
    - [Tamaño de las imágenes](#Tama%C3%B1o-de-las-im%C3%A1genes)
  - [Internacionalización, localización y accesibilidad](#Internacionalizaci%C3%B3n-localizaci%C3%B3n-y-accesibilidad)
    - [Cómo internacionalizar tu tema](#C%C3%B3mo-internacionalizar-tu-tema)
    - [Variables](#Variables)
    - [Localizar](#Localizar)
    - [Archivos MO](#Archivos-MO)
    - [Accesibilidad](#Accesibilidad)
- [Underscores, starter theme](#Underscores-starter-theme)
  - [Empieza a trabajar con _s](#Empieza-a-trabajar-con-s)
    - [Directorio raíz](#Directorio-ra%C3%ADz)
    - [Entradas](#Entradas)
    - [Páginas](#P%C3%A1ginas)
    - [Archivo, Resultados de búsqueda y páginas de error](#Archivo-Resultados-de-b%C3%BAsqueda-y-p%C3%A1ginas-de-error)
    - [Plantilla por defecto](#Plantilla-por-defecto)
    - [Plantilla de comentarios](#Plantilla-de-comentarios)
    - [Archivo functions](#Archivo-functions)
    - [Hojas de estilos](#Hojas-de-estilos-1)
    - [Captura de pantalla](#Captura-de-pantalla)
    - [Carpetas dentro del directorio raíz](#Carpetas-dentro-del-directorio-ra%C3%ADz)
    - [Directorio “inc”](#Directorio-inc)
    - [Directorio “js”](#Directorio-js)
    - [Directorio “languages”](#Directorio-languages)
    - [Directorio “layouts”](#Directorio-layouts)
  - [Temas padres y temas hijos](#Temas-padres-y-temas-hijos)
    - [Qué es un tema padre](#Qu%C3%A9-es-un-tema-padre)
    - [Qué es un tema hijo](#Qu%C3%A9-es-un-tema-hijo)
    - [Cómo crear un tema hijo](#C%C3%B3mo-crear-un-tema-hijo)
  - [Temas premium](#Temas-premium)

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

# Plantillas y funcionalidades extra
## Plantillas para entradas, páginas y medios 
Las plantillas son el músculo de nuestro tema. Los archivos de las plantillas son código PHP que controlan el contenido mostrado al visitante. Estos archivos también generan el HTML para el navegador que controlan como se muestra el contenido. WordPress decide qué plantilla ha de ser usada en cada petición de contenido.

Existen una cantidad determinada de plantillas que podemos llegar a crear en nuestro blog para que WordPress pueda responder a todas las peticiones de contenido con una de estas plantillas. Además, podemos añadir cuántas plantillas personalizadas queramos.

### Feed y página individual de entradas

El **feed** de WordPress es la plantilla que muestra todas las entradas ordenadas por orden cronológico descendente por defecto. 

El **loop** de WordPress, es el que devuelve el feed. La forma correcta de implementar el feed es en el archivo **front-page.php**. 

  La plantilla **front page** se cargará cuando se seleccione como página principal una página estática en **Ajustes -> Lectura**. Si tenemos seleccionado el ajuste por defecto para que WordPress muestre como página principal nuestras últimas entradas, tenemos que crear el archivo **home.php**. 
  
  Muchos desarrolladores se ahorran este proceso utilizando el archivo **index.php** como feed y una plantilla personalizada como página de inicio.

La plantilla que debemos usar para mostrar una **entrada completa** tiene que ser implementada en el archivo **single.php**. WordPress usa esta plantilla para todas las consultas en el caso de que exista una plantilla para dicha consulta. Por ejemplo, si hemos creado un Custom Post Type para Eventos y no existe la plantilla single-eventos.php WordPress usará single.php para cargar el contenido del Post Type Eventos.

Ejemplo de **single.php** extraído del tema TwentySixteen:

    <?php
    get_header(); ?>

    <div id="primary" class="content-area">
        <main id="main" class="site-main" role="main">
            <?php
            // Start the loop.
            while ( have_posts() ) : the_post();

                // Include the single post content template.
                get_template_part( 'template-parts/content', 'single' );

                // If comments are open or we have at least one comment, load up the comment template.
                if ( comments_open() || get_comments_number() ) {
                    comments_template();
                }

                if ( is_singular( 'attachment' ) ) {
                    // Parent post navigation.
                    the_post_navigation( array(
                        'prev_text' => _x( '<span class="meta-nav">Published in</span><span class="post-title">%title</span>', 'Parent post link', 'twentysixteen' ),
                    ) );
                } elseif ( is_singular( 'post' ) ) {
                    // Previous/next post navigation.
                    the_post_navigation( array(
                        'next_text' => '<span class="meta-nav" aria-hidden="true">' . __( 'Next', 'twentysixteen' ) . '</span> ' .
                            '<span class="screen-reader-text">' . __( 'Next post:', 'twentysixteen' ) . '</span> ' .
                            '<span class="post-title">%title</span>',
                        'prev_text' => '<span class="meta-nav" aria-hidden="true">' . __( 'Previous', 'twentysixteen' ) . '</span> ' .
                            '<span class="screen-reader-text">' . __( 'Previous post:', 'twentysixteen' ) . '</span> ' .
                            '<span class="post-title">%title</span>',
                    ) );
                }

                // End of the loop.
            endwhile;
            ?>

        </main><!-- .site-main -->

        <?php get_sidebar( 'content-bottom' ); ?>

    </div><!-- .content-area -->

    <?php get_sidebar(); ?>
    <?php get_footer(); ?>

### Etiquetas de plantilla

En el ejemplo anterior se puede ver el uso de varias etiquetas de plantilla. Las etiquetas de plantilla (o Template Tags en inglés) se usan dentro de un tema WordPress para recuperar el contenido de la base de datos. El contenido puede ser desde el título de un blog a una sidebar completa. Las etiquetas de plantilla son la mejor forma de traer el contenido a nuestro tema porque:

    - Pueden mostrar contenido dinámico.
    - Pueden ser usando en múltiples archivos de plantillas.
    - Separan el tema en secciones más pequeñas y comprensibles.


Una Template Tag se divide en tres componentes:

    - Una etíqueta de código PHP.
    - Una función de WordPress.
    - Parámetros opcionales.



Se puede usar una **Template Tag** para llamar a otro archivo del tema o para extraer información de la base de datos.

Por ejemplo, la Template Tag **get_header()** le dice a WordPress que obtenga el archivo header.php y lo incluya en el archivo actual. Lo mismo que get_footer() hace para el archivo footer.php.

Hay otro tipo de etiquetas de plantilla:

    - **the_title() **- le dice a WordPress que obtenga el título de la página o entrada desde la base de datos y lo incluya.
    - **bloginfo('name')** - le dice a WordPress que obtenga el título del blog de la base de datos y lo incluya en el archivo actual.


Algunas etiquetas de plantilla te permiten pasarle parámetros. Los parámetros son información extra que determina qué será extraído de la base de datos.

Por ejemplo, la Template Tag bloginfo() permite que se le pase un parámetro para indicar qué información se desea. Para mostrar el nombre del blog, solo tienes que pasar un parámetro llamado 'name':

    bloginfo( 'name' )

Para mostrar la versión de WordPress que está corriendo en el blog, tienes que pasar el parámetro 'version':

    bloginfo( 'version' )

En el Codex encontrarás una lista detallada de los parámetros que se le pueden pasar a cada Template Tag. [Lista de Template Tags.](https://codex.wordpress.org/Template_Tags)

### Enlazando plantillas y directorios

#### Enlazando a plantillas del tema

Como ya hemos aprendido anterioremente, un tema WordPress está compuesto por un número diferente de plantillas. Como mínimo, suelen incluir los archivos **sidebar.php, header.php y footer.php**. Estos archivos son referenciados a lo largo del tema usando etiquetas de plantilla, por ejemplo:

    - get_header( 'plantilla_personalizada' );
    - get_footer( 'plantilla_personalizada' );
    - get_sidebar( 'plantilla_personalizada' );


WordPress crea páginas ensamblando varios archivos. Aparte de los archivos básicos para el header, footer y la sidebar, puedes crear plantillas personalizadas y referenciarlas desde cualquier lugar de la página usando la función **get_template_part()**. Para crear una plantilla personalizada tienes que darle al archivo el nombre correcto y usar el mismo sistema de plantillas personalizado que con los archivos header, sidebar y footer:

    slug-template.php

Por ejemplo, si quisieras crear una **plantilla personalizada para manejar el contenido de una entrada** puedes crear una plantilla llamada **content.php** y entonces añadir un diseño específico para el contenido de una publicación personalizada (Custom Post Type) extendiendo el nombre del archivo a **content-product.php**. Entonces, podrás acceder a esta nueva plantilla con esta función:

    get_template_part( 'content', 'product' );

Un ejemplo que veíamos en el código del archivo **single.php** del tema TwentySixteen:

    // Include the single post content template.
    get_template_part( 'template-parts/content', 'single' );


#### Enlazando a directorios del tema

Para enlazar a un directorio del tema, puedes usar las siguientes funciones:

    - get_template_directory_uri();
    - get_stylesheet_directory_uri();


Si no estás usando un tema hijo ambas funciones devolverán lo mismo, la URI completa a la carpeta principal de tu tema. Puedes usar estas funciones para referenciar sub-carpetas en tu tema:

    echo get_template_directory_uri() . '/images/logo.png';

En cambio, si estás usando un tema hijo, la función **get_stylesheet_directory_uri()** devolverá la URI de tu tema hijo, mientras que **get_template_directory_uri()** devolverá la URI de tu tema padre.

### Etiquetas condicionales
Las etiquetas condicionales (Conditional Tags) se usan para **alterar la visualización del contenido dependiendo de las condiciones que coincidan en la página actual**. Le dan la información a WordPress de qué código mostrar bajo unas condiciones específicas. Las etiquetas condicionales normalmente trabajan con la sentencia condicional if / else de PHP.

Por ejemplo, puedes preguntar si un usuario está logueado, y entonces darle un saludo diferente dependiendo del resultado.

    if ( is_user_logged_in() ):
        echo 'Welcome, registered user!';
    else:
        echo 'Welcome, visitor!';
    endif;


### Dónde usar etiquetas condicionales

Para poder usar una etiqueta condicional, la información debe estar cargada de la base de datos, por ejemplo, la consulta debe estar ejecutada. Si usas una etiqueta condicional antes de que haya información, no habrá nada que comprobar en la sentencia if / else.

Es importante saber que WordPress **carga el archivo functions.php antes que ninguna consulta**, así que si incluyes una etiqueta condicional en este archivo, no funcionará.

Dos formas de implementar etiquetas condicionales son:

    - Colocarlas en un archivo de plantilla.
    - Crear una función fuera del functions.php que “enganche” en una acción o filtro y sea lanzada en un momento posterior.

Para una lista detallada de todas las etiquetas condicionales visita el siguiente enlace. [Etiquetas condicionales.](https://codex.wordpress.org/Template_Tags)

## SIDEBAR
Una sidebar es una zona donde podemos colocar widgets en nuestro tema. No es obligatorio añadir una sidebar a nuestro tema, pero hacerlo permite a los editores y otros usuarios de WordPress poder añadir contenido a las zonas de widgets a través del Customizer (Personalizador) o en el panel de administración de widgets.

Los widgets pueden utilizarse para varios propósitos, que van desde listar las entradas recientes hasta habilitar un chat en vivo.


### Registar una Sidebar
Para usar una sidebar, tenemos que registrarla en el archivo **functions.php.**

Para empezar, la función **register_sidebar()** tiene varios parámetros que deben ser definidos independientemente de que estén marcados como opcionales.

- name - nombre de la sidebar. El nombre que los usuarios verán en el panel de Widgets.
- id - debe ser en minúsculas. Puedes referenciar esta sidebar usando la función dynamic_sidebar y este id.
- description - Descripción de la sidebar. También se mostrará en el panel de administración de widgets.
- class - El nombre de la clase CSS para asignar al código HTML del widget.
- before_widget - Código HTML que se establecerá antes de cada widget.
- after_widget - Código HTML que se establecerá después de cada widget. Se debe usar para cerrar las etiquetas de before_widget.
- before_title - Código HTML que se establecerá antes del título de cada widget, como una especie de cabecera (header) de etiqueta.
- afer_title - Código HTML que se establecerá después de cada título. Se debe usar para cerrar las etiquetas de before_title.


Para registrar una sidebar usamos la función **register_sidebar y la función widgets_init**.

    function themename_widgets_init() {
        register_sidebar( array(
            'name'          => __( 'Primary Sidebar', 'theme_name' ),
            'id'            => 'sidebar-1',
            'before_widget' => '<aside id="%1$s" class="widget %2$s">',
            'after_widget'  => '</aside>',
            'before_title'  => '<h1 class="widget-title">',
            'after_title'   => '</h1>',
        ) );

        register_sidebar( array(
            'name'          => __( 'Secondary Sidebar', 'theme_name' ),
            'id'            => 'sidebar-2',f
            'before_widget' => '<ul><li id="%1$s" class="widget %2$s">',
            'after_widget'  => '</li></ul>',
            'before_title'  => '<h3 class="widget-title">',
            'after_title'   => '</h3>',
        ) );
    }
    add_action( 'widgets_init', 'themename_widgets_init' );


Al registrar una sidebar le decimos a WordPress que estamos creando una zona de widgets en Apariencia -> Widgets dónde los usuarios pueden arrastrar sus widgets. Hay dos funciones para registrar una sidebar:

- register_sidebar().
- register_sidebars().

La primera nos permite registrar una sidebar y la segunda múltiples de ellas.

### Mostrar sidebars en nuestro tema
Una vez que registramos nuestra sidebar, necesitamos una forma de mostrarlas en nuestro tema. Para hacerlo, hay dos pasos:

- Crear el archivo de plantilla **sidebar.php** y mostrar la sidebar usando la función **dynamic_sidebar.**
- Cargarla en tu tema usando la función **get_sidebar**.


### Crear la plantilla sidebar.php
Una plantilla sidebar contiene el código de nuestra sidebar. WordPress reconoce el archivo sidebar.php y cualquier plantilla con el tema **sidebar-{name}.php**. Esto significa que podemos organizar nuestros archivos para que cada plantilla contenga una sidebar.

En el ejemplo de la plantilla single.php del tema TwentySixteen se hace referencia a una sidebar por su id:

    <?php get_sidebar( 'content-bottom' ); ?>

## Widgets
Un widget añade contenido y características a una sidebar. Las zonas de widgets proveen una forma de personalizar su sitio a los usuarios. Una zona de widgets puede aparecer en múltiples páginas o solo en una página. Tu tema puede tener una zona de widgets o todas las que quieras.

Algunos ejemplos de usos de zonas de widgets son:

- Diseñar una página de inicio usando widgets. Esto permite a los propietarios del sitio decidir qué debe aparecer en cada seción de su página de inicio.
- Crear un pie de página (footer) que los usuarios puedan personalizar con su propio contenido.
- Añadir una sidebar personalizable al blog.


Un widget es un **objeto PHP que puede mostrar código HTML**. El mismo tipo de widget puede ser usado varias veces en la misma página, por ejemplo un widget de texto puede repetirse con el mismo o distinto contenido en la misma sidebar varias veces. Los widgets pueden guardar información en la base de datos (en la tabla **wp_options**).

Cuando creamos un nuevo widget, aparecerá en la sección **Apariencia -> Widgets** de nuestro WordPress. Los ususarios pueden añadir un widget a una zona de widgets y personalizar la configuración del widget desde el Escritorio de WordPress.

## Menus de navegación
Para poder crear/modificar nuestro menú desde el Escritorio de WordPress tenemos que añadirlo programáticamente. Realmente no estaremos creando un menú, sino dando soporte a nuestro tema para usar menús de navegación dinámicos.

Para registrar un menú, de nuevo tenemos que acudir a nuestro archivo **functions.php** y registar nuestro menú.

Usaremos la función register_nav_menus() para registrar un menú.

      function register_my_menus() {
        register_nav_menus(
          array(
            'header-menu' => __( 'Header Menu' ),
            'extra-menu' => __( 'Extra Menu' )
          )
        );
      }
      add_action( 'init', 'register_my_menus' );

En este ejemplo, se han añadido dos localizaciones a la pestaña “Gestionar localizaciones” en Apariencia -> Menus. Estas localizaciones son “Header Menu” y “Extra Menu”. Podremos crear tantas localizaciones como necesitemos, evaluando qué tipos de menús vamos a utilizar en nuestro tema.

### Mostrar el Menú
Una vez que lo hemos registrado, tenemos que usar la función **wp_nav_menu()** para decirle a nuestro tema dónde mostrar el menú. Por ejemplo, añadir la siguiente línea de código a nuestro archivo header.php para mostrar el header-menu anteriormente registrado:

    wp_nav_menu( array( 'theme_location' => 'header-menu' ) );


[Referencia de la función wp_nav_menu.](https://developer.wordpress.org/themes/basics/conditional-tags/#function-reference)

## Paginación y comentarios
La paginación permite al lector ir hacia atrás y hacia adelante a través de múltiples páginas de contenido.

WordPress puede usar la paginación cuando:

- Estás viendo una lista de entradas y existen más entradas de las que caben en una página.
- “Rompes” un mensaje más largo de lo deseado manualmente usando la etiqueta <!--nextpage-->.


**El uso más común de la paginación en WordPress** es el de dividir la lista de entradas en páginas separadas. Si estás viendo una categoría, página de archivo o el feed por defecto, WordPress solo muestra **10 entradas por defecto**. Los usuarios pueden **cambiar el número** de entradas que aparecen en cada página en la sección **Ajustes -> Lectura.**

En este ejemplo se muestra dónde puedes añadir las funciones de paginación para el loop principal. Añade las funciones antes o después del loop:


    <?php if ( have_posts() ) : ?>

        <!-- Add the pagination functions here. -->

        <!-- Start of the main loop. -->
        <?php while ( have_posts() ) : the_post(); ?>

        <!-- the rest of your theme's main loop -->

        <?php endwhile; ?>
        <!-- End of the main loop -->

        <!-- Add the pagination functions here. -->

      <div class="nav-previous alignleft"><?php next_posts_link( 'Older posts' ); ?></div>
      <div class="nav-next alignright"><?php previous_posts_link( 'Newer posts' ); ?></div>

    <?php else : ?>

    <?php _e('Sorry, no posts matched your criteria.'); ?>

    <?php endif; ?>

## Imágenes destacadas y miniaturas
Las imágenes destacadas son imágenes que representan a una entrada, página o tipo de contenido personalizado. Cuando creamos un tema, puedes mostrar la imagen destacada de formas diferentes, en la página de Archivo, en la cabecera, arriba de un post, por ejemplo.

### Dar soporte a imágenes destacadas
Los temas tienen que declarar el soporte para las imágenes destacadas antes de que la interface de imágenes destacadas aparezca en la pantalla de edición. El soporte para imágenes destacadas es declarado poniendo la siguiente línea en el archivo **functions.php** de nuestro tema:

    add_theme_support( 'post_thumbnails' );

### Establecer una imagen destacada
Una vez que hayamos añadido soporte para imágenes destacadas, podremos asignar una imagen destacada a una entrada o página en la pantalla de edición de la misma.

### Tamaño de las imágenes
El tamaño por defecto de las imágenes de WordPress son “Miniatura”, “Mediano”, “Grande” y “Tamaño Completo” (el tamaño original de la imagen cargada). Estos tamaños de imagen pueden ser configurados en el Escritorio de WordPress bajo **Ajustes -> Medios.** También podemos definir nuestros propios tamaños de imagen pasando un array con las dimensiones de la imagen.:

    the_post_thumbnail(); // Sin parámetro -> Miniatura
    the_post_thumbnail( 'thumbnail' ); // Miniatura (por defecto 150px x 150px max)
    the_post_thumbnail( 'medium' ); // Resolución media (por defecto 300px x 300px max)
    the_post_thumbnail( 'large' ); // Resolución grande (por defecto 640px x 640px max)
    the_post_thumbnail( 'full' ); // Resolución de la imagen original (Sin modificar)
    the_post_thumbnail( array( 100, 100 ) ); // Otras resoluciones (alto, ancho)

## Internacionalización, localización y accesibilidad
Internacionalización es el proceso de desarrollar un tema fácilmente traducible en otros lenguajes. Internacionalización se abrevia normalmente por i18n (porque hay 18 letras entre la i y la n).
 
### Cómo internacionalizar tu tema
Para hacer las cadenas de caracteres traducibles tenemos que **encerrar las cadenas originales en una llamada** a un conjunto de funciones especiales.

La función básica que usaremos para internacionalizar nuestro tema es **__()**. A esta función le pasaremos dos parámetros, el primero es la cadena a traducir, y el segundo es el dominio del texto, es decir, el identificador que le dirá a WordPress a dónde pertenece esa cadena.

**El dominio del texto debe coincidir con el slug del tema**. Si el nombre del tema es Mi tema o está en una carpeta llamada mi-tema, el nombre de dominio debe ser mi-tema.

Cadena de ejemplo:

    __( $text, $text_domain );
    __('String(texto a internacionalizar)', 'mi-tema' );

### Variables
Si estamos usando variables en una cadena tenemos que usar un placeholder. Por ejemplo:

    echo "Tu ciudad es $ciudad."

Usa la función printf:

    printf(
    __( 'Tu diudad es %s.', 'mi-tema' ),
    $ciudad
    );

Existe una amplia gamas de funciones para internacionalizar cadenas, échale un vistazo a la lista en la documentación. 
[Funciones de localización](https://developer.wordpress.org/themes/functionality/internationalization/#localization-functions)

### Localizar
Localizar (localization en inglés) es el proceso de traducir un tema internacionalizable. Se abrevia como l10n (porque hay 10 letras entre la l y la n).

Archivos de localización
Archivos PO

Cada traductor toma un archivo POT y traduce la sección msgstr en su propio idioma. El resultado es un archivo PO con el mismo formato que el POT, pero con las traducciones y cabeceras específicas del lenguaje. Hay un archivo PO por cada lenguaje en un tema.

### Archivos MO

De cada archivo PO traducido se genera un archivo MO. Estos archivos legibles por la máquina son binarios que las funciones gettext usan, y son una versión “compilada” de un archivo PO.

Echa un vistazo a la documentación sobre cómo generar archivos MO y POT. Generar archivos POT.

### Accesibilidad
Un tema de WordPress debe generar páginas que todo el mundo pueda usar, incluyendo aquellos que no pueden ver o usar un ratón. Aunque la accesibilidad web puede ser un tema complejo, se reduce a cuatro principios básicos. El contenido debe ser:

- Perceptible : El contenido debe estar disponible para todos.
- Operable : Los usuarios deben ser capaces de moverse por el sitio y operar en él de manera efectiva.
- Entendible : El contenido debe ser presentado de una manera que apoye el entendimiento.
- Robusto : El contenido debe estar igual de disponible para un rango amplio de usuarios.


Te recomiendo que sigas las Pautas de [Accesibilidad de la W3C. WCAG 2.0](http://www.codexexempla.org/traducciones/pautas-accesibilidad-contenido-web-2.0.htm)

# Underscores, starter theme
Underscores, también conocido **como _s**, es un starter theme Open Source creado principalmente por desarrolladores de Automattic. 
**Un starter theme es un tema creado por desarrolladores experimentados que te ahorran gran cantidad de trabajo**, ya que suele tener implementado las plantillas y características básicas que necesitamos en un theme.

Las características de **Underscores** son:

- Una buena cantidad de plantillas HTML5 livianas, bien documentadas y modernas.
- Una plantilla 404 muy útil.
- Una implementación de una cabecera personalizada en inc/custom-header.php que puede ser activada con solo descomentar una línea de código en functions.php y añadir el bloque de código que se encuentra en los comentarios del archivo inc/custom-header.php al archivo header.php.
- Etiquetas de plantilla personalizadas en inc/template-tags.php que mantienen las plantillas limpias y previenen la duplicación de código.
- Pequeños tweaks en inc/extras.php que pueden mejorar la experiencia en el desarrollo del tema.
- Un script en js/navigation.js que adaptan el menú de navegación para dispositivos móviles. Solo te tienes que preocupar de darle los estilos que necesite.
- Dos ejemplos de diseños en CSS en la carpeta layouts/ para una sidebar en cada lateral del contenido.
- Estilos CSS bien organizados e inteligentes en el archivo styles.css que nos ayudarán a crear un diseño rápidamente.


Para crear un tema basado en _s solo tenemos que ir a **underscores.me** y generar nuestro tema basado en _s. Con solo poner el nombre del tema que queremos crear y pulsar en el botón “Generate” tendremos nuestro starter theme listo para empezar a crear.

## Empieza a trabajar con _s
Cómo organices los archivos de tu tema es algo que irás depurando con el tiempo. Con la excepción de uno o dos archivos, la disposición de los archivos no tiene límite si ya tienes una base con PHP. Pero tienes que encontrar el equilibrio entre tú método de organización de archivos, fácil de usar para tus usuarios (porque ellos podrán crear temas hijos), y el simple sentido común.

Por ahora veamos cómo es la estructura de archivos de Underscores y cómo usarla, incluyendo funciones extra.

### Directorio raíz
Al descargar Underscores por primera vez, podría asustarnos la cantidad de archivos que encontramos en el tema. No te preocupes, la mayoría de ellos se explican solo con su nombre de archivo. Y otros pueden agruparse porque tienen un comportamiento similar.

La estructura principal de archivos HTML manejan la cabecera, el pie de página, la columna de contenido y el área de widgets del sitio. Como bien sabes, el código HTML de cada elemento se encuentran en los archivos header.php, footer.php y sidebar.php. Por defecto, el archivo que carga el contenido es el index.php. Normalmente colocaremos el contenido en una columna y la sidebar en otra.

WordPress sabe que este archivo es el último recurso. En su lugar, busca otros archivos en la raíz del tema por nombre y los usa si tienen un propósito especial.

### Entradas
Cuando se carga una entrada, WordPress busca el archivo single.php para mostrar el contenido. Sin embargo, en Underscores este archivo solo contiene el loop (bucle) para detectar el posts, pero es el archivo content-single.php el que contiene el HTML que se mostrará finalmente.

Al fin y al cabo, los dos archivos se comportan igual, peor se modulariza al crear un archivo para “maquetar” el contenido.

### Páginas
Cuando se carga una página, WordPress busca el archivo page.php para mostrar el contenido. Y de la misma forma que las entradas, carga una plantilla extra para maquetar el contenido en HTML, esta plantilla se encuentra en el archivo content-page.php.

### Archivo, Resultados de búsqueda y páginas de error
La misma funcionalidad aplica a otras plantillas de WordPress basadas en la jerarquía de plantillas. Las principales plantillas a parte de las entradas y páginas serán archive.php, search.php y 404.php.

Estos archivos controlan todas las páginas de Archivo (taxonomías [categorías y etiquetas]), archivos de fecha y archivos de autor), resultados de búsqueda y páginas de error, respectivamente.

### Plantilla por defecto
Si no existiera ninguno de los archivos anteriormente mencionados o la página que se tiene que cargar no corresponde a ninguna plantilla específica de WordPress, WordPress sabe que tiene que recurrer al archivo index.php. Es la plantilla genérica y a prueba de errores, por eso es uno de los archivos obligatorios en todo tema.

Dentro del index.php hay un loop como en cualquier otra plantilla. Sin embargo, este loop llama a la plantilla content.php que sirve como contenido genérico, sin emportar el tipo de contenido cargado. En el caso de que no hubiera ninguna entrada publicada, carga la plantilla content-none.php.

<a href="https://openwebinars.net/media/django-summernote/2016-02-15/d8b919e4-80dc-4165-8009-179edcaaee5d.png"><img src="https://openwebinars.net/media/django-summernote/2016-02-15/d8b919e4-80dc-4165-8009-179edcaaee5d.png" width="300px"></a>

### Plantilla de comentarios
El archivo comments.php es el responsable de mostrar los comentarios, pings y formulario de comentarios. Tanto en la plantilla single.php como en page.php, se usa la función comments_template() para habilitar la funcionalidad de los comentarios. Esta función de WordPress sabe que teine que buscar el archivo comments.php en la raíz del tema.

### Archivo functions
Cómo describíamos en las primeras lecciones de este curso, el archivo functions.php sirve para esteblecer la funcionalidad básica de neustro tema. Además de poder extender la funcionalidad de nuestro tema, en este archivo registramos la zona de wigets, establecemos los tamaños de las miniaturas, y cargamos los recursos del tema como los archivos JavaScript. WordPress lo lee automáticamente, así que lo que pongas en él será tenido en cuenta.

### Hojas de estilos
En la hoja de estilos de Underscores podemos ver toda la información que necesitaríamos detallar para nuestre tema profesional y listo para publicar. Toda la información que se muestra en el Escritorio de WordPress, bajo la sección Apariencia -> Temas, es cargada de este archivo.

Underscores tiene una serie de estilos cargados, que haremos bien en dejar, cuando empecemos a crear los nuestros.

También se incluye otra hoja de estilos en Underscores, es el archivo rtl.css. RTL significa “right to left” o “de derecha a izquierda”. Este archivo se usa para ajustar los estilos del tema para lenguajes que se leen de derecha a izquierda. Normalmente, no requiere de mucho código CSS para hacer este ajuste.

### Captura de pantalla
En el Escritorio de WordPress, concretamente en la página de temas, verás comunmente una captura de pantalla para cada tema. Esta captura de pantalla puede diferenciar tu tema o compañía. WordPress busca el archivo **screenshot.png** para mostrarlo, así que ¡sé creativo!.

### Carpetas dentro del directorio raíz
WordPress no requiere ninguna carpeta en el tema, pero es una buena práctica organizar nuestros archivos en directorios. Underscores viene con las carpetas inc, js, languages, layouts y template-parts.

### Directorio “inc”
Este directorio, abreviatura de “includes”, contiene archivos PHP que son una extensión del archivo functions.php. Incluir otros archivos desde el archivo functions.php asegura que estos se usarán también. Puedes echarle un vistazo a cada archivo, que contiene código de buena calidad y bien documentado para saber qué hace cada archivo.

### Directorio “js”
Este directorio contiene los archivos JavaScript personalizado de tu tema. Incluye los archivos customizer.js, navigation.js y skip-link-focus-fix.js.

### Directorio “languages”
Dependiendo de cómo vayamos a utilizar nuestro tema, tendremos que prepararlo para usar otros idiomas a parte del original. El directorio “languages” es el lugar para proveer las instruciones y archivos necesarios para traducción.

### Directorio “layouts”
Este directorio contiene dos hojas de estilos para configurar las columnas de contenido y sidebar. Underscores sabe que la mayoría de los temas tienen una disposición contenido/sidebar o sidebar/contenido, así que estos dos archivos proveen código CSS de ejemplo para usar cualquiera de estas dos disposiciones.

## Temas padres y temas hijos
Un tema hijo permite cambiar pequeños aspectos de la apariencia de un sitio que todavía preserva la funcionalidad y el diseño del tema original. Para entender cómo funcionan los temas hijos, es importante de entender primero la relación entre temas padres y temas hijos.

### Qué es un tema padre
Un tema padre es un tema completo de WordPress que contiene todas las plantillas requeridas en un tema WordPress y lo necesario para que el tema funcione. Todos los temas (excluyendo los temas hijos) son considerados temas padres.

### Qué es un tema hijo
Un tema hijo hereda el look and feel del tema padre y toda su funcionalidad, pero puede usarse para hacer modificaciones a cualquier parte del tema. De esta forma, separamos las modificaciones de los archivos del tema padre. Usando un tema hijo, podemos seguir actualizando el tema padre sin que esto afecte a las modificaciones hechas en nuestro sitio.

Los temas hijos:

- Hacen nuestras modificaciones portables y replicables.
- Mantienen las modificaciones separadas de las funcionalidades del tema padre.
- Permite que el tema padre se actualice sin destruir las modificaciones.
- Nos ahorra tiempo en el desarrollo ya que no estamos reinventando la rueda.
- Son una gran forma de aprender sobre el desarrollo de temas.

### Cómo crear un tema hijo
1. Crea la carpeta del tema hijo
Primero, tienes que crear una carpeta en el directorio de temas localizado en **wp-content/themes.**

Esta carpeta tiene que llamarse igual que el tema padre, pero seguida de -child. Por ejemplo, para el tema twentysixteen el tema hijo debería ser twentysixteen-child.


2. Crea una hoja de estilos: styles.css
Lo siguiente es crear una hoja de estilos llamada styles.css, la que contendrá todos los estilos y las declaraciones que controlan el diseño de nuestro tema. La hoja de estilos debe contener la cabecera requerida en todo tema WordPress. Como añadido a esta cabecera, tendremos que indicarle el tema padre al que corresponde este tema hijo en la línea “Template”.

    /*
    Theme Name:     Twenty Sixteen Child
    Theme URI:      http://example.com/
    Description:    Child theme for the Twenty Sixteen theme
    Author:         Your name here
    Author URI:     http://example.com/about/
    Template:       twentysixteen
    Version:        0.1.0
    */

3. Crea un archivo functions.php
La mayoría de los archivos de nuestro tema hijo sobreescribirán a los mismos del tema padre. Por ejemplo, el archivo styles.css sobreescribe a los estilos en el mismo archivo del tema padre. Sin embargo, el archivo functions.php es diferente: en vez de sobreescribir la funcionalidad del tema padre, se cargan los dos archivos. Específicamente, el archivo functions.php del tema hijo es cargado antes del functions.php del tema padre.

Crear el functions.php es opcional. Solo se necesita para añadir código PHP adicional al tema. Alternativamente, el código PHP puede estar dentro de un plugin, lo que hace nuestra funcionalidad más portable sin importar el tema que estemos usando.

4. Heredar estilos
A menos que queramos cambiar completamente el diseño de nuestro tema, es recomendable que carguemos todos los estilos del tema padre. Heredar estos estilos nos ahorrará tiempo si solo vamos a hacer cambios menores en el diseño. El no hacerlo nos permitirar usar las plantillas del tema padre para mostrarlas de la forma en la que deseemos, con un diseño totalmente personalizado desde cero.

Para importar los estilos del tema padre tendrás que añadir la siguiente línea al archivo styles.css de tu tema hijo:

@import url(" ../twentysixteen/style.css" );

5. Añadir archivos de plantillas
A diferencia del archivo functions.php, cualquier archivo que añadamos a nuestro tema hijo sobreescribirá el mismo archivo en el tema padre.

En la mayoría de los casos, lo mejor es crear una copia de la plantilla que queramos cambiar y hacer modificaciones sobre esa copia, dejando la plantilla en el tema padre sin cambios.

6. Incluyendo otros archivos
Cuando necesites incluir archivos que estén dentro del directorio de tu tema hijo, tendrás que usar la función get_stylesheet_directory(). Para referenciar al tema padre, tendrías que usar la función get_template_directory().

7. Añadiendo estilos y scripts
Los scripts y estilos tienen que ser añadidos (enqueued) en una función propia, y entonces tienen que ser encerrados en una acción.

WordPress no cargará automáticamente los estilos de tu tema hijo en el front-end. Para ello tienes que cargarlo de la forma que se mostraba en las primeras unidades. Aquí viene un ejemplo para refrescar la memoria. El siguiente código tendrías que añadirlo en el **functions.php** de tu tema:

    <?php
    add_action( 'wp_enqueue_scripts', 'my_plugin_add_stylesheet' );
    function my_plugin_add_stylesheet() {
        wp_enqueue_style( 'my-style', get_stylesheet_directory_uri() . '/style.css', false, '1.0', 'all' );
    }

## Temas premium

Los temas premiums son temas de pago que son mantenidos por sus desarrolladores con regularidad. Los temas premium ofrecen un diseño final, aunque la mayoría de ellos son muy personalizables. Elegir un tema premium puede ser abrumador, puesto que hay miles de ellos. Pero hay algo que siempre has de tener en cuenta, compra siempre temas premium desde marketplaces reputados. Para facilitarte la tarea, te recomendamos esta serie de sitios en los que encontrarás los mejores temas premium:

    www.themeforest.net
    www.elegantthemes.com
    www.mojo-themes.com
    www.woothemes.com

¡Y muchos más! Utilizar temas premium te facilitan mucho trabajo, no reinventas la rueda, y puedes entregar un sitio listo para usar en muy poco tiempo. Algunas ventajas de usar temas premium son:

- Calidad. Una vez que hayas escogido un marketplace reputable, puedes esperar un tema de más alta calidad que un tema gratuito. Esto quiere decir, por ejemplo, que es más exclusivo.
- Funcionalidad. De las mejores cosas que tiene un tema premium, es la gran lista de opciones que puedes encontrar para personalizar el tema, y dotarle de funcionalidades infinitas.
- Seguridad. Esta característica estará presente en un tema premium si has seguido la recomendación de comprarlo en un marketplace reputado y no descargarlo gratuitamente de otro lugar.
- Actualizaciones. Una vez que hayas comprado el tema, recibirás actualizaciones, normalmente durante un año, o en algunos casos indefinidas. Las actualizaciones mantienen la seguridad de tu tema y eliminan tecnologías obsoletas.
- Soporte. De las mejores cosas que obtienes al comprar un tema premium es el soporte por parte de su desarrollador. Además, suelen estar muy bien documentados.

Como decíamos antes, temas premium existen miles, pero si quieres cerrar el círculo, aquí tienes los tres temas premium más conocidos:

  Divi
  Me arriesgaría a decir que Divi es el tema premium más famoso. Es una navaja suiza, un tema muy potente que permite personalizarlo de tal forma que no parezca Divi. Cómo una de sus últimas características, el nuevo Page Builder, que te permitirá crear un diseño totalmente personalizado sin necesidad de código.

  Avada
  Es el tema más vendido en themeforest, que a su vez es el marketplace más famoso. La mejor característica de Avada son la cantidad de Demos que trae consigo. Son como pequeños temas dentro de Avada que te dejan un sitio listo para entregar en muy poco tiempo.

  Flatsome
  Puede que sea el más developer-friendly de los tres. Un tema muy enfocado a eCommerce y que usa shortcodes para casi todo. Puedes usar estos shortcodes tanto en páginas/posts como en plantillas dentro de un tema hijo.