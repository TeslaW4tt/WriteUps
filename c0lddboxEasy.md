
# Escaneo 
### Realizamos un escaneo utilizando nmap 


![Escaneo de puertos](Imagenes/c0lddbox/1.PNG)

En los resultados del escaneo sabemos que los puertos 80 y 4512 están abiertos, asi que colocamos la dirección IP en el navegador para acceder a la pagina que almacena

![Escaneo de puertos](Imagenes/c0lddbox/2.PNG)

No encontramos nada interesante por lo que hacemos escaneo de directorios 

![Escaneo de puertos](Imagenes/c0lddbox/3.PNG)


Encontramos algunos directorios interesantes como wp-admin y wp-content asi que usaremos la herramienta WPScan para escanear el WordPress
enumeramos utilizando 
- `-e u para enumerar usuarios`

![Escaneo de puertos](Imagenes/c0lddbox/4.PNG)

Encontramos interesante que existen 3 usuarios 
- c0ldd
- hugo
- philip


![Escaneo de puertos](Imagenes/c0lddbox/5.PNG)


Utilizando el directorio accedemos con la ip/wp-login.php para colocar el usuario y contraseñas 

![Escaneo de puertos](Imagenes/c0lddbox/6.PNG)

Ahora volvemos a enumerar ahora con el directorio /wp-login.php y hacemos la prueba utilizando la wordlist y el usuario *c0ldd*


![Escaneo de puertos](Imagenes/c0lddbox/7.PNG)

Obtenemos la contraseña para el usuario c0ldd 


![Escaneo de puertos](Imagenes/c0lddbox/8.PNG)

Con el usuario c0ldd y la password que encontramos accedemos en login de wordpress

![Escaneo de puertos](Imagenes/c0lddbox/9.PNG)

Entramos al panel de de administración de wordpress
![Escaneo de puertos](Imagenes/c0lddbox/10.PNG)

Entramos a apperance > Editor > 404 template  y vemos que existe una sección donde podemos insertar codigo para ejecutar 
![Escaneo de puertos](Imagenes/c0lddbox/11.PNG)


En nuestra terminal de la maquina atacante buscamos una reverse-shell 

![Escaneo de puertos](Imagenes/c0lddbox/12.PNG)

Copiamos la reverse a nuestro directorio local que creamos para la maquina 


![Escaneo de puertos](Imagenes/c0lddbox/13.PNG)


Editamos el código php con nuestra IP y el puerto 4444

![Escaneo de puertos](Imagenes/c0lddbox/14.PNG)

Una vez hayamos editado el código copiamos el contenido del archivo shell.php al portapapeles


![Escaneo de puertos](Imagenes/c0lddbox/15.PNG)

Pegamos el código en la sección de wordpress que vimos anteriormente 

![Escaneo de puertos](Imagenes/c0lddbox/16.PNG)

Para ejecutar el código que subimos primero debemos ponernos a la escucha utilizando netcat

![Escaneo de puertos](Imagenes/c0lddbox/17.PNG)

Ejecutamos el código utilizando el siguiente directorio que es donde se sube el código que pegamos 

![Escaneo de puertos](Imagenes/c0lddbox/18.PNG)


Una vez lo ejecutamos nos devuelve acceso a la maquina vulnerable 

![Escaneo de puertos](Imagenes/c0lddbox/19.PNG)

Una vez dentro de la maquina listamos el contenido 
![Escaneo de puertos](Imagenes/c0lddbox/20.PNG)

Dentro de home/c0ldd sabemos que existe el archivo user.txt pero con el usuario que somos (www-data) no podemos leer el contenido.
Es necesario ser usuario *c0ldd*

![Escaneo de puertos](Imagenes/c0lddbox/21.PNG)

Sabemos que archivos de configuración muy comúnmente están guardados en el directorio `/var/www/html` donde existe el archivo  `wp-settings.php`.
Leemos el contenido y encontramos la password de c0ldd

![Escaneo de puertos](Imagenes/c0lddbox/22.PNG)
![Escaneo de puertos](Imagenes/c0lddbox/23.PNG)

Cambiamos al usuario *c0ldd* utilizando la password que encontramos

![Escaneo de puertos](Imagenes/c0lddbox/24.PNG)

Una vez que somos el usuario c0ldd nos ubicamos dentro del directorio del usuario c0ldd y listamos el contenido.

![Escaneo de puertos](Imagenes/c0lddbox/25.PNG)

Ahora si podemos leer el contenido de la user.txt

![Escaneo de puertos](Imagenes/c0lddbox/26.PNG)

Para hacer la escalada de privilegios a root ejecutamos el comando sudo -l
![Escaneo de puertos](Imagenes/c0lddbox/27.PNG)

Podemos ejecutar el binario ftp para escalar privilegios por lo que utilizando la web de GTFObins buscamos el comando para ftp

![Escaneo de puertos](Imagenes/c0lddbox/28.PNG)

Ejecutamos el comando para escalar privilegios y somos root

![Escaneo de puertos](Imagenes/c0lddbox/29.PNG)

Listamos el contenido en el directorio root y encontramos la root.txt

![Escaneo de puertos](Imagenes/c0lddbox/30.PNG)










