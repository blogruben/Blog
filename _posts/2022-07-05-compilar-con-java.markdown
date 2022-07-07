---
layout: post
title:  "Compilar con Java"
date:   2022-07-07
categories: Java Compilar Empaquetar Classpath
---
## Intro
Vamos a ver las herramientas para compilar y empaquetar archivos de java que provee JDK, y como funciona el classpath.
Basicamente el JRE es la maquina virtual de java JVM y ciertas librerías necesarias para ejecutar las aplicaciones de Java,    
y por otro lado el JDK esta penssado para el desarrollo, por lo que trae JRE más las herramientas necesarios como el compiladores, debuggear empaquetadores ...
[Diagrama de JDK 8](https://docs.oracle.com/javase/8/docs/)


## Requisitos
Los requisitos para esta practica es tener instalado el JDK 8,
aunque actualmente ya estamos por la version 18, la version 8 aun sigue siendo muy usada,
y para aprender como compilar el código fuente es suficiente. 
Para ello, podemos descargarlo el [JDK de Oracle](https://www.oracle.com/java/technologies/downloads/) o el [OpenJDK](https://openjdk.org/projects/jdk8/)
y añadir el path en Windows, en este caso.


![Imagen de la papelera del escritorio](/img/papelera.png)

Comprobamos que lo tenemos instalado
```
C:\Users\Ruben>java -version
java version "1.8.0_202"
Java(TM) SE Runtime Environment (build 1.8.0_202-b32)
Java HotSpot(TM) Client VM (build 25.202-b32, mixed mode)
```

Tambien comprobamos el comando `jar` para ejecutar archivos java.
Si no lo reconoce debemos añadirlo al path
```
#jar no se reconoce porque no esta en el path
C:\Users\Ruben>jar --help
"jar" no se reconoce como un comando interno o externo,
programa o archivo por lotes ejecutable.
```





## 1 Compilar y descompilar una clase java

### 1.1 Compilar HolaMundo
Para ver la ayuda
```
jar --help
```

Creamos un archivo llamado HolaMundo.java
```
public class HolaMundo {
	public static void main(String[] args) {
		System.out.println("Hola Mundo");
	}  
}
```

