## Requisitos en el header

Como mínimo, un comentario de cabecera debe contener el nombre del plugin, pero puedes - y debes - incluir algunos datos más:

    * Plugin Name: El nombre del plugin, el cuál se mostrará en la lista de plugins en el admin de WordPress.
    * Plugin URI: La página de inicio del plugin, que debe estar en WordPress.org o en tu propio sitio web.
    * Description: Una descripción corta del plugin. Mantén esta descripción por debajo de los 140 caracteres.
    * Version: La versión actual de tu plugin. Nota que WordPress y la API de plugins usa la función version_compare() 
    cuando considera los números de versiones: por ejemplo, 1.02 es mayor que 1.1.
    * Author: El nombre del autor del plugin. Si hay más de uno, sepáralos por coma.
    * Author URI: El sitio web del autor o su perfil en otro sitio web como el de WordPress.org.
    * License: El nombre corto de la licencia (slug), por ejemplo GPLD2.
    * License URI: Enlace para la licencia.
    * Text Domain: El text domain se usa para poder internacionalizar tu plugin, o traducirlo a otros idiomas. 
    Usa el paquete gettext.
    * Domain Path: La ruta del dominio le indica a WordPress dónde encontrar las traducciones.

Así quedaría el código básico de la cabecera en un plugin de WordPress:

    /**
     * Plugin Name: Prueba
     * Plugin URI:  https://rabasco-developer.es/plugin
     * Description: Curso creación de plugin
     * Version:     2020-08
     * Author:      rabasco-developer
     * Author URI:  https://rabasco-developer.es
     * License:     GPL2
     * License URI: https://www.gnu.org/licenses/gpl-2.0.html
     * Text Domain: erb
     * Domain Path: /languages
     */

## Hooks - Actions y Filters

Los hooks (o ganchos) de WordPress son la forma en la que una pieza de código puede interactuar con otra pieza. Es la base de cómo interactúan los plugins y temas con WordPress, pero también lo extienden.

Hay dos tipos des hooks: Actions y Filters (acciones y filtros). Para usarlos, necesitas escribir una función personalizada, también llamada de retorno (o Callback), y entonces, registrarla con un hook de WordPress para una acción o filtro específico.

    Actions: te permiten añadir data o cambiar cómo opera WordPress. Las funciones de retorno para las acciones correrán 
    en un punto específico de la ejecución de WordPress y pueden ejecutar alguna tarea, como mostrar una salida al usuario 
    o insertar algo en la base de datos.

    Filters: te dan la habilidad de cambiar datos durante la ejecución de WordPress. La función de retorno para los filtros 
    aceptará una variable, la modificará y la devolverá. Están diseñados para trabajar de manera aislada y nunca deben tener 
    efectos secundarios como el de afectar a variables globales.

WordPress provee muchos hooks que puedes usar, pero también puedes crear los tuyos propios, de esta forma, otros desarrolladores pueden extender y modificar tu plugin o tema.

Por otro lado, la activación y desactivación de hooks provee formas de ejecutar acciones cuando el plugin es activado o desactivado.

En la activación, los plugins pueden ejecutar una rutina para añadir reglas de reescritura o establecer valores por defecto.

En la desactivación, los plugins pueden ejecutar una rutina para eliminar datos temporales como la caché y archivos y directorios temporales.

Hook de activación > función register_activation_hook():

    register_activation_hook( __FILE__, 'pluginprefix_function_to_run' );

Hook de desactivación > función register_deactivation_hook():

    register_deactivation_hook( __FILE__, 'pluginprefix_function_to_run');

El primer parámetro en cada una de estas funciones hace referencia al archivo principal de tu plugin. Normalmente estas dos funciones se activarán dentro del archivo principal del plugin; sin embargo, si las funciones están colocadas en otro archivo, tienes que actualizar el primer parámetro para apuntar correctamente al archivo principal del plugin.

## Organización de archivos

El directorio raíz de tu plugin debe contener un archivo llamado como tu plugin: plugin-name.php y opcionalmente un archivo para la desinstalación, uninstall.php. Todos los otros archivos deben estar organizados en sub-carpetas cuando sea posible.
Estructura de carpetas

Una estructura de carpetas limpia ayuda a mantener los archivos similares juntos. Aquí tienes un ejemplo de estructura de carpetas como referencia:

    /plugin-name
         plugin-name.php
         uninstall.php
         /languages
         /includes
         /admin
         /admin/js
         /admin/css
         /admin/images
         /public
         /public/js
         /public/css
         /public/images

### Boilerplate
Podemos usar algunos alguna plantilla o punto de partida para desarrollar el plugin: https://github.com/DevinVinson/WordPress-Plugin-Boilerplate

## Validando los datos

Hay al menos 3 formas de hacerlo: funciones de PHP, funciones de WordPress y funciones personalizadas que tu escribas.

#### Funciones de PHP

La validación básica es factible usando muchas de las funciones de PHP, incluyendo estas:

    isset() y empty() para comprobar si una variable existe y no está en blanco.

    mb_strlen() o strlen() para comprobar que una cadena tenga el número de caracteres esperados.

    preg_match(), strpos() para comprobar ocurrencias de ciertas cadenas en otras cadenas.

    count() para comprobar cuántos ítems hay en un array.

    in_array() para comprobar si algo existe dentro de un array.

#### Funciones de WordPress

WordPress provee muchas funciones útiles que te ayudan a validar diferentes tipos de datos. Aquí hay algunos ejemplos:

    is_email() va a validar si es una dirección de correo electrónico válida.

    term_exists() comprueba si un tag, categoría u otra taxonomía existe.

    username_exists() comprueba si nombre de usuario existe.

    validate_file() validará que una ruta insertada hacia un archivo sea una ruta real (pero no si el archivo existe).

Puedes comprobar la referencia del código de WordPress para más funciones como estas. Busca funciones con nombres como estos: *_exists(), *_validate() y is_*(). No todas estas son funciones de validación pero muchas son útiles.
Funciones de PHP y JavaScript personalizadas

#### Funciones propias
Cuando escribas funciones de validación debes nombrarlas como una pregunta (ejemplos: is_phone, is_available, is_es_zipcode).

La función debe devolver un valor booleano, sea true o false, dependiendo de si el dato es válido o no. Esto te permetirá usar la función como condición.
Ejemplo

Digamos que vas a realizar una consulta a la base de datos sobre una publicación y quieres darle al usuario la posibilidad de ordenar los resulatdos de la consulta.

Este ejemplo de código comprueba una clave de ordenación entrante (llamada orderby) contra un array de claves permitidas usando la función de PHP in_array con tipado estricto habilidado (que dice a PHP que se asegure que la clave de ordenación no está solo en el array sino también en la cadena como se espera).

        <?php
        $allowed_keys = ['author', 'post_author', 'date', 'post_date'];

        $orderby = sanitize_key($_POST['orderby']);

        if (in_array($orderby, $allowed_keys, true)) {
            // modifica la consulta para ordenar por la clave orderby
        }
        
## Securizando la entrada
Securizar la entrada es el proceso de sanear (limpiar y filtrar) datos de entrada. 

La serie de funciones de ayuda sanitize_*() de WordPress soy muy buenas, ya que te aseguran que estás usando datos finales seguros, y requieren un mínimo esfuerzo por tu parte:

    sanitize_email()
    sanitize_file_name()
    sanitize_html_class()
    sanitize_key()
    sanitize_meta()
    sanitize_mime_type()
    sanitize_option()
    sanitize_sql_orderby()
    sanitize_text_field()
    sanitize_title()
    sanitize_title_for_query()
    sanitize_title_with_dashes()
    sanitize_user()
    esc_url_raw()
    wp_filter_post_kses()
    wp_filter_nohtml_kses()

Ejemplo

Digamos que tenemos un campo de entrada llamado título (title).

    <input id="title" type="text" name="title">

Puedes sanear los datos de entrada con la función sanitize_text_field():

    $title = sanitize_text_field($_POST['title']);
    update_post_meta($post->ID, 'title', $title);

Bajo la cortina, sanitize_text_field() hace lo siguiente:

    Comprueba por codificación UTF-8 no válida.
    Convierte el símbolo menor-que (<) a entidad.
    Elimina todas las etiquetas.
    Elimina los saltos de línea, tabulaciones y espacios en blanco extra.
    Elimina los bytes nulos.


## Securizando la salida
Securizar la salida es el proceso de escapado de datos de salida. Escapado significa eliminar los datos no queridos, como HTML mal formado o etiquetas de scripts.

Cuando estás procesando datos, asegúrate de escaparlos correctamente. El escapado previene de ataques XSS.

### Escapado

El escapado te ayuda a securizar tus datos antes de procesarlos para el usuario final. WordPress tiene unas cuantas de funciones que puedes usar para los escenarios más comunes.

    esc_html() - Usa esta función en cualquier momento que un elemento HTML encierre una sección de datos que se vayan a mostrar.
    esc_url() - Usa esta función en todas las URLs, incluyendo aquellas en los atributos src y href de un elemento HTML.
    esc_js() - Usa esta función para el código JavaScript en el mismo documento.
    esc_attr() - Usa esta función en todo lo que esté mostrado en un atributo de un elemento HTML.

    La mayoría de las funciones de WordPress prepararán tus datos para mostrarlos escapados, así que no necesitarás escapar los datos de neuvo. Por ejemplo, puedes usar con seguridad la función the_title() sin escapado.

### Escapado con Localización

En vez de usar echo para mostrar datos, es normal usar las funciones de localización de WordPress, como _e() o __(). Estas funciones simplemente envuelven una función de localización dentro de una función de escapado:

esc_html_e('Hello World', 'text_domain');
// Es lo mismo que
echo esc_html(__('Hello World', 'text_domain'));

Estas funciones de ayuda combinan localización y escapado:

    esc_html__()
    esc_html_e()
    esc_html_x()
    esc_attr__()
    esc_attr_e()
    esc_attr_x()

### Escapado personalizado

En el caso que necesites escapar tu salida de una forma específica, la función wp_kses() (pronunciada “kisses”) será util. Esta función te asegura que sólo los elementos HTML especificados, los atributos y los valores de atributos aparezcan en tu salida y normalicen las entidades HTML.

        $allowed_html = [
            'a'      => [
                'href'  => [],
                'title' => [],
            ],
            'br'     => [],
            'em'     => [],
            'strong' => [],
        ];
        echo wp_kses($custom_content, $allowed_html);

La función wp_kses_post() es una función envolvente para wp_kses donde $allowed_html es una configuración de reglas usadas por el contenido de una publicación.

    echo wp_kses_post( $post_content )


## Nonces
Los Nonces son números generados para verificar el origen y destino de la solicitud por razones de seguridad. Cada nonce puede ser usado una sola vez. La palabra Nonce se forma del inglés once (una sola vez) y N (Número).

Si tu plugin permite a los usuarios enviar datos; sea en el lado de Administración o público; tienes que asegurarte que el usuario es quien dice ser y que tiene las capacidades necesarias para realizar esa acción. Haciendo ambas cosas los datos cambiaran solo cuando el usuario espere que cambien.

Cuando tu generas un enlace de borrado, tienes que usar la función wp_create_nonce() para añadir un nonce al link, el argumento pasado a la función se asegurará de que el nonce creado sea único para una acción en particular.

Entonces, cuando estás procesando una petición del enlace de borrado, puedes comprobar que el nonce es el que tu esperabas que fuera.

Ejemplo completo

        <?php
        /**
         * generate a Delete link based on the homepage url
         */
        function wporg_generate_delete_link($content)
        {
            // run only for single post page
            if (is_single() && in_the_loop() && is_main_query()) {
                // add query arguments: action, post, nonce
                $url = add_query_arg(
                    [
                        'action' => 'wporg_frontend_delete',
                        'post'   => get_the_ID(),
                        'nonce'  => wp_create_nonce('wporg_frontend_delete'),
                    ],
                    home_url()
                );
                return $content . ' <a href="' . esc_url($url) . '">' . esc_html__('Delete Post', 'wporg') . '</a>';
            }
            return null;
        }

        /**
         * request handler
         */
        function wporg_delete_post()
        {
            if (
                isset($_GET['action']) &&
                isset($_GET['nonce']) &&
                $_GET['action'] === 'wporg_frontend_delete' &&
                wp_verify_nonce($_GET['nonce'], 'wporg_frontend_delete')
            ) {

                // verify we have a post id
                $post_id = (isset($_GET['post'])) ? ($_GET['post']) : (null);

                // verify there is a post with such a number
                $post = get_post((int)$post_id);
                if (empty($post)) {
                    return;
                }

                // delete the post
                wp_trash_post($post_id);

                // redirect to admin page
                $redirect = admin_url('edit.php');
                wp_safe_redirect($redirect);

                // we are done
                die;
            }
        }

        if (current_user_can('edit_others_posts')) {
            /**
             * add the delete link to the end of the post content
             */
            add_filter('the_content', 'wporg_generate_delete_link');

            /**
             * register our request handler with the init hook
             */
            add_action('init', 'wporg_delete_post');
        }

Buen artículo con ejemplo de nonce: https://decodecms.com/que-son-los-nonces-en-wordpress/


## Crear página de configuración del plugin
El primer paso para empezar a darle funcionalidad a nuestro plugin es tener un sitio donde poder modificar el comportamiento del mismo. Esto normalmente lo haremos en el Escritorio de WordPress. 

Podemos crear una sección única para nuestro plugin 

    (add_menu_page( string $page_title, string $menu_title, string $capability, string $menu_slug, callable $function = '', string $icon_url = '', int $position = null ) ), 

o añadirlo a secciones que ya tiene WordPress 

    (add_options_page( $page_title, $menu_title, $capability, $menu-slug, $function )), como Ajustes, Herramientas u otras.

Para insertar nuestra página de configuración del plugin usaremos el gancho admin_menu. Concretamente, si queremos insertarlo en el menú Ajustes, contamos con la función add_options_page(). El código para crear nuestra página de configuración básica en WordPress sería:

    /*
     * Add a link to our plugin in the admin menu
     * under 'Settings > OpenWebinars Badges'
     */

    function openwebinars_badges_menu() {

      /*
       * Use the add_options page function
       * add_options_page( $page_title, $menu_title, $capability, $menu-slug, $function );
       */

      add_options_page(
        'Official OpenWebinars Badges Plugins',
        'OpenWebinars Badges',
        'manage_options',
        'openwebinars-badges',
        'openwebinars_badges_options_page'
      );
    }
    add_action( 'admin_menu', 'openwebinars_badges_menu' );

Esto creará una página de configuración vacía en Ajustes -> OpenWebinars Badges. Pero en la función add_options_page() hemos indicado que la función que “llenará” nuestra página, o la función a ejecutar dentro de esa página sea openwebinars_badges_options_page. 

    function openwebinars_badges_options_page() {
      if( !current_user_can( 'manage_options' ) ) {
        wp_die( 'You do not have sufficient permissions to access this page.' );
      }

      echo '<p>Welcome to our plugin page!</p>';
    }

Es importante que securicemos nuestro plugin desde el principio. Esta página solo estará disponible para los usuarios que puedan manejar opciones, es decir de Editores hacia arriba.

Menús de administración: https://codex.wordpress.org/Administration_Menus
Crear menus en el panel de administración: https://danielcastanera.com/crear-menus-panel-administracion-wordpress/
Iconos: https://developer.wordpress.org/resource/dashicons/#welcome-learn-more


