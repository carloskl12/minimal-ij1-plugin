Versión original del proyecto en inglés [minimal plugin](https://github.com/imagej/minimal-ij1-plugin)

Esta es la estructuctura mínima para la implementación de un proyecto con Maven de un plugin para ImageJ 1.x.

Se pretende que sea un punto de partida ideal para desarrollar nuevos plugins para ImageJ 1.x en un IDE de su elección. Es posible colaborar con desarrolladores que trabajan con un IDE diferente al suyo.

En [Eclipse](http://eclipse.org), por ejemplo, esto es tan simple como
_File&gt;Import...&gt;Existing Maven Project_

En [Netbeans](http://netbeans.org), es incluso más simple: _File&gt;Open_
Project. De igual forma en [IntelliJ](http://jetbrains.net).

Si [jEdit](http://jedit.org) es su IDE preferido, necesita instalar [Maven
Plugin](http://plugins.jedit.org/plugins/?MavenPlugin).

Programadores rebeldes en línea de comandos pueden usar directamente  Maven 
llamando _mvn_ en el directorio raiz.

No obstante, al generar el proyecto, al final tendrá el archivo ```.jar```
(llamado *artifact* en la jerga Maven) en el subdirectorio _target/_

Para copiar el *artifact* en el lugar correcto, se debe llamar ```mvn
-Dimagej.app.directory=/path/to/Fiji.app/```. Esto no solamente copia el artifact,
si no tambien todas las dependencias. Para notar los cambios, reiniciar ImageJ o 
realizar *Help>Refresh Menus* para mirar su plugin en los menus.

Desarrollar plugins en un IDE es conveniente, especialmente para la fase de 
depuración (debugging). Para hacer debugging, el plugin contiene el método
_main()_ que establece la propiedad del sistema _plugins.dir_ (de modo que el 
plugin se agrega al menu Plugins), inicia ImageJ, carga una imagen y corre el plugin.
Mirar tambien [esta página](fiji.sc/Debugging#Debugging_plugins_in_an_IDE_.28Netbeans.2C_IntelliJ.2C_Eclipse.2C_etc.29)
para información de cómo hacer en Fiji para el debugging usando un IDE.

Dado que este proyecto pretende ser un punto de partida para sus propios desarrollos,
este es de dominio público

Cómo usar este proyecto como punto de partida
=============================================

Ya sea

* ```git clone git://github.com/imagej/minimal-ij1-plugin```, o
* Descomprimir https://github.com/imagej/minimal-ij1-plugin/archive/master.zip

Entonces:

1. Editar el archivo ```pom.xml```. Cada entrada debe ser bastante autoexplicativa.
   En particular, cambiar:
    1. el *artifactId* (**Nota**: debe contener un caracter'_'), nombre del plugin.
    2. el *groupId* (opcional)
    3. la *version* (notar que tipicamente cuando se desea usar un número de versión
     como sufijo,*_SNAPSHOT*, es  para indicar que el trabajo está en progreso en lugar de ser una versión final)
    4. las *dependencies* (leer como especificar correctamente la terna *groupId/artifactId/version* 
       [aquí](http://fiji.sc/Maven#How_to_find_a_dependency.27s_groupId.2FartifactId.2Fversion_.28GAV.29.3F))
    5.  *developer*, información del desarrollador.
    6. *scm* información scm.
2. Eliminar el archivo ```Process_Pixels.java``` y crear su archivo ```.java```  en
   ```src/main/java/<package>/``` (si necesita archivos de soporte como iconos en el resultado ```.jar```,
   colocarlos en ```src/main/resources/```)
3. Editar ```src/main/resources/plugins.config```
4. Reemplazar el contenido de ```README.md``` con la información acerca de su proyecto.

Si clonó el repositorio ```minimal-ij1-plugin```, probablemente desea publicar los 
resultados en su propio repositorio:

1. Llamar ```git status``` para verificar la lista de archivos modificados y que no 
    se deben ignorar (patrones de los archivos a ignorar se dan en .gitignore)
2. Llamar ```git add .``` y ```git add -u``` para  preparar los archivos actuales
    para un commit (en jerga de github, un commit es cuando se aceptan los cambios realizados)
3. Llamar ```git commit``` o ```git gui``` para realizar el commit.
4. [Crear un nuevo repositorio en GitHub](https://github.com/new)
5. ```git remote set-url origin git@github.com:<username>/<projectname>``` Enlaza con el repositorio
    remoto.
6. ```git push origin HEAD``` , sube los archivos.

### Eclipse:  Para asegurarse que Maven haga las copias en su carpeta de Fiji 

1. Ir a _Run Configurations..._
2. Escoger _Maven Build_
2. Agregar los siguientes parámetros: name: ```imagej.app.directory``` value: ```/path/to/Fiji.app/```

Esto asegura que el archivo final ```.jar``` también sea copiado en su carpeta de plugins de Fiji cada vez que Maven construye el proyecto.
