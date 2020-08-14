## Instalar Vagrant
Vagrant, una gran herramienta que facilita la creación de entornos virtuales de forma sencilla y replicable

https://xenfacil.com/paginas/scotchbox/

En vez de Vagrant vamos a instalar <strong>scotch box </strong>, para ello previamente debemos:

	Instalar VirtualBox
	Instalar Vagrant
      
Nos posicionamos en la carpeta donde vayamos a instalarlo y clonamos el repositorio que se indica en: https://box.scotch.io/

	git clone https://github.com/scotch-io/scotch-box my-project

- Se creará una carpeta <b>/public </b> que será donde incluyamos nuestros proyectos.

- Un archivo Vagrantfile, para configurar los valores de la máquina: https://javiermartinalonso.github.io/devops/devops/vagrant/2018/02/09/vagrant-vagrantfile.html


Y por último arrancaremos la máquina:

	vagrant up
	
(la primera vez que lo ejecutemos nos descargará la máquina)

	http://192.168.33.10

### VPDistillery (preparado para instalar Wordpress)
