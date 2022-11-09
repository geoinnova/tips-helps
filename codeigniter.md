## Creada función para mostrar todas las querys que se han ejecutado

```php
function mostrar_querys(){
	$CI = get_instance();
	$times = $CI->db->query_times;
	foreach ($CI->db->queries as $key => $query) 
	{ 
		$sql = $query . " \n "; 
		// $sql = $query . " \n Execution Time:" . $times[$key]; 

		echo $sql . "<br><br>";    
	}

}
    
$this->mostrar_querys();
```
    
    

## ¿Actualizar completamente la página en CodeIgniter
```php
redirect($_SERVER['REQUEST_URI'], 'refresh');
```

Descomprimir y subir al servidor
configurar la URL en System/application/config/config.php


Call to undefined function CodeIgniter\locale_set_default() - Xampp
https://stackoverflow.com/questions/71434878/call-to-undefined-function-codeigniter-locale-set-default-xampp

Go to C:\xampp\htdocs\projectfolder\system\CodeIgniter.php - line 184 and change the next line.

Before:

locale_set_default($this->config->defaultLocale ?? 'en');

After:

if( function_exists('locale_set_default' ) ) :
    locale_set_default($this->config->defaultLocale ?? 'en');
    endif;

Once I updated Xampp to the 7.4 version (download here), I just needed to enable the extension=intl in the xampp\php\php.ini file. As it is explained here, you just have to uncomment the line from ;extension=intl to extension=intl.

Then you can leave the C:\xampp\htdocs\projectfolder\system\CodeIgniter.php - line 184 as it was in the beginning.

locale_set_default($this->config->defaultLocale ?? 'en');

### Cómo instalar o configurar CodeIgniter 4 en Xampp Server
https://www.youtube.com/watch?v=uZJyh7rON_Q


### https://forum.codeigniter.com/thread-76953.html 
 Sigue mostrando "404 Página no encontrada" excepto el mensaje de bienvenida predeterminado 
 
 ###  404 - Archivo no encontrado Codeigniter 4 
 https://forum.codeigniter.com/thread-77786.html
 
 ## Instalación manual de codeigniter 4 en xampp windows
  https://www.youtube.com/watch?v=lfViPGxfO0I

 
