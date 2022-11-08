## Dar formato a un objeto y/o arreglo
```php 
echo "<pre>";
   print_r($myarray);
echo "</pre>";
```

## Generar un nombre de archivo único

    <?php 
    echo "mi nombre de archivo es: ". getFileName("pepe.png");

    function getFileName($nombre_archivo){
        $name = hash('md5', gmdate('U').$nombre_archivo.rand(0, 1000)); 
        return $name.".".pathinfo($nombre_archivo, PATHINFO_EXTENSION);
    }

    ?>
