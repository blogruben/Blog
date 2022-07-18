---
layout: post
title:  "Crear un perfil en WAS 9"
date:   2022-07-18
categories: Instalacion WAS
---

# Introducción

WebSphere Application Server en adelante [WAS](https://www.ibm.com/es-es/cloud/websphere-application-server), es una servidor de IBM enfocado en el sector empresarial donde se facilita el manejo de grandes clustes o aplicaciones pesadas.

Para desarrollar una servicio o una aplicacion web enfocado a un servidor WAS en tu ordenador local se usa el [RSA](https://www.ibm.com/products/rational-software-architect-designer) que es una evolución de Eclipse para adaptarse a los productos de IBM. Y antes de poder crear un proyecto web debemos crear un perfil de WAS.

Un perfil de WAS es donde se guardan todos los recursos, las JNDI, los orígenes de datos ... es decir es todo lo necesario para que la aplicacion funcione. 

El hecho de tener instalado un servidor WAS en tu ordenador, no significa que puedas desplegar aplicaciones directamente hasta que se haya creado un perfil donde se pueda guardar toda la configuración.

Principalmente tenemos dos versiones de WAS: *"WebSphere Liberty"* que esta enfocado aplicaciones cloud y *"Traditional WebSphere"* que se instala en un servidor IBM, en esta practica instalaremos el traditional WAS.

Para desarrollar de forma local se pueden crear varios perfiles e incluso en diferentes versiones de servidor WAS, cada uno con su configuración.

En esta practica para [crear un perfil en WAS 9](https://www.ibm.com/docs/es/was-nd/9.0.5?topic=interface-creating-application-server-profiles), no se permite compartir el perfil entre diferentes equipos, es solo para el equipo local.

# 1. Abrir la ventana de Gestión de perfil

Cuando abrimos el RSA, a parte de preguntarmos sobre el directorio del workspace, tenemos que configurar el servidor.  Primero nos pregunta si queremos añadir el WAS9 en el RSA, es con el que vamos a trabajar.
![Dar de alta servidor WAS 1](/img/Perfil-WAS/00-01-dar-alta-servidor-WAS9.png)

Luego pregunta por la WAS8, este no lo necesitamos.
![Dar de alta servidor WAS 2](/img/Perfil-WAS/00-02-dar-alta-servidor-WAS9.png)

En la vista de servidores dice que no hay servidores disponibles, eso es porque no hemos creado ningún perfil. 
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


# 2. Crear perfil de WAS 9

Tenemos dos maneras de gestionar la configuracion del servidor. Si seleccionamos *Gestión* podemos manejar al configuracion de varios servidor desde un mismo agente administrativo. Con la opcion de *Servidor de aplicaciones* el servidor que creemos se le asocia una consola administrativa que es un panel donde se configuran los recursos. Teniendo en cuenta que estamso en un entorno de serrollo, solo necesitamos administrar los recursos de este perfil was por lo que selecionamos *Servidor de aplicaciones* 

![Imagen](/img/Perfil-WAS/02-01-crear-perfil.png)

Ahora selecionamos entre la *Creación de perfiles típico* en la que se ponen valores por defecto o en la *Creación de perfiles avanzada* en la que se permite configurar más parametros. Seleccionamos la opcion de *Creación de perfiles avanzada* 

![Imagen](/img/Perfil-WAS/02-02-crear-perfil.png)

En la ventana de *Despliegue de aplicaciones opcionales* seleccionamos la consola administra muy importante para gestionar los recursos de WAS y la herramienta de verificacion de la instalacion. La opcion de *Desplegar la aplicacion por omisión* no es necesario, esto instala una aplicaciones a modo de ejemplo como Hello Snoop HitCount

![Imagen](/img/Perfil-WAS/02-03-crear-perfil.png)

Por defecto el perfil se llama *AppSrv01*. Es recomentable que el directorio se llame igual que el perfil. Esa decir si queremos llamar al perfil *hola mundo* sería:
- Nombre de perfil: HolaMundo
- Directorio del perfil: C:\IBM\WebSphere\AppServer90\profiles\HolaMundo

En el *Valor de ajuste de rendimiento de ejecucíon de servidor* podemos Desarrollo para que el servidor consuma menos recursos y sea más ligero para el desarrollo.

![Imagen](/img/Perfil-WAS/02-04-crear-perfil.png)

Nombre de nodo: xxxxNode01
Nombre de servidor: server1
Nombre de host: xxxx.company.es

![Imagen](/img/Perfil-WAS/02-05-crear-perfil.png)

Para trabajar, en local no es necesario activar la seguridad administrativa que se refiere a poner una contraseña al panel de control del WAS.

![Imagen](/img/Perfil-WAS/02-06-crear-perfil.png)

Usamos un certificado por defecto.

![Imagen](/img/Perfil-WAS/02-07-crear-perfil.png)

Dejamos los valores por defecto del cerficado de seguridad.

![Imagen](/img/Perfil-WAS/02-08-crear-perfil.png)

El puerto al se que tenemos que prestar más atención es el tranporte HTTP, si creamos un servicio o un servlet, este sera despachado por *http://localhost:9080/*

![Imagen](/img/Perfil-WAS/02-09-crear-perfil.png)

La [definición de servidor web](https://www.ibm.com/docs/es/was/9.0.5?topic=console-web-server-definition) ayuda a la gestion del servidor en producción, por lo tanto no la ponemos.

![Imagen](/img/Perfil-WAS/02-10-crear-perfil.png)

Se genera el perfil.

![Imagen](/img/Perfil-WAS/02-11-crear-perfil.png)


![Imagen](/img/Perfil-WAS/02-12-crear-perfil.png)

Ya podemos ver el perfil que acabamos de crear.

![Imagen](/img/Perfil-WAS/03-01-iniciar-servidor-en-rsa.png)

# Añadimos el perfil a la vista de servidores del RSA

En el RSA, en la vista de servidores no se muestra el perfil que hemos creado. Se debe añadir al RSA para que lo encuentre. Click derecho sobre el fondo blanod de la vista de servidores y vamos a *Nuevo > Servidor*

![Imagen](/img/Perfil-WAS/03-02-iniciar-servidor-en-rsa.png)

Seleccionamos el tipo de servidor IBM y la version *"WebSphere Application traditional V9.0"* 

![Imagen](/img/Perfil-WAS/03-03-iniciar-servidor-en-rsa.png)

Aquí seleccionamos el nombre del perfil que hemos creado *AppSrv01* y finalizamos.

![Imagen](/img/Perfil-WAS/03-04-iniciar-servidor-en-rsa.png)

Ya se muestra el servidor, hacemos doble click sobre el servidor, y en el panel de control, cambiamos el nombre de servidor  en la seccion de informacion general.

![Imagen](/img/Perfil-WAS/03-05-iniciar-servidor-en-rsa.png)

En la sección del servidor, ponemos seleccionar la opcion *"Terminar servidor al concluir el entorno de trabajo"*, es interesante porque aveces cerramos el RSA sin darnos cuenta que tenemos el servidor arrancado y se queda funcionando en segundo plano.

![Imagen](/img/Perfil-WAS/03-06-iniciar-servidor-en-rsa.png)

# Abrir la Consola Administrativa

En la vista de los servidores, vemos que tenemos detenido el servidor.

![Imagen](/img/Perfil-WAS/04-01-iniciar-servidor.png)

Para acceder a la consola administrativa tenemos que arrancar el servidor,
para eso, hacemos click derecho en el servidor, y le demos a "iniciar".

![Imagen](/img/Perfil-WAS/04-02-iniciar-servidor.png)

Para abrir la consola administrativa que es un panel para configurar los recursos de servidor, le damos a sobre el servidor click derecho > Administracion > Ejecutar consola Administrativa
![Imagen](/img/Perfil-WAS/04-03-iniciar-servidor.png)

Se abre el consola Administrativa en el RSA

![Imagen](/img/Perfil-WAS/05-01-abrir-consola-administrativa.png)

Tambien podemos ver, la consola administrativa desde el navegador, si el puerto
de *"puerto de tranporte HTTP"* es el "9080, entramos en **http://localhost:9060/ibm/console/**

![Imagen](/img/Perfil-WAS/05-02-abrir-consola-administrativa.png)

Para ver el puerto de HTTP, hacemos click derecho sobre el servidor, y le damos a propiedades.

![Imagen](/img/Perfil-WAS/05-03-abrir-consola-administrativa.png)

![Imagen](/img/Perfil-WAS/05-04-abrir-consola-administrativa.png)

# Ver logs

En el RSA, vemos la vista de la consola donde se muestran los logs de servidor y de la aplicacion levantada.

![Imagen](/img/Perfil-WAS/05-01-ver-logs.png)

Estos logs, estan en la ruta *"C:\IBM\WebSphere\AppServer90\profiles\<NOMBRE_PERFIL>\logs\<SERVIDOR>\"* y se pueden visualizar directamente. En este caso la ruta es *"C:\IBM\WebSphere\AppServer90\profiles\AppServer90\logs\server1\"*

![Imagen](/img/Perfil-WAS/05-02-ver-logs.png)
