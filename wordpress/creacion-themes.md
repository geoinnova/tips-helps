- [FUNCTIONS.PHP](#FUNCTIONSPHP)
  - [registrar menu (1-1'27'')](#registrar-menu-1-127)
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
  - [Etiquetas condicionales](#Etiquetas-condicionales)
  - [Dónde usar etiquetas condicionales](#D%C3%B3nde-usar-etiquetas-condicionales)

# FUNCTIONS.PHP
## registrar menu (1-1'27'')


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

## Enlazando plantillas y directorios

### Enlazando a plantillas del tema

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


##Enlazando a directorios del tema

Para enlazar a un directorio del tema, puedes usar las siguientes funciones:

    - get_template_directory_uri();
    - get_stylesheet_directory_uri();


Si no estás usando un tema hijo ambas funciones devolverán lo mismo, la URI completa a la carpeta principal de tu tema. Puedes usar estas funciones para referenciar sub-carpetas en tu tema:

    echo get_template_directory_uri() . '/images/logo.png';

En cambio, si estás usando un tema hijo, la función **get_stylesheet_directory_uri()** devolverá la URI de tu tema hijo, mientras que **get_template_directory_uri()** devolverá la URI de tu tema padre.

## Etiquetas condicionales
Las etiquetas condicionales (Conditional Tags) se usan para **alterar la visualización del contenido dependiendo de las condiciones que coincidan en la página actual**. Le dan la información a WordPress de qué código mostrar bajo unas condiciones específicas. Las etiquetas condicionales normalmente trabajan con la sentencia condicional if / else de PHP.

Por ejemplo, puedes preguntar si un usuario está logueado, y entonces darle un saludo diferente dependiendo del resultado.

    if ( is_user_logged_in() ):
        echo 'Welcome, registered user!';
    else:
        echo 'Welcome, visitor!';
    endif;


## Dónde usar etiquetas condicionales

Para poder usar una etiqueta condicional, la información debe estar cargada de la base de datos, por ejemplo, la consulta debe estar ejecutada. Si usas una etiqueta condicional antes de que haya información, no habrá nada que comprobar en la sentencia if / else.

Es importante saber que WordPress **carga el archivo functions.php antes que ninguna consulta**, así que si incluyes una etiqueta condicional en este archivo, no funcionará.

Dos formas de implementar etiquetas condicionales son:

    - Colocarlas en un archivo de plantilla.
    - Crear una función fuera del functions.php que “enganche” en una acción o filtro y sea lanzada en un momento posterior.

Para una lista detallada de todas las etiquetas condicionales visita el siguiente enlace. [Etiquetas condicionales.](https://codex.wordpress.org/Template_Tags)

#SIDEBAR
Hemos referenciado a la sidebar varias veces pero aún no hemos definido qué es una sidebar (barra lateral). Una sidebar es una zona donde podemos colocar widgets en nuestro tema. No es obligatorio añadir una sidebar a nuestro tema, pero hacerlo permite a los editores y otros usuarios de WordPress poder añadir contenido a las zonas de widgets a través del Customizer (Personalizador) o en el panel de administración de widgets.

Los widgets pueden utilizarse para varios propósitos, que van desde listar las entradas recientes hasta habilitar un chat en vivo.


Registar una Sidebar
Para usar una sidebar, tenemos que registrarla en el archivo functions.php.

Para empezar, la función register_sidebar() tiene varios parámetros que deben ser definidos independientemente de que estén marcados como opcionales.

name - nombre de la sidebar. El nombre que los usuarios verán en el panel de Widgets.

id - debe ser en minúsculas. Puedes referenciar esta sidebar usando la función dynamic_sidebar y este id.

description - Descripción de la sidebar. También se mostrará en el panel de administración de widgets.

class - El nombre de la clase CSS para asignar al código HTML del widget.

before_widget - Código HTML que se establecerá antes de cada widget.

after_widget - Código HTML que se establecerá después de cada widget. Se debe usar para cerrar las etiquetas de before_widget.

before_title - Código HTML que se establecerá antes del título de cada widget, como una especie de cabecera (header) de etiqueta.

afer_title - Código HTML que se establecerá después de cada título. Se debe usar para cerrar las etiquetas de before_title.


Para registrar una sidebar usamos la función register_sidebar y la función widgets_init.

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
        'id'            => 'sidebar-2',
        'before_widget' => '<ul><li id="%1$s" class="widget %2$s">',
        'after_widget'  => '</li></ul>',
        'before_title'  => '<h3 class="widget-title">',
        'after_title'   => '</h3>',
    ) );
}
add_action( 'widgets_init', 'themename_widgets_init' );


Al registrar una sidebar le decimos a WordPress que estamos creando una zona de widgets en Apariencia -> Widgets dónde los usuarios pueden arrastrar sus widgets. Hay dos funciones para registrar una sidebar:

register_sidebar().

register_sidebars().
La primera nos permite registrar una sidebar y la segunda múltiples de ellas.


Mostrar sidebars en nuestro tema
Una vez que registramos nuestra sidebar, necesitamos una forma de mostrarlas en nuestro tema. Para hacerlo, hay dos pasos:

Crear el archivo de plantilla sidebar.php y mostrar la sidebar usando la función dynamic_sidebar.

Cargarla en tu tema usando la función get_sidebar.


Crear la plantilla sidebar.php
Una plantilla sidebar contiene el código de nuestra sidebar. WordPress reconoce el archivo sidebar.php y cualquier plantilla con el tema sidebar-{name}.php. Esto significa que podemos organizar nuestros archivos para que cada plantilla contenga una sidebar.

En el ejemplo de la plantilla single.php del tema TwentySixteen se hace referencia a una sidebar por su id:

<?php get_sidebar( 'content-bottom' ); ?>