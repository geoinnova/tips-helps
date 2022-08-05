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


## Páginas a revisar:
### Cómo utilizar la API de WordPress y crear nuestros Custom Post Types : https://help.clouding.io/hc/es/articles/360017428140-C%C3%B3mo-utilizar-la-API-de-WordPress-y-crear-nuestros-Custom-Post-Types)
### Post url en local de la API: https://geoinnova.org/wp-json/wp/v2/posts
### Url getCourses (listado) http://localhost/_geoinnova.org/wp-json/v1/getCourses

### Obtener rutas y endpoints: [Routes and Endpoints](https://developer.wordpress.org/rest-api/extending-the-rest-api/ro
https://ourawesomesite.com/wp-json/

### Obtener campos personalizados con get_post() https://maswordpress.info/questions/50097/campos-personalizados-con-get-post

```php
 foreach ($posts as $clave => $valor) {
        $registro['ID'] = $posts[$clave]->ID;
        $registro['title'] = $posts[$clave]->post_title;
        $registro['meta'] = get_post_meta($registro['ID']);
        array_push($data, $registro);
    }
 ```
 
 https://developer.wordpress.org/reference/functions/get_post_meta/
```php
$post_metas = get_post_meta(get_the_ID());

sample output:
array(2) {
  ["_meta_key1"]=>
  array(1) {
    [0]=> "value1"
   }
  ["_meta_key2"]=>
  array(1) {
    [0]=> "val2"
   }
}
```
 
### Agregar endpoints a la API REST de WordPress: https://decodecms.com/agregar-endpoints-a-la-api-rest-de-wordpress/

### fecht api - pasar token
https://es.stackoverflow.com/questions/381268/fetch-api-con-javascript-token

```js
fetch('https://randomuser.me/api',
     headers: {
       "Authorization": "Bearer API_TOKEN", //Agregado
     },
     )
    .then(r => r.json())
    .then(data => {
        (data.results[0])
            contenido.innerHTML = `
            <img src="${data.results['0'].picture.large}">
            <p>Nombre: ${data.results['0'].name.title +' ' + data.results['0'].name.last +' ' + data.results['0'].name.last}</p>
            `
    })
   ```

https://es.stackoverflow.com/questions/428354/error-al-pasar-token-a-trav%C3%A9s-de-api-por-fetch

https://www.youtube.com/watch?v=hioDMKdJhwQ

## Ejemplo de CRUD API REST para CPT
https://www.youtube.com/watch?v=jKLhwFhf9AA

https://github.com/Pricoders/wp-rest-api-endpoints-example/blob/master/functions.php

### CRUD para JS con Fetch API
https://postsrc.com/code-snippets/how-to-make-patch-request-with-fetch-api

### Añadir de forma correcta tanto js como css al plugin

https://kinsta.com/es/blog/wp-enqueue-scripts/




