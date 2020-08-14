### Error: Syntax error or access violation: 1463 Non-grouping field 'loquesea' is used in HAVING clause


Compruebe en el archivo config / database.php en la conexión mysql que lo estricto es falso:

    'strict' => false,

Si está en true, ponerlo a false

https://stackoverflow.com/questions/39053335/laravel-5-3-syntax-error-or-access-violation-1463-non-grouping-field-distance

