## Sistema de roles
composer create-project laravel/laravel laravel_roles

creo bbdd laravel_roles
conectar la bbdd configurar .env
php artisan migrate

### sistema de autenticación
composer require laravel/ui
para activarlo > php artisan ui vue --auth

para instalar los paquetes del package.json > npm install && npm run dev



### Error: Syntax error or access violation: 1463 Non-grouping field 'loquesea' is used in HAVING clause


Compruebe en el archivo config / database.php en la conexión mysql que lo estricto es falso:

    'strict' => false,

Si está en true, ponerlo a false

https://stackoverflow.com/questions/39053335/laravel-5-3-syntax-error-or-access-violation-1463-non-grouping-field-distance

