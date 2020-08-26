## Requisitos en el header

Como mínimo, un comentario de cabecera debe contener el nombre del plugin, pero puedes - y debes - incluir algunos datos más:

    - Plugin Name: El nombre del plugin, el cuál se mostrará en la lista de plugins en el admin de WordPress.
    - Plugin URI: La página de inicio del plugin, que debe estar en WordPress.org o en tu propio sitio web.
    - Description: Una descripción corta del plugin. Mantén esta descripción por debajo de los 140 caracteres.
    - Version: La versión actual de tu plugin. Nota que WordPress y la API de plugins usa la función version_compare() 
    cuando considera los números de versiones: por ejemplo, 1.02 es mayor que 1.1.
    - Author: El nombre del autor del plugin. Si hay más de uno, sepáralos por coma.
    - Author URI: El sitio web del autor o su perfil en otro sitio web como el de WordPress.org.
    - License: El nombre corto de la licencia (slug), por ejemplo GPLD2.
    - License URI: Enlace para la licencia.
    - Text Domain: El text domain se usa para poder internacionalizar tu plugin, o traducirlo a otros idiomas. 
    Usa el paquete gettext.
    - Domain Path: La ruta del dominio le indica a WordPress dónde encontrar las traducciones.

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

### Validando los datos

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
        


