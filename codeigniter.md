## Mensajes en codeigniter
https://groups.google.com/g/codeigniter-spanish/c/HLWV23tvSLk?pli=1

podrias usar este conjunto de funciones

para los mensajes puedes usar la funcion set_flashmessage(); que se encuentra en la clase de manejo de sesiones
para insertar y recuperar los datos en caso de errores usar el form_validation

con el tema del insert haces algo como
en tu controlador ---

```php
if($this->mi_modelo->insertar_datos())
{
// si inserto
redirect('http://url.de.tu.pagina/controlador/metodo/lista');
}
----

entu modelo
function insertar_datos()
{
 $data = array( ... datos de tus columnas para la tabla...);
if($this->db->insert('tabla',$data))
 $this->session->set_flashdata('resultado_insercion','Se inserto correctamente el registro');
return true;
}else{
 $this->session->set_flashdata('resultado_insercion','Error al insertar el registro');
return false;
}
}//end function


y en tu vista ....

html

body

<div class='mensaje_resultado'> <?=$this->session->flashdata('resultado_insercion'); ?> </div>

/body


Uso con Alert boostrap

```php
<!-- alert boostrap -->
<div class="alert alert-info">
	<button type="button" class="close" data-dismiss="alert">&times;</button>
	<? echo $this->session->flashdata('mensaje'); ?>
</di>

```

Ejemplo: 
```php
//consulta.php
$this->session->set_flashdata('message',['No existen datos con este criterio', 'danger']);


//consulta_model
function mostrar_messages(){
	if ($this->session->flashdata('message') !='') { 
		// <!-- alert boostrap -->	
		echo '
		<div class="alert alert-'.$this->session->flashdata('message')[1].'">
			<button type="button" class="close" data-dismiss="alert">&times;</button>'
			.$this->session->flashdata('message')[0].'
		</div>';

	}
}

//informe_dashboar.php
<div id="infoMessage"><? echo $this->session->flashdata('mensaje'); ?></div>

```
## Guia usuario query builder
https://codeigniter.com/userguide3/database/query_builder.html

```

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

 
