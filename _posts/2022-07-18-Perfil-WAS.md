---
layout: post
title:  "Crear un perfil en WAS 9"
date:   2022-07-18
categories: Instalacion WAS
repasado: casi
---

## Introducción

WebSphere Application Server en adelante [WAS](https://www.ibm.com/es-es/cloud/websphere-application-server), es una servidor de IBM enfocado en el sector empresarial donde se facilita el manejo de grandes clusters o aplicaciones pesadas.

Para desarrollar un servicio o una aplicación web enfocada a un servidor WAS en tu ordenador local, se usa el IDE llamado [RSA](https://www.ibm.com/products/rational-software-architect-designer) (Rational Software Architect Designer) que es una evolución de Eclipse para adaptarse a los productos de IBM. 

Es importante recalcar que antes de poder crear un proyecto web, debemos crear un perfil en WAS.

> Un perfil de WAS es donde se guardan todos los recursos, las JNDI, los orígenes de datos ... es decir, todo lo necesario para que la aplicacion funcione. 

El hecho de tener instalado WAS en tu ordenador, no significa que puedas desplegar aplicaciones directamente sobre él, es necesario un perfil donde se guarda toda la configuración necesaria.

Principalmente tenemos dos versiones de WAS: *"WebSphere Liberty"* que esta enfocado a aplicaciones cloud y *"Traditional WebSphere"* que se enfoca en desplegar las aplicaciones en su propio servidor IBM. En la práctica que vamos a ver de cómo [crear un perfil en WAS 9](https://www.ibm.com/docs/es/was-nd/9.0.5?topic=interface-creating-application-server-profiles) instalaremos el servidor de traditional WAS.

En un desarrollo normal en el PC local se pueden crear varios perfiles e incluso en diferentes versiones de servidor WAS, cada uno con su propia configuración para trabajar con varias aplicaciones.


## 1. Abrir la ventana de Gestión de perfil

![Dar de alta servidor WAS 1](/img/Perfil-WAS/00-01-dar-alta-servidor-WAS9.png)

Cuando abrimos el RSA, a parte de preguntarmos sobre el directorio del workspace, tenemos que configurar el servidor.  Primero nos pregunta si queremos añadir el WAS 9 en el RSA, es con el que vamos a trabajar. Marcamos el check.

![Dar de alta servidor WAS 2](/img/Perfil-WAS/00-02-dar-alta-servidor-WAS9.png)

Luego pregunta por la WAS 8, este no lo necesitamos, ya que vamos a crear un perfil en WAS 9.

![Imagen](/img/Perfil-WAS/01-01-abrir-gestion-de-perfil.png)

En la vista de servidores dice que no hay servidores disponibles, eso es porque no hemos creado ningún perfil. 
Si no se muestra la vista Servidores en el panel inferior, podemos abrirlo en 
*Menu > Mostrar Vista > Servidores*

Para abrir la ventana de gestión de perfiles de WAS, 
primero abrimos las preferencias *Menu > Ventana > Preferencias*

![Imagen](/img/Perfil-WAS/01-02-abrir-gestion-de-perfil.png)

En la ventana de preferencias, vamos a la opción de *Servidor > WebSphere Application.*

En la ventana tenemos dos tablas, en la primera table *(Gestión de perfiles locales de WebSphere Server)* se muestra donde esta la instalación de servidor, podemos tener varias instalaciones con diferentes versiones como WAS8, WAS8.5 o WAS9. En mi caso solo tengo la versión 9. 

En la segunda tabla *(Perfiles de WebSphere Aplication Server)* vemos los perfiles que tenemos creados de cada servidor, en nuestro caso no tenemos ninguno.

Para crear un perfil en el servidor de WAS9 que tenemos seleccionado, hacemos click en boton *(Ejecutar herramienta de gestión de perfiles)* 

![Imagen](/img/Perfil-WAS/01-03-abrir-gestion-de-perfil.png)

Puede ser que en la ventana de preferencias, no aparezca la opción de *Servidores* en menu lateral. Eso se debe a que tenemos una perpectiva que no tiene habilitado los servidores. Para poner la perpectiva de Java EE y poder ver la sección de servidores, hacemos click en el botón *(Abrir perpectiva)* situado arriba a la derecha para abrir la perpectiva de Java EE

![Imagen](/img/Perfil-WAS/01-04-abrir-gestion-de-perfil.png)

Se nos muestras los perfiles existentes, no tenemos ninguno y le damos al boton de *Crear...*

## 2. Crear perfil de WAS 9

![Imagen](/img/Perfil-WAS/02-01-crear-perfil.png)

Tenemos dos maneras de gestionar la configuración del servidor. Si seleccionamos *(Gestión)* podemos manejar la configuración de varios servidores desde un mismo *Agente Administrativo*. Si seleccionamos la opción de *(Servidor de aplicaciones)* el servidor que creemos se le asocia una consola administrativa. La consola administrativa que es un panel donde se configuran los recursos del perfil WAS.

Teniendo en cuenta que estamos en un entorno de desarrollo, solo necesitamos administrar los recursos de un perfil por lo que selecionamos *Servidor de aplicaciones*.

![Imagen](/img/Perfil-WAS/02-02-crear-perfil.png)

Ahora seleccionamos entre la *Creación de perfiles típico* en la que se ponen valores por defecto o en la *Creación de perfiles avanzada* en la que se permite configurar más parametros. Seleccionamos la opcion de *Creación de perfiles avanzada* 

![Imagen](/img/Perfil-WAS/02-03-crear-perfil.png)

En la ventana de *Despliegue de aplicaciones opcionales* seleccionamos la consola administrativa muy importante para gestionar los recursos de WAS y la herramienta de verificación de la instalación. La opción de *Desplegar la aplicacion por omisión* no es necesario, esto instalará una aplicacion a modo de ejemplo como Hello Snoop HitCount

![Imagen](/img/Perfil-WAS/02-04-crear-perfil.png)

Por defecto el perfil se llama *AppSrv01*. Es recomentable que el directorio se llame igual que el perfil para simplificar. Es decir, si queremos llamar al perfil *hola mundo* sería:
- Nombre de perfil: HolaMundo
- Directorio del perfil: C:\IBM\WebSphere\AppServer90\profiles\HolaMundo

En el *Valor de ajuste de rendimiento de ejecucíon de servidor* ponemos *"Desarrollo"* para que el servidor consuma menos recursos y sea más ligero para el equipo local.

![Imagen](/img/Perfil-WAS/02-05-crear-perfil.png)

- Nombre de nodo: xxxxNode01
- Nombre de servidor: server1
- Nombre de host: xxxx.company.es

![Imagen](/img/Perfil-WAS/02-06-crear-perfil.png)

La seguridad administrativa es para a poner una contraseña al panel de control del WAS, en local no es necesario, ya que no esta publicado.

![Imagen](/img/Perfil-WAS/02-07-crear-perfil.png)

Usamos un certificado por defecto.

![Imagen](/img/Perfil-WAS/02-08-crear-perfil.png)

Dejamos los valores por defecto del cerficado de seguridad.

![Imagen](/img/Perfil-WAS/02-09-crear-perfil.png)

El puerto al que tenemos que prestar más atención es el tranporte HTTP, si nuestra aplicación tiene un servicio o un servlet, este será despachado por *http://localhost:9080/*

![Imagen](/img/Perfil-WAS/02-10-crear-perfil.png)

La [definición de servidor web](https://www.ibm.com/docs/es/was/9.0.5?topic=console-web-server-definition) ayuda a la gestión del servidor en producción, por lo tanto no la ponemos.

![Imagen](/img/Perfil-WAS/02-11-crear-perfil.png)


![Imagen](/img/Perfil-WAS/02-12-crear-perfil.png)

Se genera el perfil.

![Imagen](/img/Perfil-WAS/03-01-iniciar-servidor-en-rsa.png)

Ya podemos ver el perfil que acabamos de crear.


### Añadimos el perfil a la vista de los servidores del RSA

![Imagen](/img/Perfil-WAS/03-02-iniciar-servidor-en-rsa.png)

En el RSA, en la vista de los servidores no se muestra el perfil que hemos creado. Se debe añadir el servidor al RSA para que lo muestre. Click derecho sobre el fondo blanco de la vista de servidores y vamos a *Nuevo > Servidor*

![Imagen](/img/Perfil-WAS/03-03-iniciar-servidor-en-rsa.png)

Seleccionamos el tipo de servidor IBM y la versión *"WebSphere Application traditional V9.0"* 

![Imagen](/img/Perfil-WAS/03-04-iniciar-servidor-en-rsa.png)

Aquí seleccionamos el nombre del perfil que hemos creado *AppSrv01* y finalizamos.

![Imagen](/img/Perfil-WAS/03-05-iniciar-servidor-en-rsa.png)

Ya se muestra el servidor, hacemos doble click sobre el servidor, y en el panel de control, cambiamos el nombre de servidor  en la seccion de información general y guardamos.

![Imagen](/img/Perfil-WAS/03-06-iniciar-servidor-en-rsa.png)

En la sección del servidor, podemos seleccionar la opción *"Terminar servidor al concluir el entorno de trabajo"*. Esto es interesante porque a veces cerramos el RSA sin darnos cuenta que tenemos el servidor arrancado y se queda funcionando en segundo plano.


## 3. Abrir la Consola Administrativa

![Imagen](/img/Perfil-WAS/04-01-iniciar-servidor.png)

En la vista de los servidores, vemos que tenemos detenido el servidor.

![Imagen](/img/Perfil-WAS/04-02-iniciar-servidor.png)

Para acceder a la *"Consola Administrativa"* tenemos que arrancar el servidor,
para eso, hacemos click derecho en el servidor, y le demos a *"Iniciar"*.

![Imagen](/img/Perfil-WAS/04-03-iniciar-servidor.png)

La *"Consola Administrativa"* es un panel para configurar los recursos de servidor, las JNDI, los orígenes de datos etc. Para abrirla, le damos *click derecho sobre el servidor > Administracion > Ejecutar consola* Administrativa

![Imagen](/img/Perfil-WAS/05-01-abrir-consola-administrativa.png)

Se abre la "Consola Administrativa" en el RSA

![Imagen](/img/Perfil-WAS/05-02-abrir-consola-administrativa.png)

También podemos ver, la *"Consola Administrativa"* [desde el navegador](https://www.ibm.com/docs/en/tfim/6.2.2.7?topic=server-starting-console), si *"el puerto
de tranporte HTTP"* es el 9080, entramos en la url  **http://localhost:9080/ibm/console/**

![Imagen](/img/Perfil-WAS/05-03-abrir-consola-administrativa.png)

![Imagen](/img/Perfil-WAS/05-04-abrir-consola-administrativa.png)

Para ver *"el puerto de HTTP"*, hacemos click derecho sobre el servidor, y le damos a propiedades.


## 4. Ver logs

![Imagen](/img/Perfil-WAS/05-01-ver-logs.png)

En el RSA tenemos la vista de la consola donde se muestran los logs del servidor y de la aplicación levantada.

Si no se muestra, ir a *"Menu > Ventana > Mostrar Vista > Consola "*

![Imagen](/img/Perfil-WAS/05-02-ver-logs.png)

Estos logs, estan en la ruta *"C:\IBM\WebSphere\AppServer90\profiles\(PERFIL)\logs\(SERVIDOR)\"* y se pueden visualizar directamente, sin necesidad del RSA. 

En este caso la ruta es *"C:\IBM\WebSphere\AppServer90\profiles\AppServer90\logs\server1\"*


En esta práctica hemos visto como crear un perfil en WAS 9 con el RSA. También como acceder a la *Consola Administrativa* y visualidad los logs, en un próximo post haremos un Servicio SOAP y como desplegarlo en el perfil de WAS que hemos creado. 
