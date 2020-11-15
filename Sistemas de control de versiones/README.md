# Sistemas de control de versiones
En este documento vamos a ver los pasos principales sobre como trabajar con un repositorio de GitHub desde la herramienta git en sistemas operativos Linux.

A continuación vamos a ir paso a paso por todos los puntos necesarios para llevarlo a cabo.

## Instalación.
Lo primero que vamos a tener que hacer antes de usar la herramienta git va a ser instalarla en nuestro ordenador, para ello utilizaremos el instalador de paquetes de nuestra máquina.

### Distribuciones con gestor de paquetes apt ( Ubuntu / Debian )
~~~
$ sudo apt install git
~~~
### Distribuciones con gestor de paquetes yum ( Red Hat / Fedora / CentOS )
~~~
$ sudo yum install git
~~~
### Distribuciones con gestor de paquetes pacman ( Arch Linux / Manjaro )
~~~
$ sudo pacman - S git
~~~

Una vez lo tengamos instalado comprobaremos si se ha instalado correctamente con el siguiente comando

~~~
$ git --version
> git version 2.24.3
~~~

Si nos devuelve un resultado similar al descrito en el bloque de código superior significará que lo hemos hecho correctamente, en caso contrario probaremos las siguientes soluciones:

- Cerrar la consola y volver a abrirla
- Reiniciar la máquina
- Volver a instalar git

## Configuración.
A continuacion vamos a hacer la configuracion básica para que nuestro git funcione correctamente y para poder utilizarlo sin necesidad de iniciar sesión cada vez que tengamos que hacer algun cambio en el repositorio.

### Configuraciones globales de git
Para funcionar git requiere que el usuario haya configurado como mínimo dos variables de configuración global: su nombre y su correo eléctronico.

Para ello utilizaremos los siguientes comandos:

~~~
$ git config --global user.name "<Tu nombre>"
$ git config --global user.email "<tu_email@example.com>"
~~~

Para comprobar si lo hemos hecho correctamente y se han guardado las configuraciones utilizaremos el siguiente comando:

~~~
$ git config -–global –list
> name = Rubén Cabrera
> email = fireshafter@hotmail.com
~~~

Si hemos recibido un resultado similar pero con nuestros datos, significará que lo hemos hecho correctamente, si falta alguno de los datos o ambos comprueba que has copiado los comandos anteriores con la sintaxis correcta y que has añadido las dobles comillas ( ```" "``` ) al principio y al final de cada uno de los datos que has guardado.

## Configuraciones remotas de git ( autenticación en GitHub ).
En esta sección vamos a ver como conectarnos de forma remota a GitHub con nuestro usuario, de forma que podamos