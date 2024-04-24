<!--

Configuración de Github Classroom

- Una organización por curso: mads-ua-20-21, mads-ua-21-22, etc.
- Para actualizar la organización a un plan Team gratuito usar la página:
https://education.github.com/toolbox/offers/github-org-upgrades

https://classroom.github.com/help/upgrade-your-organization

-->

# Práctica 1: Primera aplicación con Spring Boot#

En esta práctica tendremos un primer contacto con Spring Boot, Git y
Docker. Será una práctica de una semana.

Los objetivos principales son:

- Empezar a conocer Spring Boot, ejecutando una sencilla aplicación _hola mundo_ en Spring Boot.
- Empezar a conocer el _framework_ de plantillas Thymeleaf, realizando
  pequeñas modificaciones en la aplicación que usen un formulario.
- Trabajar de forma regular, realizando pequeños commits que se deben
  subir al repositorio personal de la asignatura en GitHub.
- Crear una aplicación desplegable usando Docker y publicar el contenedor en
  DockerHub
  
La duración de la práctica es de 1 semana, la fecha límite de
entrega es el día 19 de septiembre y su puntuación es de 0,4 puntos en la nota final
de la asignatura.

## 1. Instalación de software ##

Vamos a trabajar bastante con el terminal. En Linux o macOS podemos
usar el terminal que viene con el sistema. En Windows se puede usar el
terminal Git Bash que se instala en la instalación de Git para
Windows.

Es posible desarrollar la práctica en cualquier sistema
operativo. Debemos instalar el siguiente software:

- Git
- Java JDK 8 o posterior
- IntelliJ Ultimate

!!! Note "No puedo ayudar con posibles problemas en Windows"
    Aunque en los apuntes aparezca información sobre cómo trabajar desde
    Windows, no puedo garantizar que las instrucciones funcionen correctamente
    en todas las posibles configuraciones (aunque deberían funcionar bien, por
    estar trabajando con tecnología Java), ni te podré ayudar con posibles
    problemas, porque no es un sistema operativo que maneje habitualmente. Por
    tanto, si tienes Windows, te recomiendo que instales una máquina virtual
    Linux y la uses para la práctica.

### IntelliJ Ultimate ###

Recomendamos hacer el desarrollo usando el IDE [IntelliJ
Ultimate](https://www.jetbrains.com/idea/download/). Aunque es de
pago, es posible [obtener una licencia de
estudiante](https://www.jetbrains.com/shop/eform/students) usando la
dirección de correo de la UA.

### Alta en GitHub educativo ###

Darse de alta en GitHub con el correo de la UA y solicitar el [registro como
estudiante](https://education.github.com/discount_requests/application) para
obtener beneficios como el uso de GitHub Pro (que incluye Copilot) y poder
solicitar el [GitHub Student Developer
pack](https://education.github.com/pack/offers) con ofertas como $200 en 
servidores de Digital Ocean.

### Instalación básica ###

#### Linux ####

Para instalar el software en Linux.

- Instalar Git y Java:

```
$ sudo apt install git
$ sudo apt install default-jdk
```

- Instalar [IntelliJ Ultimate](https://www.jetbrains.com/idea/download/)

#### macOS ####

- Git y Java vienen instalados con el sistema operativo. 
- Instalar [IntelliJ Ultimate](https://www.jetbrains.com/idea/download/)

#### Windows ####

Es recomendable instalar [git for Windows](https://gitforwindows.org),
que además de Git instala Git BASH, un terminal Bash integrado en
Windows.

Además, hay que instalar Java e [IntelliJ Ultimate](https://www.jetbrains.com/idea/download/).


### Después de la instalación básica  ###

Es fácil probar que funciona el software instalado. Basta con ejecutar
desde el terminal:

```
$ git --version
$ java -version (imprime la versión de Java)
```

#### Configuración del prompt para que aparezca la rama de Git ####

**Bash**

Es también bastante útil configurar el prompt para que aparezca la
rama del repositorio Git en que nos encontramos. Para ello se debe
añadir en el fichero `$HOME/.bashrc` (linux y Git Bash Windows) o
`$HOME/.bash_profile` (macOS con shell `bash`) :

```
parse_git_branch() {
    git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/ (\1)/'
}
export PS1="\[\e[37m\]\A \[\e[m\]\[\033[32m\]\W\[\033[33m\]\$(parse_git_branch)\[\033[00m\] $ "
```

Podemos encontrar más opciones de configuración del prompt en muchas
páginas en Internet. Por ejemplo
[aquí](https://www.cyberciti.biz/tips/howto-linux-unix-bash-shell-setup-prompt.html).

**Zsh**

Si trabajas con el shell `zsh` que viene por defecto en MacOS, debes
añadir en el fichero `.zshrc` lo siguiente:

```
parse_git_branch() {
    git branch 2> /dev/null | sed -n -e 's/^\* \(.*\)/ [\1]/p'
}
setopt PROMPT_SUBST
export PROMPT='%1~%F{green}$(parse_git_branch)%f %% '
```

## 2. Creación del repositorio GitHub con la práctica ##

Para inicializar el repositorio de GitHub en el que vas a trabajar en
esta práctica debes seguir los siguientes pasos:

1. Inicializa tu nombre de usuario y tu correo en Git. El nombre de
   usuario será el nombre que aparecerá en los _commits_. Pon tu nombre
   y apellido.
   
    ```
    $ git config --global user.name "Pepe Perez"
    $ git config --global user.email pepe.perez@example.com
    ```

2. Crea una cuenta en GitHub. Puedes usar el nombre de usuario que
   quieras (o usar el que ya tienes), pero **escribe correctamente tu
   nombre y apellidos en el perfil** usando la opción _Settings >
   Profile_ y actualizando el campo _Name_.
   
3. Una vez logeado en GitHub, pincha en el enlace con una invitación
   que compartiremos en el foro de Moodle. Deberás aceptar las
   peticiones de GitHub Classroom y podrás aceptar la práctica _Spring
   Boot Demo App_. 

    <img src="imagenes/aceptar-classroom.png" width="500px"></img>
   
    Se creará automáticamente el repositorio `springboot-demo-app-<usuario>` en la
    organización [mads-ua-23-24](https://github.com/mads-ua-23-24/). Es un
    repositorio privado al que tienes acceso tú y el profesor. Contiene
    el código inicial del proyecto demostración de Spring Boot (es una
    copia del repositorio
    [domingogallardo/spring-boot-demoapp](https://github.com/domingogallardo/spring-boot-demoapp)).

    <img src="imagenes/aplicacion-inicial-spring-boot.png" width="700px"></img>
    
    Es importante que tengas en cuenta que el repositorio recién
    creado no reside en tu cuenta, sino en la organización
    `mads-ua-23-24`. Puedes acceder a él desde el _dashboard_ de GitHub que
    aparece cuando te logeas o pulsando en el icono de GitHub:
   
    <img src="imagenes/dashboard-github.png" width="700px"/>

4. El profesor te invitará a formar parte de la organización `mads-ua-23-24`
   y recibirás un mensaje de correo electrónico en el que deberás
   aceptar esta invitación. También se puede aceptar la invitación
   accediendo a <https://github.com/mads-ua-23-24>.
   

## 3. Aplicación Demo de Spring Boot ##

Haremos una primera práctica sencilla en la que primero pondremos en
marcha y publicaremos una aplicación inicial en Spring Boot y
después añadiremos alguna funcionalidad.

En el documento [Introducción a Spring Boot](./intro-spring-boot.md)
se explica cómo ejecutar una aplicación Spring Boot y cómo lanzar sus
tests. También se proporciona una introducción a los distintos
componentes de la aplicación. Debes leerlo y aprender el
funcionamiento básico de este _framework_.

### Construcción y ejecución de la aplicación ###

Lo primero que deberás hacer será descargar la aplicación
 `demo-spring-boot` que tienes en el repositorio creado en el punto
 anterior y comprobar que funciona correctamente. Debes hacer lo siguiente:

1. Configura un [Personal Access
   Token](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token) (PAT)
   en GitHub para poder autenticarte desde el terminal. Dale todos los
   permisos de acceso a repositorios y copia la clave generada. Será
   la contraseña que deberás introducir cuando un comando git te la
   pida.
   
2. Descarga en tu ordenador el repositorio creado en GitHub en el apartado
   anterior, usando el comando `git clone`:
  
    ```
    $ git clone https://github.com/mads-ua-23-24/springboot-demo-app-<usuario>.git
    ```

    Cuando git te pida autenticación, usa como nombre de usuario tu usuario
    de GitHub y como contraseña el PAT que has creado anteriormente.


Una vez descargado el repositorio con la aplicación deberás ejecutarla
desde la línea de comandos, probar los tests e importarla en IntelliJ
y ejecutar y depurar con el IDE la aplicación y los tests.

3. Desde el directorio donde está la aplicación, probamos todos sus
   tests usando el Maven Wrapper:
   
      ```
      $ ./mvnw test
      ```
     
4. Para poner en marcha la aplicación la arrancamos como una
   aplicación Java:

      ```
      $ ./mvnw package
      $ java -jar target/demoapp-0.0.1-SNAPSHOT.jar 
      ```

    También podemos lanzarla usando el plugin `spring-boot` de Maven:

      ```
      $ ./mvnw spring-boot:run
      ```

    La aplicación se arranca por defecto en el puerto local 8080. Una
    vez arrancada la aplicación podemos conectarnos desde un navegador
    a sus páginas de inicio.

    En el caso de la aplicación demo descargada, podemos probar las
    siguientes páginas:

    - [http://localhost:8080](http://localhost:8080)
    - [http://localhost:8080/saludo/Pepito](http://localhost:8080/saludo/Pepito)
    - [http://localhost:8080/saludoplantilla/Pepito](http://localhost:8080/saludoplantilla/Pepito)
    - [http://localhost:8080/saludoform](http://localhost:8080/saludoform)

Recomendamos hacer el desarrollo usando el IDE [IntelliJ
Ultimate](https://www.jetbrains.com/idea/download/). Aunque es de
pago, es posible [obtener una licencia de
estudiante](https://www.jetbrains.com/shop/eform/students) usando la
dirección de correo de la UA.

También es recomendable instalar el [plugin GithHub
Copilot para JetBrains](https://plugins.jetbrains.com/plugin/17718-github-copilot) para
trabajar con este asistente de IA como ayudante de código. Tras instalar el
plugin deberás activarlo introduciendo tu usuario de GitHub.

Puedes trabajar de forma gratuita con [GitHub
Copilot](https://github.com/features/copilot/) dándote de alta en el [GitHub
Student Developer Pack](https://education.github.com/pack).

5. Abre proyecto el en IntelliJ. Debes importar el directorio donde se
   encuentre el fichero `pom.xml`. Se puede hacer desde la pantalla de
   bienvenida de IntelliJ con la opción **Import Project** o usando la
   opción **"File > New > Project from Existing
   Sources**. Aparecerá la pantalla de importación y seleccionamos el
   importador **Maven**:


    <img src="imagenes/import-intellij.png" width="600px" />

    IntelliJ abre el proyecto correctamente:

    <img src="imagenes/proyecto-desplegado.png" width="350px"/>

    Podemos ejecutarlo abriendo un terminal y lanzándolo con Maven. O
    también desde la **configuración de Run** que ha creado IntelliJ al
    realizar la importación:

    <img src="imagenes/configuracion-run.png" width="250px"/>

    Se abrirá un panel de ejecución desde el que se puede parar la
    aplicación, volverla a lanzar, etc:

    <img src="imagenes/panel-ejecucion.png" width="900px"/>
    
    Desde la configuración de Run también podemos depurar el proyecto,
    pulsando el botón de depuración.

    <img src="imagenes/configuracion-debug.png" width="250px"/>

6. Lanza los tests desde el propio IntelliJ, pulsando en el
   panel del proyecto sobre el directorio de tests con el botón
   derecho. Los tests se lanzarán y aparecerá un panel en el que se
   mostrará si pasan correctamente (verde) o no.

    <img src="imagenes/tests-intellij.png" width="600px" />


Por último, haz algún pequeño cambio a la aplicación. 

7. Cambia el mensaje de saludo que da el controller de la raíz para incluir tu nombre. 
   Comprueba que los tests pasan (modifícalos si no es así) y que la aplicación funciona
   correctamente.

    <img src="imagenes/hello-world-nombre.png" width="500px"/>


### _Dockerización_ de la aplicación ###

[Docker](https://www.docker.com) es un software de virtualización que
utiliza el propio sistema operativo compartimentado y permite
gestionar _contenedores_ (similares a las máquinas virtuales) de forma
mucho menos pesada y rápida que con sistemas de virtualización
tradicionales como VirtualBox. 

Las máquinas Docker son muy eficientes porque comparten los servicios
del sistema operativo en el que se ejecutan, utilizando menos recursos
que las máquinas virtuales tradicionales. 

Docker proporciona un sistema muy sencillo de distribución y puesta en
producción de software, ya que las máquinas Docker pueden ser
distribuidas usando repositorios (como [Docker
Hub](https://hub.docker.com)) y ejecutadas en cualquier ordenador que
tenga instalado el _Docker Engine_.

La tecnología es muy popular y se usa en gran cantidad de empresas de
desarrollo para simplificar la ejecución en en múltiples entornos y
para que los contenedores
(máquinas Docker en ejecución) se pueden configurar y combinar o
ejecutar en clusters usando herramientas como
[Kubernetes](https://kubernetes.io).

En nuestro caso, vamos a construir una _máquina Docker_ basada en la
aplicación demo. Posteriormente, la publicaremos en _Docker Hub_ y 
la desplegaremos en un _host_ para ponerla en producción.

1. Instala [Docker
   Desktop](https://www.docker.com/products/docker-desktop). Los
   usuarios de Linux debéis seguir las instrucciones de [esta
   página](https://docs.docker.com/engine/install/ubuntu/) para
   instalar Docker Engine. Usaremos la línea de comando para lanzar
   los comandos Docker. La aplicación Docker Desktop permite usar una
   interfaz de usuario para interactuar con imágenes y contenedores,
   pero no proporciona ninguna funcionalidad que no esté disponible en
   la línea de comando.
   
     Una vez instalado puedes probar el tutorial rápido (2 minutos)
     desde Docker Desktop para comprobar que todo funciona
     correctamente. También puedes desde el terminal comprobar la
     versión de Docker instalada:
   
     ```
     $ docker version
     ```

2. Crea una cuenta de usuario en [Docker
   Hub](https://hub.docker.com). De esta forma tendrás un repositorio
   en el que podrás subir las imágenes de las máquinas Docker que
   construyas. Deberás dar un nombre de usuario que será el que
   utilizarás para publicar estas imágenes.
   

3. Crea un fichero llamado `Dockerfile` (sin extensión) en el
  directorio raíz de la aplicación con el siguiente contenido:
  
    **Fichero `./Dockerfile`:**

      ```docker
      FROM openjdk:8-jdk-alpine
      COPY target/*.jar app.jar
      ENTRYPOINT ["java","-Djava.security.egd=file:/dev/urandom","-jar","/app.jar"]
      ```

    El fichero `Dockerfile` consiste en un conjunto secuencial de
    instrucciones con las que se construye la máquina Docker:
    
    - `FROM`: este comando indica la máquina base sobre la que se van
      a ejecutar el resto de comandos. En nuestro caso una máquina de
      la organización `openjdk` que contiene la distribución 8 del
      `Java Development Kit (JDK)` y que está basada en una
      distribución linux Alpine. El primer paso de la construcción de
      nuestra máquina Docker consiste por tanto en descargar esta
      máquina `openjdk:8-jdk-alpine` y usarla como máquina base.
    - `COPY`: este comando indica que se debe copiar un fichero o
      conjunto de ficheros de la máquina host (el directorio en el que
      estamos) en la máquina base. En este caso se copia el fichero
      JAR que constituye nuestra aplicación que está situado en el
      directorio `./target` y se copia en la máquina Docker con el
      nombre `app.jar`.
    - `ENTRYPOINT`: este comando indica el comando a ejecutar cuando se
      pone en marcha la máquina Docker. En este caso se lanza la
      aplicación (`app.jar`) con el comando `java -jar`. 
      
        El modificador `-Djava.security.egd` hace que se inicialice el
        generador de números aleatorios de Java usando el fichero del
        sistema `/dev/urandom` en lugar del fichero por defecto
        `/dev/random`. Es necesario para resolver un bug que aparece
        al ejecutar el contenedor en servidores como los alojados en
        DigitalOcean.

4. Vuelve a compilar la aplicación para asegurarte de que se genera el fichero
   JAR que la contiene. Este fichero es que vamos a _dockerizar_.

    ```
    $ ./mvnw package
    $ ls -l ./target/*.jar
    ./target/demoapp-0.0.1-SNAPSHOT.jar
    ```

5. Ya puedes construir la máquina Docker con el siguiente comando,
  desde el directorio raíz de la aplicación (en el que debe estar el
  fichero `Dockerfile` anterior):

    ```bash
    $ docker build -t <usuario-docker>/spring-boot-demoapp . 
    ```

    Comprueba que la imagen se ha creado correctamente. Debe aparecer
    en el _Docker Desktop_ y con el comando `docker image ls`:
    
      ```bash
      $ docker image ls 
      REPOSITORY                            TAG
      domingogallardo/spring-boot-demoapp   latest 
      ```

6. Pon en marcha un la imagen con la aplicación:

    ```
    $ docker run -p 8080:8080 <usuario-docker>/spring-boot-demoapp
    ```
    
    El comando `docker run` pone en marcha la imagen indicada, creando
    lo que se denomina un _contenedor Docker_. Es similar a una máquina
    virtual en ejecución. El parámetro `-p 8080:8080` indica que el
    puerto interno 8080 del contenedor se va a mapear en el puerto
    8080 del _host_. De esta forma podremos conectarnos desde el
    _host_ a la aplicación Spring Boot en funcionamiento.
    
    Verás que en la consola aparecen los mensajes de salida de la
    aplicación Spring Boot que se ejecuta en el contenedor.
    
    Prueba a abrir un navegador y conectarte a la URL
    [localhost:8080](http://localhost:8080). Deberás ver el mensaje de
    saludo de la aplicación ejecutándose en el contendor.
    
    Haciendo `ctrl+c` puedes parar el contenedor. El efecto es similar
    a suspender una máquina virtual. Puedes ver el identificador del
    contenedor con el comando:
    
      ```
      $ docker container ls -a
      CONTAINER ID   IMAGE                NAMES
      5bd9d0b055a9   domingogallardo/spring-boot-demoapp  inspiring_feynman
      ```
    Puedes usar tanto el ID del contenedor (`5bd9d0b055a9`) como su
    nombre (`inspiring_feynman`) para identificarlo.
    
    Estando parado, puedes volver a poner en marcha el contenedor
    haciendo:
    
      ```
      $ docker container start <identificador>
      ```
      
    También podemos parar el contenedor:
    
      ```
      $ docker container stop <identificador>
      ```
       
    Y borrarlo definitivamente con 
    
      ```
      $ docker container rm <identificador>
      ```
    
    Otros comandos útiles de Docker son:
    
    - `docker run -d` : lanza el contendor en modo _background_.
    - `docker run --rm` : lanza el contenedor de forma que al pararlo
      se borra automáticamente.
    - `docker container logs <identificador>` : muestra los logs del
      contenedor indicado.
    
    En la aplicación Docker Engine podemos realizar también muchos de
    estos comandos interactuando directamente con la
    interfaz. Pruébalo.
    
7. Ahora que has comprobado que el fichero `Dockerfile` funciona
   correctamente debes añadirlo a git y subirlo al respositorio
   GitHub:
   
     ```
     $ git status
     $ git add .
     $ git status
     $ git commit -m "Añadido Dockerfile"
     $ git push
     ```
    
8. Vamos a terminar publicando la imagen en tu cuenta de Docker Hub.

    - Ve a [Docker Hub](https://hub.docker.com) y logéate.
    
    - Crea un repositorio **público** con el nombre `spring-boot-demoapp`. En
      ese repositorio vas a subir la imagen con el mismo nombre. En un
      repositorio Docker puedes mantener múltiples versiones de una misma
      imagen, usando _tags_.
      
    - Una vez creado el repositorio puedes publicar la imagen en él
      logeándote desde la línea de comando (introduce tu usuario y
      contraseña de Docker Hub) y con el comando `docker push`:
      
      ```
      $ docker login
      $ docker push <usuario-docker>/spring-boot-demoapp
      ```
      
      Verás que automáticamente se asigna la etiqueta `latest`
      (etiqueta por defecto) a la imagen y que ésta se sube al
      repositorio. Podrías asignar una etiqueta específica a la imagen
      con el comando `docker tag`. Por ejemplo, si quisiéramos fijar
      esta imagen con la versión `1.0` podríamos hacerlo con el
      siguiente comando:
      
      ```
      $ docker tag <usario-docker>/spring-boot-demoapp <usuario-docker>/spring-boot-demoapp:1.0
      ```
      
      - Comprueba en la página web del repositorio que se
      ha subido. El repositorio es público y cualquiera puede
      descargar la imagen haciendo:
      
      ```
      $ docker pull <usuario-docker>/spring-boot-demoapp
      ```

      Al no indicar la etiqueta, se descargaría la imagen etiquetada
      con `latest`. Si quisiéramos descargar una versión concreta
      habría que especificar la etiqueta:
      
      ```
      $ docker pull <usuario-docker>/spring-boot-demoapp:1.0
      ```

9.  Escribe en el fichero `README.md` del repositorio GitHub un enlace a la
    **vista pública** de la imagen en Docker Hub. La vista pública tiene el
    formato
    [https://hub.docker.com/r/domingogallardo/spring-boot-demoapp](https://hub.docker.com/r/domingogallardo/spring-boot-demoapp).

!!! Danger "Importante"
    Asegúrate de que es posible acceder al enlace de tu imagen docker  **sin estar logeado en
    DockerHub**. Abre otro navegador diferente en el que no estés logeado y prueba
    que el enlace funciona correctamente. Ese enlace es el que voy a usar para
    comprobar el funcionamiento correcto de la práctica.

## 4. Estudia el funcionamiento de la aplicación y su arquitectura ##

En el documento [Introducción a Spring Boot](./intro-spring-boot.md)
se comenta el código fuente de la aplicación Spring Boot con la que
estamos trabajando. Léelo despacio, revisando también el código
fuente, para entender los aspectos básicos (controladores, servicios,
inyección de dependencias, plantillas) del funcionamiento de
Spring Boot.

Estudia también despacio el funcionamiento de los tests y el
funcionamiento del formulario y la validación. 

Puedes ver un ejemplo adicional de validación de un formulario en el
repositorio
[domingogallardo/spring-boot-validate](https://github.com/domingogallardo/spring-boot-validate).

Verás también ahí varios ejemplos de tests en los que se realiza una
petición POST pasando parámetros y se obtiene información del modelo
resultante, llamando al método `model()`. El siguiente es un ejemplo
de uno de los tests:

```java
@Test
public void checkPersonInfoWhenNameTooShortThenFailure() throws Exception {
    mockMvc.perform(post("/")
                    .param("name", "R")
                    .param("age", "20"))
            .andExpect(model().hasErrors());
}
```

## 5. Añadimos alguna funcionalidad sencilla a la aplicación ##

Para demostrar que comprendes el funcionamiento de una aplicación
Spring Boot, debes añadir alguna funcionalidad sencilla a la aplicación
Demo. Debes definir tú la funcionalidad a implementar. Por ejemplo,
cualquiera de los siguientes ejemplos o alguno similar que se te ocurra:

- Palíndroma: lee una palabra y comprueba si es palíndroma.
- Número par: lee un número y comprueba si es par
- Cuadrado: lee dos números y comprueba si el segundo es el cuadrado del primero
- Calculadora: lee un par de números y una operación y devuelve el resultado.

La aplicación debe realizar lo siguiente:

- Leer datos de un formulario usando Thymeleaf y **realizar alguna validación**.
- Llamar a un **método de servicio** que procese los datos leídos.
- Mostrar el resultado devuelto por el servicio en una página Thymeleaf.
- Tests de la capa de servicio y de la capa de presentación
  (controllers web).
- En la página principal de la aplicación debe aparecer tu nombre y apellidos.

**Muy importante**, debemos desarrollar la aplicación en **pequeños
commits**. Cada commit debe compilar correctamente y añadir una
pequeña funcionalidad o debe realizar una refactorización en la que no se
incluye ninguna nueva funcionalidad pero se mejora el código. 

Debemos subir los commits al repositorio de GitHub.

!!! Note "Pequeños commits"
    Para la realización correcta de la práctica debes ir construyendo la
    aplicación a base de pequeños commits que incrementen su funcionalidad. Si
    no has trabajado nunca de esta forma te resultará algo complicado al
    principio, pero poco a poco irás cogiéndole el tranquillo.
    
    La idea es que antes de emepezar a escribir el código debes tener claro qué
    cosas quieres hacer. Veremos que la técnica de TDD nos ayuda a ello, pero
    por ahora no vamos a usarla. 
    
    Por ejemplo, si queremos hacer una aplicación que compruebe si una palabra 
    es palíndroma necestaremos una función en un servicio que haga esa
    comprobación. Procedemos entonces a escribir código para
    implementarla. Antes de grabar el commit debemos comprobar que funciona
    correctamente. ¿Cómo lo hacemos? Podemos hacerlo de dos formas: crear un
    sencillo controller que la llame a esa función con un ejemplo concreto o
    crear un test. Una vez comprobado que funciona correctamente la función
    grabamos el commit.
    
    Una vez terminada la capa de servicio deberemos programar el controller y el
    formulario para usar la aplicación. También lo debemos hacer poco a poco,
    con commits pequeños. Por ejemplo, primero podemos programar una versión
    sencilla (primer commit), después podemos añadir validaciones al formulario
    (segundo commit) y por último podemos hacer algún retoque del aspecto de la
    aplicación (tercer commit).


Cuando termines de implementar todos los tests (cuantos más mejor) y compruebes
que funcionan correctamente y que la aplicación funciona bien en local, debes
crear la máquina Docker con la etiqueta `final` y subirla a tu repositorio
DockerHub.

## 6. Comandos Git ##

Comandos Git necesarios para realizar la práctica:

- git clone
- git status
- git add
- git commit
- git push
- git log

Puedes encontrar más información sobre estos comandos en el documento
[Resumen de comandos Git](./comandos-git.md) que resume los conceptos más
importantes de Git necesarios para estas primeras prácticas de la
asignatura.


## 7. Entrega ##

- La práctica tiene una duración de 1 semana y debe estar terminada
  el martes 19 de septiembre.

- La calificación de la práctica tiene un peso de un 4% en la nota
  final de la asignatura.

Para realizar la entrega debes hacer lo siguiente:

- Realizar la aplicación en el repositorio creado e ir subiendo los
  commits a GitHub conforme se van realizando.
- Actualizar el fichero `README.md` con el enlace a la vista pública de la
  imagen subida DockerHub. En esa página debe estar la imagen con la etiqueta
  `final`. El formato de la URL debe ser
  `https://hub.docker.com/r/<usuario-docker>/spring-boot-demoapp`.
- Añadir una página de documentación `doc/practica1.md` en la que se
  explique brevemente tanto la funcionalidad como la implementación y tests
  añadidos. Se debe incluir también la URL  de los repositorios en GitHub y en Docker
  Hub. Deberás escribir esta documentación en Markdown. Tienes
  disponible en GitHub una breve pero útil [introducción a
  Markdown](https://guides.github.com/features/mastering-markdown/).
- Entregar en Moodle un ZIP con el directorio del proyecto (incluyendo el
  directorio .git con el repositorio git), después de haber hecho
  `./mvnw clean` para eliminar los binarios compilados.

Para la evaluación se tendrá en cuenta:

- Desarrollo continuo (los _commits_ deben realizarse a lo largo de
  toda la semana y no dejar todo para el último día).
- Commits pequeños, cada commit debe ser funcional e introducir algún elemento
  nuevo o realizar alguna refactorización.
- Correcto desarrollo de la metodología.
- Diseño e implementación del código y de los tests de las
  características desarrolladas.

!!! Danger "Penalización por realizar la práctica el último día"
    En la asignatura se recompensa el trabajo continuo y la realización de los
    _commits_ a lo largo de toda la semana. Si se realiza todo el trabajo en el
    último día se tendrá una penalización en la nota.
