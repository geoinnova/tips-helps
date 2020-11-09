## Instalar Vagrant
Vagrant, una gran herramienta que facilita la creación de entornos virtuales de forma sencilla y replicable

https://xenfacil.com/paginas/scotchbox/

Utilizaremos <strong>Scotch Box</strong>, que es un Vagrant Box preconfigurado con una gama completa de funciones LAMP. Para ello previamente debemos tener instalados:

	VirtualBox
	Vagrant
      
Nos posicionamos en la carpeta donde vayamos a instalarlo y clonamos el repositorio que se indica en: https://box.scotch.io/

	git clone https://github.com/scotch-io/scotch-box my-project

- Se creará una carpeta <b>/public </b> que será donde incluyamos nuestros proyectos.

- Un archivo Vagrantfile, para configurar los valores de la máquina: https://javiermartinalonso.github.io/devops/devops/vagrant/2018/02/09/vagrant-vagrantfile.html


Y por último arrancaremos la máquina:

	vagrant up
	
(la primera vez que lo ejecutemos nos descargará la máquina)

	http://192.168.33.10

### VPDistillery (preparado para instalar WordPress)
Prepara el Vagrantfile con la instalación de WordPress. Documentación: https://github.com/flurinduerst/WPDistillery

### Dependencies

    ScotchBox (using Vagrant & Virtualbox)
    Vagrant Hostsupdater (vagrant plugin install vagrant-hostsupdater) > Es un plugin de Vagrant que crea como un 
    servidor DNS para no tener que utilizar la dirección IP sino que podamos usar un nombre de dominio
    
    vagrant plugin install vagrant-hostsupdater
    vagrant plugin uninstall vagrant-hostsupdater


#### Setup

To setup a new project running Scotch Box and WordPress, simply follow these steps:

1. In a terminal, run: `git clone https://github.com/flurinduerst/WPDistillery.git my-project`
2. Customize `wpdistillery/config.yml` to suit your needs. See [configuration file documentation](https://github.com/flurinduerst/WPDistillery/blob/master/README_CONFIG.md).
3. Inside the `Vagrantfile` add your local URL at `config.vm.hostname`. This should be the same as `wpsettings:url:` in `config.yml`.
4. Run `vagrant up` from where your `Vagrantfile` is.

Done! You can now access your project at the local URL (for example `yoursite.vm`) defined in **Step 3**. (or at http://192.168.33.10/)

**Note:** Currently there's an [issue](https://github.com/scotch-io/scotch-box/issues/296) related to [ScotchBox](https://github.com/scotch-io/scotch-box) that hinders Vagrant from mounting VirtualBox Shared folders. The solution is to install [vagrant-vbguest](https://github.com/dotless-de/vagrant-vbguest) before running vagrant. This will install the correct vbguest package into the box:

```
vagrant plugin install vagrant-vbguest
vagrant vbguest
```

https://www.busindre.com/guia_rapida_de_vagrant


### Actualizar php
Instalamos el gestor de paquetes brew
	/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
	


