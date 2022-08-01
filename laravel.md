## Modificar .env para conexión

Importante estos datos:
```sh
APP_NAME=geoApp
APP_ENV=local
APP_KEY=base64:8uxkjKoAbC3EdBgER+So8rRv9EHOHcsbFMn/RK7DkSU=
APP_DEBUG=false
APP_URL=http://visores2.geoinnova.org/geoapp/

LOG_CHANNEL=stack
LOG_LEVEL=debug

DB_CONNECTION=mysql
DB_HOST=localhost
DB_PORT=3306
DB_DATABASE=
DB_USERNAME=
DB_PASSWORD=

``` 

## Sistema de roles
composer create-project laravel/laravel laravel_roles

creo bbdd laravel_roles
conectar la bbdd configurar .env
php artisan migrate

### sistema de autenticación
composer require laravel/ui
para activarlo > php artisan ui vue --auth

para instalar los paquetes del package.json > npm install && npm run dev

Para instalar bootstrap > php artisan ui bootstrap

######
1. composer require laravel/ui
2. php artisan ui vue --auth // puede ser vue | react | bootstrap
3. npm install
4. npm run dev // Aquí está el problema 
#####

### Error: Syntax error or access violation: 1463 Non-grouping field 'loquesea' is used in HAVING clause


Compruebe en el archivo config / database.php en la conexión mysql que lo estricto es falso:

    'strict' => false,

Si está en true, ponerlo a false

https://stackoverflow.com/questions/39053335/laravel-5-3-syntax-error-or-access-violation-1463-non-grouping-field-distance

## LLamar controlador
```js
Ejemplo llamada:
http://localhost/laravel/laravel-leaflet-example/public/api/outlets
Action: App\Http\Controllers\Api\OutletController@index 
```

estoy en home-admin

