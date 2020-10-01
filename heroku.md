## Desplegar aplicación Java en Heroku

#### [Video Explicativo](https://www.youtube.com/watch?v=7p8jyidcNMs)

* Crear cuenta heroku
* [Crear nuevo proyecto](https://dashboard.heroku.com/new-app)
* Descargar en instalar GIT - Subir nuestro proyecto a GITHUB
* [Descargar e instalar Heroku CLI](https://devcenter.heroku.com/articles/heroku-cli)

  Para instalarlo en Mac utilizar la instrucción:
  
        brew tap heroku/brew && brew install heroku
      
* Crear un proyecto Java usando Maven
  la construcción del proyecto creará el archivo -1.war en la carpeta de destino
  Podemos crear el archivo war desde un jar:
  
        jar cvf servicioweb.war /ServicioWeb
  
* Inicializar Git en la carpeta del proyecto

          git init
          git add .
          git commit -am "Servicio Web Java - Primer commit"
    
* Implementar la aplicación en heroku utilizando heroku-cli
    
          heroku login
    
* Instalar heroku-cli-deploy plugin
    
          heroku plugins:install heroku-cli-deploy
    
* Deploy app on heroku
   
          heroku war:deploy target/<war_filename>.war --app <heroku-app-name>
  
* Lo ejecutamos

      heroku open --app java-trasslink
