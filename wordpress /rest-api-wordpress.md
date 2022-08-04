### API REST de Wordpress (wp-api) 404 Error: No se puede acceder a la API REST de WordPress en local

Solución: https://stackoverflow.com/questions/34670533/wordpress-rest-api-wp-api-404-error-cannot-access-the-wordpress-rest-api

```sh
solo tuve que actualizar los enlaces permanentes para obtener un sitio nuevo y recién instalado para devolver las llamadas a la API v2. Lo que hice:

    Crear sitio
    Vaya a http://yoursitename.wpengine.com/wp-json/wp/v2/posts
        obtener 404
    Vaya a administración, configuración, enlaces permanentes, elija "Nombre de la publicación"
    Haga clic en "Guardar cambios"
    Vaya a http://yoursitename.wpengine.com/wp-json/wp/v2/posts
        éxito. la página muestra la respuesta JSON
```


### Crear usuario y credenciales para utilizar la API - Creación de claves de acceso a la API
https://help.clouding.io/hc/es/articles/360017428140-C%C3%B3mo-utilizar-la-API-de-WordPress-y-crear-nuestros-Custom-Post-Types)

* Crear un usuario diferente para la API
* Utilizaremos el Plugin "Application Passwords" que nos permite crear una clave para el usuario de WordPress sin exponer su contraseña de acceso al panel de WordPress.

Para añadir el Plugin iremos a Plugins -> Añadir nuevo y en la barra de búsqueda escribiremos "Application Passwords" e instalamos y activamos el plugin.

#### Autenticación con JWT en la API de WordPress (me ha funcionado este plugin)
- https://decodecms.com/autenticacion-con-jwt-en-la-api-de-wordpress/
- https://www.youtube.com/watch?v=EkWnRaz5Obw

*modificar wp-config.php y añadir: define('JWT_AUTH_SECRET_KEY', 'una-clave-secreta');

#### Preparar el CPT para crear endpoint a la API de Wordpress

Para que sea accesible desde la api, en la configuración del CPT hay que poner:
```php
'show_in_rest'          => true,
```

Ahora hay que registrar la ruta propia para los distintos métodos. 

El siguiente código debemos insertarlo en Aparencia -> Editor de Temas -> functions.php. Esto declarará la url midominio.com/wp-json/api/v1/insertar_vps.
