# TomGhost
---

## Reconocimiento

Realizamos una escaneo con nmap 

![Escaneo de puertos](Imagenes/TomGhost/1.PNG)

Tenemos el puerto 22,53,8009 y 8080 para http asi que ponemos la dirección IP en el navegador y vemos la siguiente pagina

![Escaneo de puertos](Imagenes/TomGhost/2.PNG)

Realizamos un fuzzing usando *gobuster* pero no vemos nada interesante 
![Escaneo de puertos](Imagenes/TomGhost/3.PNG)

Dado que no vemos nada interesante en el fuzzing recordamos que tenemos un servicio ajp13 en el puerto 8009,asi que utilizando `searchsploit` buscamos un exploit que nos pueda funcionar 
![Escaneo de puertos](Imagenes/TomGhost/4.PNG)

Con ayuda de locate ubicamos el exploit y lo copiamos en nuestra carpeta local de la maquina de TomGhost
![Escaneo de puertos](Imagenes/TomGhost/5.PNG)

Una vez creado lo ejecutamos para saber que parámetros necesitamos colocar 
![Escaneo de puertos](Imagenes/TomGhost/6.PNG)

Hacemos una búsqueda en la web de ajp13 y sabemos que vulnera el directorio siguiente 
/WEB-INF/web.xml
![Escaneo de puertos](Imagenes/TomGhost/7.PNG)


Ahora que sabemos los parametros que necesitamos ejecutamos el exploit
![Escaneo de puertos](Imagenes/TomGhost/8.PNG)

El script nos muestra un usuario y una password
![Escaneo de puertos](Imagenes/TomGhost/9.PNG)


### Respuesta 1

Sabemos que la maquina tiene abierto el puerto ssh asi que utilizamos el user y password que encontramos anteriormente para conectarnos a la maquina 

![Escaneo de puertos](Imagenes/TomGhost/10.PNG)

Una vez dentro ejecutamos nos vamos al directorio home y ejecutamos el comando ls para listar el contenido.
Podemos ver que tenemos dos usuarios *merlin* y *skyfuck* asi que haremos el intento de cambiarnos al directorio del usuario *merlin*
![Escaneo de puertos](Imagenes/TomGhost/11.PNG)


Nos cambiamos exitosamente al directorio de *merlin*, listamos el contenido y podemos ver la primera flag 
![Escaneo de puertos](Imagenes/TomGhost/12.PNG)

---

### Respuesta 2

Regresando al directorio de *skyfuck* si listamos podemos ver que existen 2 archivos .pgp y .asc,los cuales son archivos encriptados 

![Escaneo de puertos](Imagenes/TomGhost/13.PNG)

Para estos archivos utilizaremos nuestra maquina local atacante por lo que tenemos que descargarlos en nuestra maquina.
Necesitamos levantar un servidor desde la maquina victima con python 

![Escaneo de puertos](Imagenes/TomGhost/14.PNG)

En nuestra maquina atacante obtenemos los dos archivos utilizando `wget` 
![Escaneo de puertos](Imagenes/TomGhost/15.PNG)

Una vez que tenemos  los archivos  ejecutamos el comando `pgp --decrypt credential` por lo que nos arroja la siguiente ventana 
![Escaneo de puertos](Imagenes/TomGhost/16.PNG)

Es necesaria una contraseña para desencriptar el archivo asi que utilizaremos la herramienta de *john* para desencriptar 

Primero debemos  convertir el archivo para que pueda ser leido por jhon 
![Escaneo de puertos](Imagenes/TomGhost/17.PNG)

Una vez creado el archivo hash utilizamos *john* para desencriptar 
![Escaneo de puertos](Imagenes/TomGhost/18.PNG)


Ahora importamos la clave privada *tryhackme.asc* y nos solicitará la contraseña anteriormente encontrada 
![Escaneo de puertos](Imagenes/TomGhost/19.PNG)

Obtenemos la contraseña para el usuario *merlin* 
![Escaneo de puertos](Imagenes/TomGhost/20.PNG)

Cambiamos al usuario *merlin* y colocamos la contraseña que anteriormente encontramos 
![Escaneo de puertos](Imagenes/TomGhost/21.PNG)

Ejecutamos el comando `sudo -l` para saber si podemos ejecutar algun binario como root
![Escaneo de puertos](Imagenes/TomGhost/22.PNG)

Sabemos que zip lo podemos ejecutar como *root* sin contraseña asi que buscamos en GTFObins el binario y el comando para ejecutar y convertirnos en *root*
![Escaneo de puertos](Imagenes/TomGhost/23.PNG)

Ejecutamos los comandos para convertirnos en root y lo logramos 
![Escaneo de puertos](Imagenes/TomGhost/24.PNG)

Obtenemos la flag para el usuario root

![Escaneo de puertos](Imagenes/TomGhost/25.PNG)



#                               P W N E D !

