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

### Instalar un paquete
    pip3 install BeautifulSoup4
    pip3 install requests

## El Python del sistema [Python 2.7.10 (default, Feb 6 2017, 23:53:20)], que en macOS Sierra (versión actual 10.12.4) no debes actualizarlo. Muchas cosas dependen de él y tu sistema podría quedar inutilizado.
[Ver fuente](https://es.stackoverflow.com/questions/64944/c%C3%B3mo-actualizar-a-python-3-desde-el-terminal-en-mac)

Tienes dos opciones:
**Homebrew**

Homebrew es un gestor de paquetes que te permite instalar muchos paquetes, incluyendo Python, de forma local, sin interferir con las versiones del sistema. Si ya tienes instalado Homebrew, solo tienes que hacer lo siguiente:

    $ brew update && brew install python

Si no has instalado Homebrew, sigue las instrucciones en su página principal.

**Pyenv**

Pyenv es un gestor de versiones de Python. Te permite instalar diferentes versiones de Python y usar la que te convenga sin que interfiera con las demás.

Personalmente te recomiendo usar el instalador que incluye una versión especial de virtualenv.

Como se usa Pyenv

Digamos que tienes un proyecto que se llama cmi, ubicado en ~/proyectos/cmi/ que usa la versión 2.7 de Python. Solo tienes que crear el entorno con el siguiente comando:

    $ pyenv install 2.7.13
    $ pyenv rehash   # para activar la nueva versión
    $ pyenv virtualenv 2.7.13 cmi

Y a continuación, en el directorio de tu proyecto, escribes lo siguiente:

    ~/proyectos/cmi$ pyenv local cmi

De este modo, cuando te cambies a ese directorio, se activará automáticamente el entorno cmi.

Si tienes otro proyecto, en ~/proyectos/sgc que necesita la versión 4.3.1 de Anaconda, la instalas, creas el entorno virtual y la activas para tu proyecto:

    ~/proyectos/sgc$ pyenv install anaconda3-4.3.1
    ~/proyectos/sgc$ pyenv rehash   # para activar la nueva versión
    ~/proyectos/sgc$ pyenv virtualenv anaconda3-4.3.1 sgc
    ~/proyectos/sgc$ pyenv local sgc

Tus entornos de Python son independientes unos de otros, puedes ocupar una versión para hacer cualquier cantidad de entornos virtuales, también independientes, etc.

Para ver todas las versiones disponibles, que son unas 300, ejecuta este comando:

    $ pyenv install --list
