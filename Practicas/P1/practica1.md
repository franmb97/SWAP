 21:08 24/03/2018# Pr�ctica 1. Preparaci�n de las herramientas
Por  Francisco Antonio Mart�nez Blanco


# Preparacion

Antes de todo, deberemos instalar dos maquinas virtuales con ubuntu server, ambas deber�n llevar instalado Apache, PHP y MySQL y estar funcionando.

En mi caso las m�quinas son:
	
|                |Nombre                          |IP                         |
|-----------|-------------------------------|-----------------------------|
|1|ubuntu|192.168.1.10|
|2|ubuntu2|192.16.1.11 |


# Cuestiones a Resolver

## Acceder por ssh de una m�quina a otra.
Si queremos entrar desde la primera m�quina a la segunda deberemos introducir:

> ssh ubuntu2@192.168.1.11 
> y nos pedira la password de dicha maquina


![Imagen 1](https://github.com/franmb97/SWAP/blob/master/Practicas/P1/1.1.JPG)

Si queremos entrar desde la segunda a la primera basta con cambiar el nombre y la ip por las de la primera m�quina.
> ssh ubuntu@192.168.1.10

## Acceder mediante curl desde una m�quina a otra

Para ello, creamos en la m�quina 1 un archivo llamado hola.html y lo guardamos en var/www/html en el archivo escribire lo siguiente en formato html lo siguiente:
> <HTML> <BODY> Esto funciona  :) </BODY> </HTML> 
Y solo nos quedaria entrar desde la segunda m�quina y escribir
> curl http://192.168.1.10/hola.html

Y nos aparecer� lo siguiente:

![Imagen 2](https://github.com/franmb97/SWAP/blob/master/Practicas/P1/1.4.JPG)