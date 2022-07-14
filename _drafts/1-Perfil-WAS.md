---
layout: post
title:  "Crear un perfil en WAS 9"
date:   2022-07-06
categories: Instalacion WAS
---

# Introduccion

WebSphere Application Server en adelante [WAS](https://www.ibm.com/es-es/cloud/websphere-application-server), es una servidor de IBM para enfocado en el sector empresarial donde se facilita el manejo de grandes clustes o aplicaciones pesadas.

Para desarrollar una servicio o una aplicacion web enfocado a un servidor WAS en tu ordenador local se usa el [RSA](https://www.ibm.com/products/rational-software-architect-designer) que es una evolovucion de Eclipse para adaptarse a los productos de IBM. Y antes de poder crear un proyecto web debemos crear un perfil de WAS.

Un perfil de WAS es donde se guardan todos los recursos, las JNDI, los orígenes de datos ... es decir es todo lo necesario para que la aplicacion funcione. 

El hecho de tener instalado un servidor WAS en un ordenador no te permite desplegar aplicaciones directamente hasta que se haya creado un perfil donde se pueda guarda toda la configuración. 

LIBERTY TRADICIONAL

Para desarrollar de forma local se pueden crear diferentes perfiles, pero en esta practica de como [crear un perfil en WAS 9](https://www.ibm.com/docs/es/was-nd/9.0.5?topic=interface-creating-application-server-profiles), no se permite compartir este perfil entre diferentes equipos.


# 1. Abrir la ventana de Gestión de perfil

Abrimos el RSA, y vemos que en la vista de servidores dice que no hay servidores disponibles, eso es porque no hemos creado ningún perfil. 
Si no se muestra la vista Servidores en el panel inferior, podemos abrirlo en 
*Barra Menu > Mostrar Vista > Servidores*

Para abrir la ventana de gestion de perfiles de WAS, 
primero abrimos las preferencias *Menu > Ventana > Preferencias*

![Imagen](/img/Perfil-WAS/01-01-abrir-gestion-de-perfil.png)

En la ventana de preferencias, vamos a la opcion de *Servidor > WebShere Application.*

En la ventana tenemos dos tablas, en la primera llamada *Gestión de perfiles locales de WebSphere Server* se muestra donde esta la instalacion de servidor, podemos tener varias instalaciones con diferentes versiones como WAS8, WAS8.5 o WAS9. En mi caso tengo la version 9. 

En la segunda tabla tenemos *Pperfiles de WebSphere Aplication Server* vemos los perfiles que hemos creado de cada servidor que no tenemos ninguno.

Hacemos click en *Ejecutar herramienta de gestión de perfiles* para crear un perfil para el servidor de WAS9 que tenemos seleccionado.


![Imagen](/img/Perfil-WAS/01-02-abrir-gestion-de-perfil.png)

Puede ser que en el menu lateral, no aparezca la opcion de *Servidores*. Eso se debe a que tenemos una perpectiva que no tiene habilitado los servidores. Para poner la perpectiva de Java EE y ver la opcion de servidores, hacer click en el boton que esta arriba a la derecha para abrir perpectiva y seleccionar Java EE

![Imagen](/img/Perfil-WAS/01-03-abrir-gestion-de-perfil.png)

Se nos muestras los perfiles existentes, no tenemos ninguno y le damos al boton de *Crear...*

![Imagen](/img/Perfil-WAS/01-04-abrir-gestion-de-perfil.png)


Tenemos dos maneras de


![Imagen](/img/Perfil-WAS/02-01-crear-perfil.png)


![Imagen](/img/Perfil-WAS/02-02-crear-perfil.png)


![Imagen](/img/Perfil-WAS/02-03-crear-perfil.png)


![Imagen](/img/Perfil-WAS/02-04-crear-perfil.png)


![Imagen](/img/Perfil-WAS/02-05-crear-perfil.png)


![Imagen](/img/Perfil-WAS/02-06-crear-perfil.png)


![Imagen](/img/Perfil-WAS/02-07-crear-perfil.png)


![Imagen](/img/Perfil-WAS/02-08-crear-perfil.png)


![Imagen](/img/Perfil-WAS/02-09-crear-perfil.png)


![Imagen](/img/Perfil-WAS/02-10-crear-perfil.png)


![Imagen](/img/Perfil-WAS/02-11-crear-perfil.png)


![Imagen](/img/Perfil-WAS/02-12-crear-perfil.png)


![Imagen](/img/Perfil-WAS/03-01-iniciar-servidor.png)


![Imagen](/img/Perfil-WAS/03-02-iniciar-servidor.png)


![Imagen](/img/Perfil-WAS/03-03-iniciar-servidor.png)


![Imagen](/img/Perfil-WAS/03-04-iniciar-servidor.png)


![Imagen](/img/Perfil-WAS/03-05-iniciar-servidor.png)


![Imagen](/img/Perfil-WAS/03-06-iniciar-servidor.png)