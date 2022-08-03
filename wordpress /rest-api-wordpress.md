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

