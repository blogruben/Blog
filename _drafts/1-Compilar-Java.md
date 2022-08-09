---
layout: post
title:  "Compilar con java usando classpath"
date:   2022-07-06
categories: Saludos
---
## Intro
Vamos a ver las herramientas para compilar y empaquetar archivos de java que provee el JDK, y como funciona el classpath.
Vamos aprender a compilar nuestras aplicaciones en Java desde la consola de manera básica sin necesidad de usar ningún IDE ni ningún gestor de librerías, cuando nuestro desarrollo va ganado en complejidad este metodo se vuelve impractible, sin embarjo es un buen ejercicio para conocer el funcionamiento de las herramientas de dessarrollo de Java a bajo nivel.

Básicamente el Java Runtime Environment (en adelante JRE) es la maquina virtual de java (JVM) más ciertas librerías necesarias para ejecutar las aplicaciones de Java,    
y por otro lado el Java Development Kit (JDK) esta pensado para el desarrollo de aplicaciones, por lo que trae el JRE para ejecutar las aplicaciones más una serie de herramientas necesarias para el desarrollo como pueden ser los compiladores, debuggear empaquetadores etc.


## Requisitos
Aunque actualmente ya estamos por la versión 18 de Java, vamos a usar el JDK 8 que a nivel empresarial aún se sigue usando ya que Oracle mantiene una licencia menos restrictiva. 
Para ello, podemos descargarlo el [JDK de Oracle](https://www.oracle.com/java/technologies/downloads/) o el [OpenJDK](https://openjdk.org/projects/jdk8/) y añadir el path en Windows, para ello puedes encontrar muchos tutoriales en internet como por ejemplo [este](https://www.aprenderaprogramar.com/index.php?option=com_content&view=article&id=389:configurar-java-en-windows-variables-de-entorno-javahome-y-path-cu00610b&catid=68&Itemid=188)

![inicar-consola](/img/Compilar-Java/01-01-inicar-consola.png)

Comprobamos que tenemos instalado el JDK en Windows. Para ello, buscando "cmd" o "Símbolo del sistema" en el buscador de Windows para abrir la consola y ejecutamos ``java -version`` para saber que el path del sistema apunta a la instalación de Java.

![inicar-consola](/img/Compilar-Java/01-02-inicar-consola.png)

También es conveniente comprobar el comando `jar` (Java Archive Tool) que sirve para empaquetar varios archivos java.
```
C:\Users\Ruben>jar
Sintaxis: jar {ctxui}[vfmn0PMe] [jar-file] [manifest-file] [entry-point] [-C dir] files ...
Opciones:
    -c  crear nuevo archivo
...
```
Se muestra la ayuda del comando, en caso de que no se encuentre la aplicación `jar` mostrará el siguiente error.
```
C:\Users\Ruben>jar
"jar" no se reconoce como un comando interno o externo,
programa o archivo por lotes ejecutable.
```
Si no se reconoce `jar` pero si `java -version` puede ser que tu variable de entorno apunte a el JRE en vez de al JDK. Puedes ver en el [diagrama de JDK 8](https://docs.oracle.com/javase/8/docs/) que el módulo "jar" pertenece a JDK pero no a JRE porque es una herramienta de desarrollo.

# 1 Compilar y descompilar una clase java

## 1.1 Compilar HolaMundo

Vamos a crear un archivo java que contenga una clase que imprima "Hola mundo", luego la vamos a compilar y ejecutar desde el set de herramientas de JDK. 

Primero creamos un archivo llamado HolaMundo.java que contenga lo siguiente:
```
public class HolaMundo {
    public static void main(String[] args) {
        System.out.println("Hola Mundo");
    }  
}
```
Para ello podemos hacerlo gráficamente:
1. Podemos hacer click-derecho sobre el escritorio
2. ir a *Nuevo* -> *Documento de texto*
3. renombralo por *HolaMundo.java*
4. abrirlo con el blog de notas para editar el archivo java

![crear-archivo](/img/Compilar-Java/02-01-crear-archivo.png)

Si prefieres la consola `cmd` seria:
1. `more >> HolaMundo.java` para guardar lo que escribamos en el archivo
2. Pegamos el contenido
3. Hacemos Ctrl+C para cerrar y guardar

imagen

Y si estamos usando la PowerShell 
1. 
2. 
3. 
powershell -Command "Write-Host This is`na multiline`ntext"


`n is the newline because ` is the escape character in powershell

Compilamos el archivo java
```
javac  HolaMundo.java
```

Ahora ejecutamos la clase
```
# esto da error porque no se pone la extension class
java HolaMundo.class
#Error: no se ha encontrado o cargado la clase principal 

# Se ejecuta asi
#java HolaMundo
> Hola Mundo
```

Lo empaquetamos
```
jar cvf hola.jar HolaMundo.class
> manifiesto agregado
> agregando: HolaMundo.class(entrada = 422) (salida = 286)(desinfl
```

#ejecutar paquete  (sin classpath en el manifest)
```
java -cp hola.jar HolaMundo
> Hola Mundo
```

## 1.2 Descompilar clase del paquete hola.jar

#ver el contenido del paquete
jar -tf hola.jar
> META-INF/
> META-INF/MANIFEST.MF
> HolaMundo.class

#ver el manifest con un solo comando
#-p es para imprimir por pantalla en vez de generar archivo
unzip -p hola.jar META-INF/MANIFEST.MF

#extraer todo en un directorio
unzip hola.jar -d Hola
#modificar lo que sea
#y volvemos a compilar
jar cvf hola.jar -C Hola/ .

#extraer todo
jar -xf hola.jar HolaMundo.class
#extraer un archivo en concreto
jar -xf hola.jar HolaMundo.class

descargar Java Decompiler Proyect
y ver el contenido de HolaMundo.class
http://java-decompiler.github.io/

## 1.3 Definir clase principal

#creamos el paquete diciendo que holaMundo es la clase principal
jar cvfe hola.jar HolaMundo HolaMundo.class

#ya podemos ejecutar sin espeificar el classpath
java -jar hola.jar


# 2 Modificar manifest y classpath
## 2.1 Crear libreria 
Creamos un paquete para el main class, ya que es necesario que tengo un paquete
para definirlo en el manifest

Creamos org/blogruben/prueba/tools/Impresion.java para imprimir
```
package org.blogruben.prueba.tools;

public class Impresion {
    public static void imprimir(String msg){
        System.out.println(msg);
    }
}
```

#compilamos
javac -d lib  com/blogruben/prueba/tools/Impresion.java

#empaquetamos
jar cvf impresion.jar Impresion.class

## 2.1 Compilar clases con sus paquetes

Tenemos la libreria de antes lib/impresion.jar

Creamos org/blogruben/prueba/HolaMundo.java
```
package org.blogruben.prueba;

import org.blogruben.prueba.tools.impresion;

public class HolaMundo {
   public static void main(String[] args) {
    impresion.imprimir("Hola mundo !!!!");
   }
}
```

Creamos org/blogruben/prueba/AdiosMundo.java
```
package org.blogruben.prueba;

import org.blogruben.prueba.tools.impresion;

public class AdiosMundo {
   public static void main(String[] args) {
       impresion.imprimir("Adios mundo cruel!");
   }
}
```

#compilamos
javac -d compilado -cp lib/impresion.jar com/blogruben/prueba/HolaMundo.java com/blogruben/prueba/AdiosMundo.java com/blogruben/prueba/tools/Impresion.java

#empaquetamos 
jar cvfe saludos.jar org.blogruben.prueba.HolaMundo org/blogruben/prueba/HolaMundo.java org/blogruben/prueba/AdiosMundo.java

> java.lang.ClassNotFoundException 
Nos dice que no encuentra la clase Impresion porque no esta en el clasepath

## 2.2 Manifest con classpath
Creamos el manifest.txt
touch manifest.txt (en linux o mac)
type nul >> "file.txt" (en windows)
(si el mainClass no tiene paquete no funciona)
```
Manifest-Version: 1.0
Created-By: Blogruben
Main-Class: org.blogruben.prueba.HolaMundo
Class-Path: ./lib/impresion.jar
```


#creamos el paquete hola con el manifest de antes
jar cfm saludos.jar manifest.txt com/blogruben/prueba/HolaMundo.class

#ejecutamos sin espeificar el classpath
java -jar saludos.jar
>Hola mundo !!!!

----
Actualizar manifest
jar uvfm chat.jar manifest.txt



[Documentacion oficial](https://docs.oracle.com/javase/tutorial/deployment/jar/build.html)





