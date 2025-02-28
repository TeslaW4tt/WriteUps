# SimpleCTF


---

Iniciamos la maquina usando la VPN de TryHackMe

![Escaneo de puertos](Imagenes/SimpleCTF/1.PNG)

## Reconocimiento

Una vez conectados a la maquina realizamos un escaneo con nmap 

![Escaneo de puertos](Imagenes/SimpleCTF/2.PNG)

### Respuesta 1

Sabemos que tenemos 2 puertos por debajo del puerto 1000

- ftp (port 21) y 80 (http)

![Escaneo de puertos](Imagenes/SimpleCTF/3.PNG)


### Respuesta 2

 El servicio que corre en el puerto mas alto es ssh 

 ![Escaneo de puertos](Imagenes/SimpleCTF/4.PNG)

 ![Escaneo de puertos](Imagenes/SimpleCTF/5.PNG)


 ### Respuesta 3

 Haciendo un fuzzing web con dirb http://10.10.5.93 nos sale como un directorio 10.10.5.93/simple/
Accediendo a la web podemos ver que tenemos una versión de CMS 2.2.8 

![Escaneo de puertos](Imagenes/SimpleCTF/6.PNG)


Buscamos esa version de CMS en Database 

![Escaneo de puertos](Imagenes/SimpleCTF/7.PNG)

En los detalles del CVE sabemos que el codigo de CVE es 2019-9053

![Escaneo de puertos](Imagenes/SimpleCTF/8.PNG)

Descargamos el CVE 

![Escaneo de puertos](Imagenes/SimpleCTF/9.PNG)


### Respuesta 4

En el titulo del CVE  sabemos que es vulnerable a SQL injection 
![Escaneo de puertos](Imagenes/SimpleCTF/10.PNG)

### Respuesta 5

Utilizando searchsploit buscamos un exploit para ejecutar y sabemos que tenemos un exploit en el directorio /usr/share/exploitdb/exploits/php/webapps/46635.py asi que lo copiamos en nuestra carpeta local con el nombre de cmsexploit.py
![Escaneo de puertos](Imagenes/SimpleCTF/11.PNG)

Al ejecutarlo utilizando python2 obtenemos un error del modulo termocolor
![Escaneo de puertos](Imagenes/SimpleCTF/12.PNG)

Asi que para instalar termcolor primero debemos instalar pip para python2
![Escaneo de puertos](Imagenes/SimpleCTF/13.PNG)

Una vez instalado pip instalamos termcolor 
![Escaneo de puertos](Imagenes/SimpleCTF/14.PNG)

Hacemos la prueba de que termcolor funciona correctamente 
![Escaneo de puertos](Imagenes/SimpleCTF/15.PNG)

Ahora ejecutamos el exploit para obtener el usuario y contraseña utilizando el exploit 
![Escaneo de puertos](Imagenes/SimpleCTF/16.PNG)

 ### Respuesta 6

 Los usuarios y contraseña los obtenemos 

 ![Escaneo de puertos](Imagenes/SimpleCTF/17.PNG)

### Respuesta 7

Sabemos que una manera de acceder a la maquina es por ssh el cual es un servicio que ==No corre en el port 22== si no en el 2222

![Escaneo de puertos](Imagenes/SimpleCTF/19.PNG)

### Respuesta 8

Accedemos utilizando ssh con el usuario y contraseña que obtuvimos
![Escaneo de puertos](Imagenes/SimpleCTF/20.PNG)


### Respuesta 9

Una vez accedemos como el usuario mitch hacemos un `ls` y posteriormente leemos el archivo user.txt con `cat` el cual tiene nuestra user flag 

![Escaneo de puertos](Imagenes/SimpleCTF/21.PNG)

### Respuesta 10

Hacemos un `cd ..` para ir al directorio home y sabemos que existe otro usuario llamado *sunbath*

![Escaneo de puertos](Imagenes/SimpleCTF/22.PNG)

### Respuesta 11

Ejecutamos un sudo -l para averiguar si podemos ejecutar algún binario como root o como sunbath.
Asi que vemos que se puede ejecutar como root el binario vim


![Escaneo de puertos](Imagenes/SimpleCTF/23.PNG)

### Respuesta 12

Para hacer el pivoting hacia el usuario root usamos la web de GTFObins y buscamos el binario vim.
Utilizamos el comando encontrado en GTFObins

![Escaneo de puertos](Imagenes/SimpleCTF/24.PNG)

Nos regresa una shell y ahora somos root 

![Escaneo de puertos](Imagenes/SimpleCTF/25.PNG)

### Respuesta 13

En el directorio /root/root.txt esta la root flag asi que la leemos con cat 

![Escaneo de puertos](Imagenes/SimpleCTF/26.PNG)


