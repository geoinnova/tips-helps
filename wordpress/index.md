# Creación de plugins en wordpress


# Hooks
	
http://hookr.io/all/#index=a


## Obtener los datos del post actual

    $post_actual = $wp_query->get_queried_object();
    echo $post_actual->post_title;
	echo $post_actual->guid;
	echo $post_actual->post_content;

https://codex.wordpress.org/es:Referencia_de_Funcion/wp_get_post_tags

https://developer.wordpress.org/reference/functions/get_the_id/
https://www.it-swarm.dev/es/wordpress/como-obtener-el-nombre-de-la-pagina-actual-en-wordpress/972113438/
https://kinsta.com/es/blog/wordpress-get_posts/



## WooCommerce Single Product Page Hooks: Visual Guide
https://www.businessbloomer.com/woocommerce-visual-hook-guide-single-product-page/

<img src="images/hook.jpg" height="250px"/>

## Botones de compartir desde el producto
https://mariasaez.com/wp-admin/options-general.php?page=sharing

Jetpack>Ajustes>Compartir

## Woocommerce - Personalizar las páginas de producto
https://www.webempresa.com/blog/personalizar-fichas-de-producto-woocommerce.html

modificar: content-single-products.php y single-products.php

https://boluda.com/tutorial/como-modificar-las-plantillas-de-woocommerce-correctamente/

## Incluir iconos sociales a una página creada dinámicamente

Dentro del theme-child > page-participantes.php (pagina creada)

    Incluir en la zona donde queramos mostrarlo (en mi caso antes del footer)
            <?php get_template_part('page-parts/social-share'); ?>
    

/page-parts/social-share.php
    
    <?php 
    global $wp;
    $url_actual = home_url( add_query_arg( array(), $wp->request ) );
    ?>
    <section class="main-color container-wrap social-share-wrap">
        <div class="container">
            <div class="share-links">

                <div class="hr-title hr-long"><abbr>Compartir</abbr></div>
                    <span class="kleo-facebook">
                        <a href="http://www.facebook.com/sharer.php?u=<?php echo $url_actual; ?>" class="post_share_facebook"       
                        onclick="javascript:window.open(this.href,'', 'menubar=no,toolbar=no,resizable=yes,scrollbars=yes,height=220,width=600');
                        return false;">
                            <i class="icon-facebook"></i>
                        </a>
                    </span>

                    <span class="kleo-twitter">
                        <a href="https://twitter.com/share?url=<?php echo $url_actual; ?>" class="post_share_twitter" 
                        onclick="javascript:window.open(this.href,'', 'menubar=no,toolbar=no,resizable=yes,scrollbars=yes,height=260,width=600');
                        return false;">
                            <i class="icon-twitter"></i>
                        </a>
                    </span>

                    <span class="kleo-whatsapp visible-xs-inline visible-sm-inline">
                        <a href="whatsapp://send?text=<?php echo $url_actual; ?>" data-action="share/whatsapp/share">
                            <i class="icon-whatsapp"></i>
                        </a>
                    </span>

                    <span class="kleo-whatsapp visible-xs-inline visible-sm-inline">
                            <a href="//telegram.me/share/url?url=<?php echo $url_actual; ?>">
                                <i class="icon-paper-plane"></i>
                            </a>
                    </span>


                    <span class="kleo-mail">
                        <a href="mailto:?subject=VERSIÓN ORIGINAL&amp;body=<?php echo $url_actual; ?>" class="post_share_email">
                            <i class="icon-mail"></i>
                        </a>
                    </span>          
            </div>
        </div>
    </section>
    

## Convertir woocommerce en catálogo
https://www.webempresa.com/blog/activar-modo-catalogo-en-woocommerce.html

            #### Cómo activar el modo catálogo sin plugins

            Si quieres evitar instalar un plugin, una simple línea de código va a convertir tu ecommerce en un catálogo de la misma forma que los anteriores.
            Para ello sólo tienes que copiar el siguiente código en el funtions.php de tu tema.

            remove_action( 'woocommerce_after_shop_loop_item',
            'woocommerce_template_loop_add_to_cart', 10 );

            remove_action( 'woocommerce_single_product_summary', 
            'woocommerce_template_single_add_to_cart', 30 );

            remove_action( 'woocommerce_simple_add_to_cart',
            'woocommerce_simple_add_to_cart', 30 );

            remove_action( 'woocommerce_grouped_add_to_cart',
            'woocommerce_grouped_add_to_cart', 30 );

    
    

## Crear theme child y modificación de archivos de theme
[Video explicativo](https://decodecms.com/crear-un-child-theme-en-wordpress-de-manera-correcta/)

Style.css

            /*
            Theme Name:   Twenty Seventeen Child
            Theme URI:    http://misitio.com/twenty-seventeen-child/
            Description:  Child theme para modificaciones varias
            Author:       Mi nombre
            Author URI:   http://misitio.com
            Template:     twentyseventeen
            Version:      1.0.0
            License:      GNU General Public License v2 or later
            License URI:  http://www.gnu.org/licenses/gpl-2.0.html
            Tags:         light, dark, two-columns, right-sidebar, responsive-layout, accessibility-ready
            Text Domain:  twenty-seventeen-child
            */



            Theme Name: nombre del tema hijo
            Theme URI: opcional, la url de la documentación y demo del tema hijo.
            Descripción, Author, Author URI: son opcionales pero se recomienda colocarlas.
            Template: este parámetro te indica el nombre de la carpeta del tema padre.
            Version: versión del tema hijo, importante para el control de cambios.
            License, License URI: si se quieres hacer alguna variación a la licencia.
            Tags: si harás variaciones en la funcionalidad del theme, puedes agregar otro tag.
            Text-Domain: si tus cambios implican agregar texto traducible.

functions.php

Una vez que has creado el archivo style.css, necesitas ahora importar los estilos del tema padre, anteriormente se usaba @import para importar los estilos, sin embargo esto es una mala práctica, lo que se recomienda es usar el archivo functions.php y a través de código cargar el archivo style.css del theme padre y, en caso se hagas modificaciones CSS en el tema hijo, cargar también el style.css del theme hijo.

        El código para cargar los estilos es similar a:

        <?php
        function enqueue_styles_child_theme() {

            $parent_style = 'twentyseventeen-style';
            $child_style  = 'twentyseventeen-child-style';

            wp_enqueue_style( $parent_style,
                        get_template_directory_uri() . '/style.css' );

            wp_enqueue_style( $child_style,
                        get_stylesheet_directory_uri() . '/style.css',
                        array( $parent_style ),
                        wp_get_theme()->get('Version')
                        );
        }
        add_action( 'wp_enqueue_scripts', 'enqueue_styles_child_theme' );

        En el código anterior:

            La función: enqueue_styles_child_theme, es llamada en la acción: wp_enqueue_scripts
            Definimos dos variables, que serán los IDs de los estilos a cargar.
                El ID del padre ya existe por lo que tenemos que buscarlo en el archivo functions.php del theme padre.
                El ID del theme hijo puede ser cualquier texto, aunque se recomienda igualmente que tenga un nombre similar al theme padre.
            Colocamos en cola el estilo del tema padre a través de la función wp_enqueue_style.
            Colocamos en cola el estilo del tema hijo, igualmente usando la función wp_enqueue_style.
            En la carga del style.css del tema hijo usamos el tercer parámetro para indicar dependencia.
            También usamos el cuarto parámetro para usar la versión que se ha definido en el archivo style.css del tema hijo.


## Cambiar estado del pedido en WooCommerce automáticamente
https://woodemia.com/cambiar-estado-del-pedido-en-woocommerce-automaticamente/

    // Actualiza automáticamente el estado de los pedidos a COMPLETADO
    add_action( 'woocommerce_order_status_processing', 'actualiza_estado_pedidos_a_completado' );
    add_action( 'woocommerce_order_status_on-hold', 'actualiza_estado_pedidos_a_completado' );
    function actualiza_estado_pedidos_a_completado( $order_id ) {
        global $woocommerce;

        //ID's de las pasarelas de pago a las que afecta
        $paymentMethods = array( 'bacs', 'cheque', 'cod', 'paypal' );

        if ( !$order_id ) return;
        $order = new WC_Order( $order_id );

        if ( !in_array( $order->payment_method, $paymentMethods ) ) return;
        $order->update_status( 'completed' );
    }
    
 En nuestra plantilla se ha modificado en el theme-child > woocommerce_code.php
           
           class WooCustomProductForm 
            {
                function __construct()
                {

                    // Updates all orders with processing status to completed
                    add_action('woocommerce_order_status_processing', array($this, 'update_order_status_to_completed'));
                    add_action('woocommerce_order_status_on-hold', array($this, 'update_order_status_to_completed'));
                }

                /**
                 * Updates all orders with processing status to completed
                 * This is needed cause tickets are virtual products and not dowloadable 
                 */
                public function update_order_status_to_completed($order_id)
                {
                    global $woocommerce;

                    // Payment gateway ids
                    $paymentMethods = array('stripe', 'paytpv', 'paypal');

                    if ( !$order_id ) return;
                    $order = new WC_Order( $order_id );

                    if ( !in_array( $order->payment_method, $paymentMethods ) ) return;
                    $order->update_status('completed');
                }
             }

# Wordpress para desarrolladores: 
[Las apis de wordpress](https://www.youtube.com/watch?v=7iEd0GtNg0w)

https://www.youtube.com/watch?v=5VaOtsYgRHA&list=PLEtcGQaT56cgWfEWXD0GzF9UGYn7eL1kj

### Diseñar plugin de formulario de datos de entrada
https://kungfupress.com/como-programar-un-formulario-en-wordpress-sin-utilizar-plugins/

## Modificar plugin búsqueda - CON AJAX
### Diferencia entre wp_ajax y wp_ajax_nopriv
https://www.linuxhispano.net/2013/08/02/diferencia-entre-wp_ajax-y-wp_ajax_nopriv/

Cuando trabajas con AJAX en WordPress, si quieres hacerlo bien, debes hacer llamadas a admin-ajax.php y desde ahí gestionar las peticiones y sus salidas. Si conocéis esta técnica, conoceréis las funciones: wp_ajax_(acción) y wp_ajax_nopriv_(acción).

La diferencia entre ambas no se suele conocer y lo malo es que si no lo sabes, recibirás todo el rato un cero (0) como salida de la petición del admin-ajax.php si no estás usándolo correctamente. La diferencia es la siguiente:

    wp_ajax: se usa cuando el usuario tiene que haber iniciado sesión
    wp_ajax_nopriv: cuando el usuario no tiene que haber iniciado sesión

La llamada sería así en cada caso:

add_action( 'wp_ajax_<acción>',  );
add_action( 'wp_ajax_nopriv_<acción>',  );

Un ejemplo práctico que acabo de hacer:

add_action( 'wp_ajax_actualizar_formulario', 'actualizar_formulario' );
add_action( 'wp_ajax_nopriv_envio_contacto', 'enviar_formulario_contacto' );

##### En mi caso para modificar la función add_action('wp_ajax_nopriv_get_matched_locations', array($this, 'get_matched_locations'));




#### Configurar ftp wordpress en local con xampp
http://www.programadorwordpress.es/configurar-ftp-wordpress-en-local-con-xampp/


### Cómo añadir las etiquetas Open Graph
https://empresiona.com/blog/wordpress-anadir-etiquetas-open-graph-facebook/
https://developer.twitter.com/en/docs/tweets/optimize-with-cards/guides/getting-started


Limpiar caché de:

twitter: https://cards-dev.twitter.com/validator
facebook: https://developers.facebook.com/tools/debug
telegram: https://stackoverflow.com/questions/34707915/how-do-you-clear-the-open-graph-cache-of-an-url-on-telegram
whatsap: https://stackoverflow.com/questions/25100917/showing-thumbnail-for-link-in-whatsapp-ogimage-meta-tag-doesnt-work#32154775


<meta name="description" content="Información y publicación gratuita de todo tipo de eventos musicales celebrados en España.">

<meta name="twitter:card" content="summary" />
<meta property="og:url" content="https://abasedemusica.es/agenda/" />
<meta property="og:title" content="Agenda A Base de Música" />
<meta property="og:description" content="La mayor agenda musical de España" />
<meta property="og:image" content="https://abasedemusica.es/agenda/wp-content/uploads/2020/06/tusumas-i-scaled.jpg"/>

Límite: 300 kB la imagen

### Personalizar pagina de micuenta woocommerce
https://ayudawp.com/personalizar-mi-cuenta-woocommerce/

### Editar los campos del formulario de checkout en Woocommerce
https://www.claserama.com/editar-campos-checkout-woocommerce/

### Variaciones del producto 
https://docs.woocommerce.com/document/variable-product/

# WORDPRESS DEVELOPER
#### CREACIÓN DE SALT
https://api.wordpress.org/secret-key/1.1/salt/

#### CONFIGURAR Nº DE REVISIONES A GUARDAR
* Dentro de wp_config.php
Constante: define('WP_POST_REVISION',[valor]); [3, false ...]

### GUARDAR QUERIES PARA DEPURAR Y COMPROBAR LO QUE SE EJECUTA
* Dentro de wp_config.php

Constante: define('SAVEQUERIES',[true | false]);
Para mostrarlo hay que insertar el siguiente código para acceder al array que se crea.
global $wpdb;
print_r($wpdb->queries);

### Consultar pedidos de WooCommerce donde no existen metadatos
https://www.it-swarm.dev/es/wp-query/consultar-pedidos-de-woocommerce-donde-no-existen-metadatos/963548720/

            Ver: https://nube.abasedemusica.es/vo/concursantes-test/

