[Descarga Python](https://www.python.org/downloads/)

[Curso Pildoras informáticas](https://www.youtube.com/watch?v=u4I9PqhqCo8&list=PLU8oAlHdN5BlvPxziopYZRd55pdqFwkeS&index=4)

## Una vez instalado crear variable de entorno
Las variables de entorno se encuentran en el fichero .bash_profile en la carpera del usuario, normalmente la ruta por defecto al abrir una consola.

    nano .bash_profile

Dentro de este fichero, si queremos incluir en el Path la variable java_home incluiremos la siguiente linea:

    PATH="/Library/Frameworks/Python.framework/Versions/3.8/bin:${PATH}"
    export PATH

Para reiniciar solamente el bash:

    source .bash_profile

Comprobamos que se ejecuta:

    python -version
    
Ahora si quisieramos ejecutar el archivo python desde el terminal solo tendríamos que escribir: Python y la dirección donde está el programa,

    Por ejemplo:   Python c:\python\1.py


### Cómo configurar Visual Studio Code para programar en Python 
https://geekytheory.com/configurar-visual-studio-code-programar-python
*https://www.mclibre.org/consultar/python/otros/vsc-python-configuracion.html

### Funciones
        type()=> tipo de la variable
