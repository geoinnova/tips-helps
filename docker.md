# Ejemplos de docker-compose.yml

```sh
version: '3'

services:
  nginx:
    build: ./nginx/
    container_name: hargadunia-nginx
    ports:
      - 80
    depends_on:
      - php
    volumes:
    - ./www/:/var/www/html
    networks:
      mysql-net:
        ipv4_address: 172.8.0.101
    restart: unless-stopped
  php:
    build: ./php/
    container_name: hargadunia-php
    expose:
      - 9000
    volumes:
      - ./www/:/var/www/html
    networks:
      mysql-net:
        ipv4_address: 172.8.0.100
    restart: unless-stopped

networks:
  mysql-net:
    external:
      name: mysql_bridge
```

.env (en el raiz)

```sh
# MySQL docker network configuration
MYSQL_DOCKER_NETWORK=mysql_bridge
NGINX_IP=172.8.0.101
PHP_IP=172.8.0.100
```

/php/Dockerfile

```sh
FROM php:5.6-fpm

RUN apt-get update && apt-get -y --no-install-recommends install \
    # gd
    libfreetype6-dev libjpeg62-turbo-dev libmcrypt-dev libpng12-dev \
    # intl
    # libicu-dev \
    # imageick
    # libmagickwand-dev \
    # memcached    
    libmemcached-dev zlib1g-dev \
    && pecl install memcached-2.2.0 \
    && docker-php-ext-enable memcached \
    && docker-php-ext-install mysql pdo_mysql mbstring \
    && echo date.timezone=Asia/Jakarta >> /usr/local/etc/php/conf.d/php.ini \
    && echo upload_max_filesize = 100M >> /usr/local/etc/php/conf.d/php.ini \
    && echo post_max_size = 108M >> /usr/local/etc/php/conf.d/php.ini \
    # && echo extension=memcached.so >> /usr/local/etc/php/conf.d/memcached.ini \
    && apt-get autoremove -y \
    && apt-get \
    && rm -rf /tmp/* /var/tmp/*
    
```

/nginx/Dockerfile

```sh
FROM nginx:alpine

COPY ./default.conf /etc/nginx/conf.d/default.conf
```

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
	
Una vez instalado te indicará una serie de pasos que puedes seguir:

	==> Next steps:
	- Run `brew help` to get started
	- Further documentation: 
	    https://docs.brew.sh
	- Install the Homebrew dependencies if you have sudo access:
	    sudo apt-get install build-essential
	    See https://docs.brew.sh/linux for more information
	- Add Homebrew to your PATH in /home/vagrant/.bash_profile: 
	    echo 'eval $(/home/linuxbrew/.linuxbrew/bin/brew shellenv)' >> /home/vagrant/.bash_profile
	    eval $(/home/linuxbrew/.linuxbrew/bin/brew shellenv)
	- We recommend that you install GCC:
	    brew install gcc


	echo 'eval $(/home/linuxbrew/.linuxbrew/bin/brew shellenv)' >> /home/vagrant/.bash_profile
	eval $(/home/linuxbrew/.linuxbrew/bin/brew shellenv)
	    

Instalamos php

	brew install php
	
	


