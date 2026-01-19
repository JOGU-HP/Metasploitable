Instalacion y configuracion de Metasploitable en Kali Linux

En esta documentacion, se documentara el despliegue de la maquina vulnerable Metasploitable, configuraciones y algunos pasos extra para llevar a cabo las mejores practicas sin complicaciones que comprometan al estudio y practica del pentest

Para estas practicas, se usaran 2 maquinas fisicas, una que contiene Kali Linux y otra que contiene Metasploitable en VirtualBox para simular un entorno mas realista

**Descarga e instalacion

En el navegador Brave, accediendo al buscador de Google, se escribe Metasploitable 2 en formato .zip, para despues descomprimirlo y con ello configurar VirtualBox

En VirtualBox, se le coloca un nombre a la maquina, y en la seccion de Create a New Virtual Hard Disk, se selecciona 
Use an Existing Hard Disk File para seleccionar el archivo que esta en la carpeta descomprimida de Metasploitable
![disk](https://github.com/JOGU-HP/Metasploitable/blob/75a5020d2d6ac83dcc2a8289135ae84819260577/Images/instalacion/disk.png)


**Configuracion

Ahora se inicia Metasploitable como se haria con cualquier sistema operativo, pero ocurre un primer error
![error](https://github.com/JOGU-HP/Metasploitable/blob/75a5020d2d6ac83dcc2a8289135ae84819260577/Images/instalacion/Error.png)

El error es con noapic, asi que se procede a buscar una solucion por internet y se llega al siguiente video https://www.youtube.com/watch?v=HCzbYKx2178

Que consiste basicamente en utilizar VirtuaBox como variable de entorno para usar comandos como vboxmanage, usando la ruta de la carpeta de VirtualBox y colocarla como variable de entorno del sistema

-Abrir powershell

-Escribir vboxmanage showinfo -Nombre de la maquina-

Localizar el parametro UUID y copiar la serie de numeros y letras para realizar los siguientes pasos

Escribir vboxmanage modifyvm UUID --acpi off

Despues vboxmanage modifyvm UUID --ioapic off

Y con ello el error de noapic estara solucionado, dejando poder iniciar la maquina vulnerable exitosamente
(Para esta solucion, la maquina Metasploitable debe estar apagada)

![solucion](https://github.com/JOGU-HP/Metasploitable/blob/75a5020d2d6ac83dcc2a8289135ae84819260577/Images/instalacion/solucion.png)

Ahora se realiza una primera configuracion referente a la red de ethernet, como se usara una red local que no afecte a otros dispositivos y con un router aislado es necesario que se realice una conexion y comunicacion entre 2 dispositivos (atacante y victima)

Al escribir ip a no mostraba ninguna red, en eth0 no mostraba alguna ip asi que se levanto el servicio dhcp con el comando -sudo dhclien eth0-

Debe mostrar informacion con una ip

Al escribir de nuevo ip a ahora si muestra conexion al router y la asignacion de una IP
![config red](https://github.com/JOGU-HP/Metasploitable/blob/75a5020d2d6ac83dcc2a8289135ae84819260577/Images/instalacion/configuracion%20%20de%20red.png)

Ahora que la conexion ya es detectada por Metasploitable, en Kali, se conecta via ethernet para la asignacion de una IP, asi que se conecta de forma fisica el cable ethernet al equipo y con ayuda del comando ip a muestra la ip que el router asigna a los equipos
![kali ip](https://github.com/JOGU-HP/Metasploitable/blob/2622ac3ca63d97bdc522f4550e78302d1202ad17/Images/instalacion/ip%20atack.png)


Ahora que ambos equipos estan conectados localmente a un mismo router, se hace un ping de comprobacion para verificar la comunicacion la cual es correcta con el envio y recibimiento de paquetes

De victima a atacante
![ping vic](https://github.com/JOGU-HP/Metasploitable/blob/2622ac3ca63d97bdc522f4550e78302d1202ad17/Images/instalacion/ping%20victima.png)



De atacante a victima



![ping atack](https://github.com/JOGU-HP/Metasploitable/blob/2622ac3ca63d97bdc522f4550e78302d1202ad17/Images/instalacion/ping%20atacante.png)

Con este ping, se comprueba la correcta instalacion y configuracion de la maquina Metasploitable

Conclusiones

Con la descarga e instalacion asi como configuracion de las maquinas para pentest me ha ayudado a recordar algunos pasos para configuraciones necesarias para la correcta comunicacion y ejecucion de programas, como VirtuaBox sin errores y tambien
de parametros necesarios como desactivar o activar ciertas configuraciones, tambien el aprendizaje de usar comandos como dhcp para la deteccion de un cable ethernet y usar herramientas ya conocidas como ping para establecer comunicacion entre las maquinas donde se haran pruebas y reforzamiento de conocimientos
