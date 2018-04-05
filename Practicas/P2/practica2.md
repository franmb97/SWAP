# Práctica 2. Clonar la información de un sitio web

### Preparacion

ubuntu--> 192.168.1.10
ubuntu2--> 192.168.1.11


## Tareas a realizar

#### Aprender a copiar archivos mediante ssh.
Primero, creamos en la máquina 1 una carpeta llamada prueba y dentro de ella un archivo prueba.txt para probar la copia.
Y ponemos lo siguiente en la maquina 1:

    tar czf - prueba | ssh ubuntu2@192.168.1.11 'cat > ~/tar.tgz'
   [](https://github.com/franmb97/SWAP/blob/master/Practicas/P2/2.1.JPG)
Y nos aparecerá en la segunda máquina el archivo tar.tgz con todo el contenido de la primera máquina.

#### Clonar contenido entre máquinas.
En mi caso ya tenia instalado rsync a si que no tuve que instalarlo.

Sin ser root ejecutamos lo siguiente:

    sudo chown ubuntu:ubuntu -R /var/www
    
Y por ejemplo, clonamos la carpeta /var/www/ en el mismo sitio pero en la otra máquina

    rsync -avz -e ssh 192.168.1.11:/var/www/ /var/www/
[](https://github.com/franmb97/SWAP/blob/master/Practicas/P2/2.2.JPG)
Nos pedirá nuestra contraseña y se empezara a copiar.

#### Configurar el ssh para acceder a máquinas remotas sin contraseña

Primero tenemos que generar una clave (yo la voy a generar en la máquina dos):

    ssh-keygen -b 4096 -t rsa
    
 [](https://github.com/franmb97/SWAP/blob/master/Practicas/P1/2.3.JPG)
y le damos a enter en todas las opciones

Ahora tenemos que copiar la clave en la otra máquina

    ssh-copy-id ubuntu@192.168.1.10

Y ya solo nos queda intentar entrar desde la máquina 1 a la máquina 2, y vemos que no nos pedirá contraseña
[](https://github.com/franmb97/SWAP/blob/master/Practicas/P1/2.4.JPG)
#### Establecer tareas en cron
Tenemos que ejecutar una tarea en cron que se ejecute cada hora para mantener actualizado el contenido del directorio /var/www entre las dos máquinas.
Lo voy a hacer en la primera máquina:

    sudo nano /etc/crontab

y en este archivo tenemos que añadir la siguiente linea:

    0	*/1	*	*	*	root	rsync -avz -e ssh 192.168.1.11:/var/www /var/www/

[](https://github.com/franmb97/SWAP/blob/master/Practicas/P1/2.5.JPG)
El segundo asterisco significa cada hora, el root significa el usuario que lo realizará y la ultima orden es la misma que hemos visto en el punto dos de esta práctica.

