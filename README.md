<p align="center">
  <img src="https://i.imgur.com/lChzWM2.png" width="100%" alt="Banner Proyecto Integrador 2025">
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
  <img src="https://custom-icon-badges.demolab.com/badge/-FTP-blue?logo=file&logoColor=white">



<p align="center">
  <img src="https://i.imgur.com/RVGaecC.png" width="100%" alt="Banner Proyecto Integrador 2025">
</p>

<div align="center">

## 📘 Índice

[1 - Introducción](#introducción)  
[2 - Objetivo](#objetivo)  
[3 - Glosario](#glosario)  
[4 - Pasos](#pasos)  
[5 - Conclusión](#conclusión)

</div>


<p align="center">
  <img src="https://i.imgur.com/RVGaecC.png" width="100%" alt="Banner Proyecto Integrador 2025">
</p>

### introducción

En este proyecto estamos configurando una **Raspberry Pi** para que funcione como un **router o simulador de router**, gestionando distintos servicios de red.  
Hasta el momento hemos trabajado y configurado servicios como **SSH**, **Xorg** y **DHCP**, los cuales nos permitieron acceder de forma remota, redirigir interfaces gráficas y asignar direcciones IP dinámicas dentro de la red.  
A partir de esta base, continuaremos incorporando nuevos servicios y configuraciones que amplíen las funciones del dispositivo como punto central de la red.


### Objetivo

En este trabajo implementaremos un **servidor FTP (File Transfer Protocol)** en nuestra **Raspberry Pi configurada como router**, con el fin de permitir la **transferencia de archivos dentro de la red LAN**.  

Primero abordaremos la **parte teórica**, comprendiendo qué es el protocolo FTP y cómo permite el intercambio de datos entre equipos dentro de una red. Luego, en la **parte práctica**, instalaremos y configuraremos el servicio **vsftpd** para que la Raspberry Pi actúe como **servidor FTP de la red local** de cada grupo.  

Para comprobar el correcto funcionamiento del servicio, utilizaremos clientes como **FileZilla** o **WinSCP** desde otras máquinas conectadas.  

**Referencias recomendadas:**  
- [Tutorial: Servidor FTP en Raspberry Pi – Geeky Theory](https://geekytheory.com/tutorial-raspberry-pi-9-servidor-ftp/)  
- [Documentación oficial de FileZilla](https://wiki.filezilla-project.org/FileZilla_Client_Tutorial_(es))  
- [Documentación oficial de WinSCP](https://winscp.net/eng/docs/ftps)

<p align="center">
  <img src="https://i.imgur.com/PxXjqZX.png" width="100%" alt="Banner Proyecto Integrador 2025">
</p>
<p align="center">
  <img src="https://i.imgur.com/RVGaecC.png" width="100%" alt="Banner Proyecto Integrador 2025">
</p>




## Glosario


<img src="https://custom-icon-badges.demolab.com/badge/-sudo-gray?logo=terminal&logoColor=white"> Permite ejecutar comandos con privilegios de **superusuario (root)**, otorgando permisos administrativos temporales.  

<img src="https://custom-icon-badges.demolab.com/badge/-apt-blue?logo=debian&logoColor=white">  Sistema de **gestión de paquetes** en distribuciones Linux. Se usa para instalar, actualizar o eliminar software.  

<img src="https://custom-icon-badges.demolab.com/badge/-update-orange?logo=refresh&logoColor=white">  Actualiza la **lista de paquetes disponibles** en los repositorios. No instala, solo sincroniza la información.  

<img src="https://custom-icon-badges.demolab.com/badge/-install-green?logo=add&logoColor=white"> Instala **paquetes o programas** en el sistema usando herramientas como `apt-get`.  

<img src="https://custom-icon-badges.demolab.com/badge/-nano-yellow?logo=file-edit&logoColor=white"> Editor de texto **simple y en línea de comandos**, útil para modificar archivos de configuración directamente desde la terminal.  

<img src="https://custom-icon-badges.demolab.com/badge/-useradd-blueviolet?logo=user-add&logoColor=white"> Crea **nuevos usuarios** en el sistema.  

<img src="https://custom-icon-badges.demolab.com/badge/-mkdir-teal?logo=folder-plus&logoColor=white"> Crea **directorios o carpetas** dentro del sistema de archivos.  

<img src="https://custom-icon-badges.demolab.com/badge/-chown-brown?logo=shield-key&logoColor=white">* Cambia la **propiedad** de un archivo o directorio, asignando nuevo usuario o grupo.  

<img src="https://custom-icon-badges.demolab.com/badge/-geekyuser:users-lightgrey?logo=users&logoColor=white"> Ejemplo de propiedad: “geekyuser” es el **usuario propietario** y “users” el **grupo asociado**.  

<img src="https://custom-icon-badges.demolab.com/badge/-passwd-red?logo=key&logoColor=white"> Permite **cambiar la contraseña** de un usuario.







## Pasos
### Instalación y Configuración de vsftpd:

<p align="center">
  <img src="https://i.imgur.com/HfoRxC1.png" width="100%" alt="Banner Proyecto Integrador 2025">
</p>
Primero vamos a descargar el servidor vsftpd. 

~~~
sudo apt-get update
sudo apt-get install vsftpd
~~~


Una vez que este descargado abrimos el siguiente archivo de configuración. 

~~~
sudo nano /etc/vsftpd.conf
~~~


Descomentamos las siguientes líneas para permitir la escritura de archivos a los usuarios de la Raspberry Pi.

~~~
local_enable=YES
write_enable=YES
~~~

Por último reiniciamos el servicio. sudo service vsftpd restart


Una vez que hemos instalado nuestro servidor FTP, vamos a ver si funciona, para ello, descargamos [Filezilla](https://filezilla-project.org/) que es un cliente FTP. Nos aparecerá una ventana y en la parte de arriba tendremos espacios para rellenar que dicen: Servidor, Nombre de usuario, Contraseña y puerto; este ultimo no lo usaremos.


Rellenamos los campos de servidor, nombre de usuario y contraseña:


<p align="center">
  <img src="https://i.imgur.com/9foz99Q.png" width="100%" alt="Banner Proyecto Integrador 2025">
</p>

Una vez que tenemos todos los datos introducidos tocamos en conectar


<p align="center">
  <img src="https://i.imgur.com/uwFbino.png" width="100%" alt="Banner Proyecto Integrador 2025">
</p>


<p align="center">
  <img src="https://i.imgur.com/zDTIHyR.png" width="100%" alt="Banner Proyecto Integrador 2025">
</p>

## Conclusión

La correcta configuración de un servidor FTP en la Raspberry Pi ofrece una valiosa herramienta para compartir archivos y fomentar la colaboración en un entorno de trabajo. Esto permite a los usuarios cargar y descargar archivos de manera eficiente, lo que a su vez mejora la productividad y la comunicación en el ámbito laboral. La implementación de un servidor FTP en la Raspberry Pi se presenta como una solución versátil para satisfacer las necesidades de transferencia de archivos en redes locales.

<p align="center">
  <img src="https://i.imgur.com/iPxDSQA.png" width="100%" alt="Banner Proyecto Integrador 2025">
</p>



