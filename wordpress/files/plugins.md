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
     * Plugin Name: WordPress.org Plugin
     * Plugin URI:  https://developer.wordpress.org/plugins/the-basics/
     * Description: Basic WordPress Plugin Header Comment
     * Version:     20160911
     * Author:      WordPress.org
     * Author URI:  https://developer.wordpress.org/
     * License:     GPL2
     * License URI: https://www.gnu.org/licenses/gpl-2.0.html
     * Text Domain: wporg
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
