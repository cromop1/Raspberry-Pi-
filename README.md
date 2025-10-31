<p align="center">
  <img src="https://i.imgur.com/Me0KRjX.png" width="100%" alt="Banner Proyecto Integrador 2025">
</p>

<p align="center">
  <img src="https://i.imgur.com/RVGaecC.png" width="100%" alt="Banner Proyecto Integrador 2025">
</p>







<p align="center">
  <img src="https://i.imgur.com/BBMgp0q.png" width="100%" alt="Banner Proyecto Integrador 2025">
</p>

<p align="center">
  <img src="https://custom-icon-badges.demolab.com/badge/Contribuidores-4-6F42C1.svg?logo=people&logoColor=white">
  <img src="https://custom-icon-badges.demolab.com/badge/Entorno-Produccion-FD7E14.svg?logo=gear&logoColor=white">
  <img src="https://custom-icon-badges.demolab.com/badge/Repo-GitHub-181717.svg?logo=github&logoColor=white">
  <img src="https://custom-icon-badges.demolab.com/badge/Status-Finalizado-28A745.svg?logo=check-circle&logoColor=white">
  <img src="https://custom-icon-badges.demolab.com/badge/Raspberry%20Pi-CC0000.svg?logo=raspberrypi&logoColor=white">
  <img src="https://custom-icon-badges.demolab.com/badge/Router-0078D7.svg?logo=router&logoColor=white">
  <img src="https://custom-icon-badges.demolab.com/badge/DHCP-008000.svg?logo=network&logoColor=white">
</p>



<p align="center">
  <img src="https://i.imgur.com/RVGaecC.png" width="100%" alt="Banner Proyecto Integrador 2025">
</p>

### Introducción
Esta guía instalaremos un servidor DHCP en la Raspberry Pi. Deberemos configurar en nuestra Raspberry Pi el esquema de direcciones IP que deseamos y controlar la asignación de IPs en la LAN creada con nuestro switch y PCs, sin depender del router del colegio.


### Objetivo

El objetivo de este documento es proporcionar una guía paso a paso para configurar un servidor DHCP en una Raspberry Pi, asegurando que las PCs conectadas a nuestra LAN obtengan direcciones IP de manera automática y sin conflictos con el DHCP del colegio.
<p align="center">
  <img src="https://i.imgur.com/kGcCLYA.png" width="100%" alt="Banner Proyecto Integrador 2025">
</p>
<p align="center">
  <img src="https://i.imgur.com/RVGaecC.png" width="100%" alt="Banner Proyecto Integrador 2025">
</p>

## 📘 Índice

1. [Introducción](#introducción)  
2. [Objetivo](#objetivo)  
3. [Glosario](#glosario)  
4. [Pasos](#pasos)  
   - [Paso 1: Instalación del servidor DHCP en Raspberry](#paso-1-instalación-del-servidor-dhcp-en-raspberry)  
   - [Paso 2: Configuración del servidor DHCP](#paso-2-configuración-del-servidor-dhcp)  
   - [Paso 3: Corrección de errores](#paso-3-corrección-de-errores)  
   - [Paso 4: Configurar la IP de nuestra Raspberry](#paso-4-configurar-la-ip-de-nuestra-raspberry)  
   - [Paso 5: Reinicia el dispositivo](#paso-5-reinicia-el-dispositivo)  
5. [Conclusión](#conclusión)

### Glosario

- *isc-dhcp-server*: Software que implementa un servidor DHCP en sistemas Unix y Linux.
- *dhcpd*: Abreviatura común para referirse al servidor DHCP.
- *reboot*: Reinicio del sistema.
- *dhclient*: Cliente DHCP utilizado para obtener direcciones IP de un servidor DHCP.
- *sudo*: Comando que otorga permisos de superusuario para ejecutar comandos.
- *apt*: Sistema de gestión de paquetes utilizado en distribuciones de Linux.
- *update*: Actualiza la lista de paquetes disponibles.
- *install*: Instala software o programas.
- *SSH*: Protocolo para acceder y gestionar sistemas remotos de manera segura.
- *nano*: Editor de texto de línea de comandos simple y fácil de usar.

## Pasos
<p align="center">
  <img src="https://img.icons8.com/fluency/512/console.png" alt="Terminal" width="180">
</p>




### Paso 1: Instalación del servidor DHCP en RaspBerry

Conéctate a tu Raspberry Pi a través de SSH y ejecuta:

~~~bash
sudo apt-get install isc-dhcp-server
~~~

Esto instalará el servicio DHCP necesario para asignar IPs a los dispositivos conectados a nuestra LAN.
<p align="center"> <img src="https://img.icons8.com/color/512/raspberry-pi.png" width="120" alt="Instalación DHCP Raspberry Pi"> </p>
<p align="center">
  <img src="https://i.imgur.com/zDTIHyR.png" width="100%" alt="Banner Proyecto Integrador 2025">
</p>

### Paso 2: Configuración del servidor DHCP

Editamos el archivo de configuración para establecer el rango de IPs y opciones de subred:
<p align="center"> <img src="https://img.icons8.com/fluency/512/ip-address.png" width="120" alt="Configuración IP estática"> </p>

~~~bash
sudo nano /etc/dhcp/dhcpd.conf
~~~

Agregamos lo siguiente (ajustando las IPs según nuestro grupo):

~~~conf
# Opciones globales
ddns-update-style none;
option domain-name "home.local";
option domain-name-servers 8.8.8.8, 8.8.4.4;

default-lease-time 259200;
max-lease-time 604800;

authoritative;
log-facility local7;

# Opciones de subred
subnet 192.168.6.0 netmask 255.255.255.0 {
    range 192.168.6.3 192.168.6.10;
    option routers 192.168.6.1;
    option subnet-mask 255.255.255.0;
    option broadcast-address 192.168.6.255;
}

# Reserva de direcciones
host timbleck-pc1 {
    hardware ethernet 00:11:22:33:44:55;
    fixed-address 192.168.6.110;
}

host timbleck-pc2 {
    hardware ethernet 00:00:00:11:11:11;
    fixed-address 192.168.6.111;
}
~~~

<p align="center">
  <img src="https://i.imgur.com/zDTIHyR.png" width="100%" alt="Banner Proyecto Integrador 2025">
</p>

### Paso 3: Corrección de errores

Verificamos la configuración con:

~~~bash
sudo dhcpd -t
~~~

Si no hay errores, el servidor está listo para iniciar.
<p align="center"> <img src="https://img.icons8.com/color/512/settings--v1.png" width="120" alt="Configuración DHCP"> </p>

<p align="center">
  <img src="https://i.imgur.com/zDTIHyR.png" width="100%" alt="Banner Proyecto Integrador 2025">
</p>

### Paso 4: Configurar la IP de nuestra Raspberry

Como no podemos deshabilitar el DHCP del router del colegio, crearemos una *LAN aislada* con el switch, la Raspberry y las PCs:

1. Asignamos IP a la Raspberry desde la terminal:

~~~bash
sudo ip addr add 192.168.6.2/24 dev eth0
sudo ip link set eth0 up
~~~

- Esto pone la IP directamente sin editar archivos de configuración permanentes.
- La interfaz eth0 ahora tiene la IP 192.168.6.2 y está activa.

2. Conexiones físicas:
- Conectar la *Raspberry al switch*.
- Conectar las *PCs al mismo switch*.
- NO conectar el switch al router del colegio para evitar conflictos de DHCP.

<p align="center"> <img src="https://img.icons8.com/color/512/computer--v1.png" width="120" alt="Cliente DHCP"> </p>
<p align="center">
  <img src="https://i.imgur.com/zDTIHyR.png" width="100%" alt="Banner Proyecto Integrador 2025">
</p>

### Paso 5: Reinicia el dispositivo

Reiniciamos la Raspberry para aplicar cambios:

~~~bash
reboot
~~~

Luego, en cada PC de la LAN, liberamos y renovamos la IP:

~~~bash
sudo dhclient -r
sudo dhclient
~~~

Las PCs deberían recibir IPs del rango 192.168.6.3–192.168.6.10 asignadas por nuestra Raspberry.
<p align="center"> <img src="https://img.icons8.com/fluency/512/restart.png" width="120" alt="Reiniciar DHCP"> </p>
<p align="center">
  <img src="https://i.imgur.com/zDTIHyR.png" width="100%" alt="Banner Proyecto Integrador 2025">
</p>

# Conclusión

La experiencia de configurar un servidor DHCP en la Raspberry Pi fue muy instructiva. Aprendimos a instalar, configurar y verificar un servicio de red fundamental, y también a *adaptarnos a un entorno donde no se puede modificar el router principal*.  

Crear una LAN aislada con el switch y las PCs nos permitió poner en práctica conceptos de direccionamiento IP, subredes y asignación dinámica, además de experimentar la importancia de la planificación de la red para evitar conflictos de DHCP.  

A pesar de las dificultades iniciales con la configuración y los errores de sintaxis, lograr que las PCs reciban IP automáticamente por la Raspberry fue muy satisfactorio y reforzó nuestra comprensión práctica de redes locales.
