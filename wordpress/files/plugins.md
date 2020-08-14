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

Para configurar un hook de activación, usa la función register_activation_hook():
register_activation_hook( __FILE__, 'pluginprefix_function_to_run' );

Para configurar un hook de desactivación, usa la función register_deactivation_hook():
register_deactivation_hook( __FILE__, 'pluginprefix_function_to_run');

El primer parámetro en cada una de estas funciones hace referencia al archivo principal de tu plugin. Normalmente estas dos funciones se activarán dentro del archivo principal del plugin; sin embargo, si las funciones están colocadas en otro archivo, tienes que actualizar el primer parámetro para apuntar correctamente al archivo principal del plugin.
