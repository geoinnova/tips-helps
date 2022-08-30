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
