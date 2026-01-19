Explotacion del puerto 21 Metasploitable

En esta documentacion, se muestra como se ha explotado la primer vulnerabilidad de Metasploitable (puerto 21), para recordar los pasos hacia vulnerabilidades con las que ya se ha trabajado con anterioridad y demostrar el conocimiento adquirido en practicas anteriories

>CONEXION

Para comenzar, se realiza un ping para comprobar la conectividad y comunicacion entre las 2 maquinas atacante y victima, a traves del envio de paquetes, recibiendo los paquetes demostrando la correcta comunicacion entre ambos equipos

![ping](https://github.com/JOGU-HP/Metasploitable/blob/308ddb06aa54f0b477f7cb59fe276d75b1d77f2b/Images/explotation1/ping.png)


>Reconocimiento

Ahora, se realiza un escaneo de puertos con nmap, usando la sintaxis nmap -p- -sS -sC -sV --min-rate 1000 192.168.0.198, para observar que puertos estan abiertos y con ello realizar un primer ataque

Veo que el primer puerto abierto, es el puerto 21 vsftpd en la version 2.3.4 lo que indica una puerta trasera

![scan](https://github.com/JOGU-HP/Metasploitable/blob/308ddb06aa54f0b477f7cb59fe276d75b1d77f2b/Images/explotation1/scan.png)


>Eleccion de herramienta

Al ver el puerto vsftpd en la version 2.3.4 determino que puede usarse Metasploit y usar un exploit con el que ya he trabajado en maquinas anteriories (DockerLabs) y enfocado a puertas traseras

Inicio Metasploit

Escribo search vsftpd 2.3.4 para encontrar el exploit y usarlo

![search](https://github.com/JOGU-HP/Metasploitable/blob/308ddb06aa54f0b477f7cb59fe276d75b1d77f2b/Images/explotation1/search.png)

>Explotacion

Encontrado el exploit, escribo use 0 para utilizar el exploit encontrado

Usando el exploit encontrado, procedo a observar que parametros son necesarios para ejecutar el exploit con show options, observando que se necesita RHOSTS para proceder con el ataque

Se configura escribiendo set RHOSTS IP de la victima

![options](https://github.com/JOGU-HP/Metasploitable/blob/308ddb06aa54f0b477f7cb59fe276d75b1d77f2b/Images/explotation1/options.png)

Configurado RHOSTS ejecuto el exploit y marca un primer error, indicando que se ejecuto el exploit pero no se creo sesion

![error](https://github.com/JOGU-HP/Metasploitable/blob/308ddb06aa54f0b477f7cb59fe276d75b1d77f2b/Images/explotation1/first%20error.png)

MI primer solucion es de nuevo ejecutar el exploit y reescribir los parametros configurados con anterioridad:

set RHOSTS IP de la victima

run

Y ahora si ha encontrado una shell, que al escribir whoami soy root

![root](https://github.com/JOGU-HP/Metasploitable/blob/308ddb06aa54f0b477f7cb59fe276d75b1d77f2b/Images/explotation1/exploit.png)
