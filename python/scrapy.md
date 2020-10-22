### Instalar scrapy con el instalador de paquetes de python
  pip3 install scrapy


[Tutorial Scrapy; Extraer información de Mercado Libre](https://github.com/luisramirez-m/mercadolibre-scrapy)

[Scrapy vagrant](https://github.com/sgarciapdx/scrapy-vagrant/blob/master/Vagrantfile)

https://gist.github.com/raphaelfruneaux/be9fd2051b52cdbffcd6

## Ver esto
instalar virtualenv https://www.accordbox.com/blog/scrapy-tutorial-2-how-install-scrapy-mac/

## Scrapy https://scrapy.org/

# Instalar Scrapy en un virtualenv [Tutorial](https://www.accordbox.com/blog/scrapy-tutorial-2-how-install-scrapy-mac/)

    pip3 install python3

Scrapy instalado a través del código anterior es global, por lo que está disponible en todos sus proyectos. Eso puede ser conveniente a veces, pero también puede convertirse en problemas. Entonces, ¿cómo instalar Scrapy en un entorno aislado? Por eso virtualenv creó. En mi Mac, solo algunos paquetes de Python, como pip y virtualenv, están disponibles globalmente; otros paquetes como Scrapy, Django se instalan en entornos virtuales.

Después de instalar Python a través de pip3, instalamos virtualenv

    pip3 install virtualenv
  
### Ahora podemos crear un virtualenv para que lo usemos
    cd ~
    mkdir Virtualenvs
    cd Virtualenvs
    virtualenv scrapy_env
    
#### Se ha creado un virtualenv llamado scrapy_env

Si necesitamos activar un virtualenv, simplemente usamos source

    source scrapy_env/bin/activate
    
    (scrapy_env) Mac:Virtualenvs erabasco$ 
  
Si necesitamos salir del virtualenv usamos el comando 

    deactivate


Usamos la fuente **scrapy_env/bin/active** para activar virtualenv, y ahora si instala el paquete python, todos ellos estarían en un entorno aislado, y el nombre del virtualenv se puede ver en el indicador de shell lo que significa que ahora estamos en un virtualenv. Si desea saber más sobre virtualenv, simplemente consulte esta buena guía de Python. Ya que estamos en un virtualenv, podemos empezar a instalar Scrapy.

    pip3 install scrapy
    
    scrapy
    
    
   [Creando una aplicación con Python y desplegando a Heroku](https://www.youtube.com/watch?v=PEcWR882goU)
   
   
   heroku login
   creamos la carpeta /teatro/scraper
   
    
    
    
