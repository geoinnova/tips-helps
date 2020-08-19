## error - Can't create/write to file '/var/folders/

Solución: https://stackoverflow.com/questions/19932371/1-cant-create-write-to-file-var-folders


      Detener completamente XAMPP, esto significa detener apache, ftp y mysql.

      Abrir el programa llamado Terminal.

      Escribir sudo -i para convertirse en root (o haga su root si el primero no funciona para usted).

      Lo más probable es que se le solicite una contraseña que debe ingresar mientras no se muestren caracteres.

      Ejecutar chmod 600 /Applications/XAMPP/xamppfiles/etc/my.cnf.

      Salir de la shell raíz con exit o simplemente cierre la Terminal.

      Reinicie XAMPP (apache, ftp y mysql).


