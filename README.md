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
> git version 2.25.1
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
$ git config --global --list
> user.name=Rubén Cabrera
> user.email=rcabrera@agil.com
~~~

Si hemos recibido un resultado similar pero con nuestros datos, significará que lo hemos hecho correctamente, si falta alguno de los datos o ambos comprueba que has copiado los comandos anteriores con la sintaxis correcta y que has añadido las dobles comillas ( ```" "``` ) al principio y al final de cada uno de los datos que has guardado.

### Configuraciones remotas de git ( autenticación en GitHub ).
En esta sección vamos a ver como conectarnos de forma remota a GitHub con nuestro usuario, de forma que podamos hacer todo tipo de operaciones remotas como `push` sin necesidad de estar constantemente introduciendo nuestras credenciales, para ello tendremos que seguir los siguientes pasos:

#### Crear un clave pública RSA
Para que GitHub sepa que somos nosotros al hacer cualquier cambio necesitaremos una forma de indentificarnos, y esta será por medio de una clave RSA, la cual crearemos y más adelante añadiremos como clave válida en nuestra cuenta de GitHub para que siempre que le lleguen peticiones con esta clave sepa que somos nosotros.

Para crear la clave utilizaremos el comando `ssh-keygen`, cabe decir que la clave ha de guardarse en un directorio llamado .ssh dentro de nuestra carpeta personal para que funcione por lo que para ello escribiremos los siguienes comandos:

~~~
$ cd ~
$ mkdir .ssh
$ cd .ssh
$ ssh-keygen -t rsa -C "<tu_email@example.com>"
> Enter file in which to save the key (/home/fireshafter/.ssh/id_rsa): 
> Enter passphrase (empty for no passphrase): 
> Enter same passphrase again: 
> Your identification has been saved in /home/fireshafter/.ssh/id_rsa
> Your public key has been saved in /home/fireshafter/.ssh/id_rsa.pub
> The key fingerprint is:
> SHA256:RMtYtAm+wOwyALywAo3aIW1QmYua3gZw3NE2/wESKbA rcabrera@agil.com
> The key's randomart image is:
> +---[RSA 3072]----+
> |+*o+ .o++        |
> |*.B+o.**.+       |
> |=BE+++o+*.       |
> |*o=... o. .      |
> |+oo . . S. .     |
> |o. o      .      |
> |. o              |
> | . o             |
> |  .              |
> +----[SHA256]-----+
~~~

Al ejecutar el comando nos mostrara varios _`prompts`_ preguntando donde queremos guardar las claves y si queremos usar un _`passphrase`_ en nuestro caso no vamos a necesitar hacer nada de eso, por lo que los dejaremos vacíos y presionaremos enter para omitirlos.

#### Subir nuestra clave pública a GitHub

Ahora necesitaremos copiar nuestra clave pública para añadirla a nuestra cuenta de github, para ello haremos un cat para mostrar su contenido y lo copiaremos.

~~~
$ cat id_rsa.pub
> ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQC6LdoNz7TkQhFW147y53df5k+TCILRMBfp2c/LzkR97TJv/6dNtbqIH3vnuSvD7VxtH0eKk39zv9VATPORgU1kgogzNoVzlEly3+Z9b1pzdFxyxjjtF8/W5naxdzP4M3Y3xWHLwbg1p630R0unxdEZo5bCxo3YYWZreTCiQsbaUh+4i4K9275ZqF3rGTZub+wxLd0oldzh/Pw0GhH/TMPsd02Dbu9hn5oQjzNg/g+hYcJJvTF4XBez8ckKV2VsV8dfzXyulf2x5eL61x5S9pvy/8UCYA9f9Rd6fovOeaYSVbaEOU7fCI5OC93nKaIX3+YNL1I6PcqZ67sglxeGJZ4LgpMnybOpCvndpM6aT4SW31/pHH9QevGVAq1DSIpLhdqfq2hI7LH2X/mO1fdkNGb/rxU2/W1RpAe3gYKgUC7AfF8wqm8vt/wjEctCcd3w9NpXQvjVRebNuST+QvUAp87LwPPih3BGeSpZWJzDaypVtWBuS1PO3L/zAPa190HDSes= rcabrera@agil.com
~~~

Una vez copiado iniciaremos sesión en GitHub desde un navegador y clicaremos en el apartado de ajustes de usuario.

![alt text](https://i.imgur.com/UKnY4Dy.png "Ajustes GitHub")

Una vez allí accederemos al apartado de claves SSH.

![alt text](https://i.imgur.com/u1ZyZbW.png "Ajustes claves SSH")

Dentro de la sección daremos click sobre la opción **New SSH key** para añadir una nueva clave SSH.

![alt text](https://i.imgur.com/UBiBHJb.png "Añadir nueva clave")

Finalmente para añadir la clave le añadiremos un título descriptivo para poder identificarla facilmente cuando ya tengamos varias de estas, y pegaremos dentro del apartado key nuestra clave pública ( la que hemos copiado previamente ) y para terminar le daremos click al botón **Add SSH Key** para guardar los cambios.

![alt text](https://i.imgur.com/ZnpyQrO.png "Creando nueva clave")

Si lo hemos hecho todo bien ahora podremos ver nuestra clave pública listada en la zona de claves SSH como podemos observar en la imagen de abajo:

![alt text](https://i.imgur.com/0zlAXen.png "Nuestra primera clave")

Ahora tendremos que conectarnos desde nuestro ordenador por vía SSH al servidor de GitHub para guardar las _`fingerprints`_ y terminar el proceso.

Para ello ejecutaremos el siguiente comando:

~~~
$ ssh -T git@github.com
> The authenticity of host 'github.com (140.82.121.3)' can't be established.
> RSA key fingerprint is SHA256:nThbg6kXUpJpKul7E1IGOCspRomTxdCARLviKw6E5SY8.
> Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
> Warning: Permanently added 'github.com,140.82.121.3' (RSA) to the list of known hosts.
> Hi Fireshafter! You've successfully authenticated, but GitHub does not provide shell access.
~~~

Cuando nos pregunte que si queremos aceptar la fingerprint del servidor escribiremos `yes`.

Y con esto hemos terminado con la instalacion de git y su configuración en GitHub.