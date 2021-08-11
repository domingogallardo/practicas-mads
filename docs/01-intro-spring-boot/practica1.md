<!--

Configuración de Github Classroom

- Una organización por curso: mads-ua-20-21, mads-ua-21-22, etc.
- Para actualizar la organización a un plan Team gratuito usar la página:
https://education.github.com/toolbox/offers/github-org-upgrades

https://classroom.github.com/help/upgrade-your-organization

-->

# Práctica 1: Primera aplicación con Spring Boot#

En esta práctica tendremos un primer contacto con Spring Boot, Git y Docker.

Los objetivos principales son:

- Empezar a conocer Spring Boot, ejecutando una sencilla aplicación _hola mundo_ en Spring Boot.
- Empezar a conocer el _framework_ de plantillas Thymeleaf, realizando
  pequeñas modificaciones en la aplicación que usen un formulario.
- Trabajar de forma regular, realizando pequeños commits que se deben
  subir al repositorio personal de la asignatura en GitHub.
- Crear una aplicación desplegable usando Docker
- Desplegar la aplicación en el servidor de la asignatura.

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

!!! Note "Nota del profesor sobre en el sistema operativo en el que realizar la práctica" 
    Aunque en los apuntes aparezca información
    sobre cómo trabajar desde Windows, no puedo garantizar que las
    instrucciones funcionen correctamente en todas las posibles
    configuraciones, ni te podré ayudar con posibles problemas, porque no
    es un sistema operativo que maneje habitualmente. Por tanto, si
    tienes Windows, te recomiendo que instales una máquina virtual
    Linux y la uses para la práctica.

Recomendamos hacer el desarrollo usando el IDE [IntelliJ
Ultimate](https://www.jetbrains.com/idea/download/). Aunque es de
pago, es posible [obtener una licencia de
estudiante](https://www.jetbrains.com/shop/eform/students) usando la
dirección de correo de la UA.

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
   
        $ git config --global user.name "Pepe Perez"
        $ git config --global user.email pepe.perez@example.com

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
    organización [mads-ua-21-22](https://github.com/mads-ua-21-22). Es un
    repositorio privado al que tienes acceso tú y el profesor. Contiene
    el código inicial del proyecto demostración de Spring Boot (es una
    copia del repositorio
    [domingogallardo/spring-boot-demoapp](https://github.com/domingogallardo/spring-boot-demoapp)).

    <img src="imagenes/aplicacion-inicial-spring-boot.png" width="700px"></img>
    
    Es importante que tengas en cuenta que el repositorio recién
    creado no reside en tu cuenta, sino en la organización
    `mads-ua-21-22`. Puedes acceder a él desde el _dashboard_ de GitHub que
    aparece cuando te logeas o pulsando en el icono de GitHub:
   
    <img src="imagenes/dashboard-github.png" width="700px"/>

4. El profesor te invitará a formar parte de la organización `mads-ua-21-22`
   y recibirás un mensaje de correo electrónico en el que deberás
   aceptar esta invitación. También se puede aceptar la invitación
   accediendo a <https://github.com/mads-ua-21-22>.
   

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

Una vez leído el documento [Introducción a Spring
 Boot](./intro-spring-boot.md) deberás descargar la aplicación
 `demo-spring-boot` que tienes en el repositorio creado en el punto 2
 anterior y comprobar que funciona correctamente. Debes hacer lo siguiente:

1. Descarga en tu ordenador el repositorio creado en GitHub en el punto
  2, usando el comando `git clone`:
  
    ```
    $ git clone springboot-demo-app-<usuario>
    ```
  
2. Importa la aplicación en IntelliJ, tal y como se explica en el
  documento _Introducción a Spring Boot_.
3. Prueba que se pasan todos los tests usando el comando Maven desde el terminal
  (`.mvnw`) y utilizando el panel de proyecto en IntelliJ.
4. Ejecuta la aplicación desde línea de comando y desde IntelliJ.
5. Haz algún pequeño cambio a la aplicación, cambiando el mensaje de
  saludo para incluir tu nombre. Comprueba que los tests pasan
  (modifícalos si no es así) y que la aplicación funciona
  correctamente.
  
### _Dockerización_ de la aplicación ###

La tecnología Docker [Docker](https://www.docker.com) permite
construir binarios (máquinas Docker) que pueden ser distribuidos y
ejecutados en ordenadores que tengan instalados el _Docker
Engine_. Las máquinas Docker son máquinas virtualizadas muy eficientes
que comparten los servicios del sistema operativo en el que se
ejecutan y utilizan menos recursos que las máquinas virtuales
tradicionales.

La tecnología es muy popular y se usa en gran cantidad de empresas de
desarrollo para simplificar la ejecución en en múltiples entornos y
para que los contenedores
(máquinas Docker en ejecución) se pueden configurar y combinar o
ejecutar en clusters usando herramientas como
[Kubernetes](https://kubernetes.io).

En nuestro caso, vamos a construir una _máquina Docker_ basada en la
aplicación demo. Posteriormente, la publicaremos en _Docker Hub_ y 
la desplegaremos en un _host_ para ponerla en producción.

1. Debes empezar por crear una cuenta de usuario en [Docker
Hub](https://hub.docker.com). De esta forma tendrás un repositorio en
el que podrás subir las imágenes de las máquinas Docker que
construyas. Deberás dar un nombre de usuario que será el que
utilizarás para publicar estas imágenes.

2. Crea un fichero llamado `Dockerfile` (sin extensión) en el
  directorio raíz de la aplicación con el siguiente contenido:
  
    **Fichero `./Dockerfile`:**

      ```docker
      FROM openjdk:8-jdk-alpine
      COPY target/*.jar app.jar
      ENTRYPOINT ["java","-jar","/app.jar"]
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
      aplicación (`app.jar`) con el comando `java`.

3. Asegúrate de que en el directorio raíz de la aplicación está
  el fichero JAR resultado de la compilación:
  
    ```bash
    $ ls -l ./target/*.jar
    ./target/demoapp-0.0.1-SNAPSHOT.jar
    ```

4. Ya puedes construir la máquina Docker con el siguiente comando,
  desde el directorio raíz de la aplicación (en el que debe estar el
  fichero `Dockerfile` anterior):

    ```bash
    $ docker build -t <usuario-docker>/spring-boot-demoapp
    ```

    Comprueba que la imagen se ha creado correctamente. Debe aparecer
    en el _Docker Desktop_ y con el comando `docker image ls`:
    
      ```bash
      $ docker image ls 
      REPOSITORY                            TAG
      domingogallardo/spring-boot-demoapp   latest 
      ```

5. Pon en marcha un la imagen con la aplicación:

    ```
    $ docker run -p 8080:8080 <usuario-docker>/spring-boot
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
      
    O borrarlo definitivamente con 
    
      ```
      $ docker container rm <identificador>
      ```
    
    Otros comandos útiles de Docker son:
    
    - `docker run -d` : lanza el contendor en modo _background_.
    - `docker run --rm` : lanza el contenedor de forma que al pararlo
      se borra automáticamente.
    - `docker container stop <identificador>` : para el contenedor
      indicado.
    - `docker container logs <identificador>` : muestra los logs del
      contenedor indicado.
    
    En la aplicación Docker Engine podemos realizar también muchos de
    estos comandos interactuando directamente con la
    interfaz. Pruébalo.
    
6. Ahora que has comprobado que el fichero `Dockerfile` funciona
   correctamente debes añadirlo a git y subirlo al respositorio
   GitHub:
   
     ```
     $ git status
     $ git add .
     $ git status
     $ git commit -m "Añadido Dockerfile"
     $ git push
     ```
    
7. Vamos a terminar publicando la imagen en tu cuenta de Docker Hub.

    - Ve a [Docker Hub](https://hub.docker.com) y logéate.
    - Crea un repositorio con el nombre `spring-boot-demoapp`. En ese
      repositorio vas a subir la imagen con el mismo nombre. En un
      repositorio Docker puedes mantener múltiples versiones de una
      misma imagen, usando _tags_.
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
    
### Puesta en producción de la aplicación ###
    
Por último deberás poner en producción la aplicación, conectándote al
servidor linux de la asignatura y poniendo allí en marcha la
aplicación.

1. Consulta en el foro de Moodle la dirección IP del servidor linux de
   la asignatura y tu usuario.

2. Conéctate al servidor con tu usuario y cambia tu contraseña. Por
   ejemplo, si tu usuario es `alu14` y la dirección IP del servidor es
   `161.35.65.197`:

    ```
    $ ssh alu02@161.35.65.197
    $ passwd
    ```
3. Comprueba si alguien más está utilizando el servidor:

    ```
    $ who
    alu02    pts/1        2021-08-11 07:01 (80.29.50.137)
    ```
    
    Si algún otro compañero está usando el servidor puede ser posible
    que se ralentice o que ya el puerto `8080` ya esté ocupado por la
    aplicación del compañero. En este último caso puedes usar un
    puerto diferente para poner la aplicación en producción.
    
4. Descarga tu imagen de la aplicación y ponla en funcionamiento:

    ```
    $ docker pull <usuario-docker>/spring-boot-demoapp
    $ docker run -p 8080:8080 <usuario-docker>/spring-boot-demoapp
    ```
    
    En el caso en que otro compañero tenga la aplicación en marcha en
    ese puerto aparecerá el siguiente mensaje de error:
    
    ```
    docker: Error response from daemon: driver failed programming ...
    Bind for 0.0.0.0:8080 failed: port is already allocated.
    ```
    
    En ese caso puedes usar otro puerto. El primer puerto es el que se
    refiere al host y el segundo a la aplicación corriendo en el
    contenedor. Por ejemplo, puedes usar el puerto `8081`:
    
    ```
    $ docker run -p 8081:8080 <usuario-docker>/spring-boot-demoapp
    ```
    
5. Comprueba que la aplicación funciona correctamente conectándote
   desde tu navegador al servidor linux de la asignatura y al puerto
   correctamente: <http://161.35.65.197:8080>.
   
    ¡Enhorabuena, ya tienes tu aplicación en producción!. Puedes
    llamar a cualquier amigo para que se conecte a esa URL y la pruebe.

    !!! Danger "Importante"
        Para entregar la práctica deberás ponerla en producción en el
        servidor de la asignatura y el profesor comprobará que
        funciona correctamente. Lo haremos en el horario de clase de prácticas.

6. Por último, para permitir que otros compañeros puedan trabajar con
   fluidez en el servidor, debes cerrar el contenedor, borrar la
   imagen y salir del servidor:
   
    ```
    $ docker container ls -a 
    $ docker container rm <container-id>
    $ docker image ls -a 
    $ docker image rm <nombre-imagen> o <image-id>
    $ exit
    ```

    !!! Danger "Importante"
        El objetivo de borrar la imagen Docker es evitar que el servidor de
        la asignatura se quede sin espacio de disco. El servidor tiene
        un espacio limitado que se debe compartir entre todos los
        estudiantes de la asignatura.
        
        No debes guardar ningún fichero ajeno a la asignatura en este
        servidor.
        

## 4. Añadimos alguna funcionalidad sencilla a la aplicación ##

Lee el siguiente documento:

- [Validating Form Input](https://spring.io/guides/gs/validating-form-input/)

Debemos añadir alguna funcionalidad sencilla a la aplicación que
realice lo siguiente:

- Leer datos de un formulario usando Thymeleaf y **realizar alguna validación**.
- Llamar a un **método de servicio** que procese los datos leídos.
- Mostrar el resultado devuelto por el servicio en una página Thymeleaf.
- Incluir al menos 2 tests:
    - 1 de la capa de servicio
    - 1 de la capa de presentación usando MockMvc y moqueando el servicio
- En la página principal de la aplicación debe aparecer tu nombre y apellidos.

Muy importante, debemos desarrollar la aplicación en **pequeños
commits**. Cada commit debe compilar correctamente y añadir una
pequeña funcionalidad. Debemos subir los commits al repositorio
personal de GitHub.

Debes definir tú la funcionalidad a implementar. Por ejemplo,
cualquiera de los siguientes ejemplos o alguno similar que se te ocurra:

- Palíndroma: lee una palabra y comprueba si es palíndroma.
- Número par: lee un número y comprueba si es par
- Cuadrado: lee dos números y comprueba si el segundo es el cuadrado del primero
- Calculadora: lee un par de números y una operación y devuelve el resultado.

Cuando compruebes que los tests funcionan correctamente y que la
aplicación funciona bien en local, debes crear la máquina Docker con
la etiqueta `final` y probar que funciona bien en producción en el
servidor de la asignatura.

## 5. Comandos Git ##

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


## 6. Entrega ##

- La práctica tiene una duración de 1 semana y debe estar terminada
  el martes 21 de septiembre. El miércoles 22 de septiembre el
  profesor comprobará en clase de prácticas el funcionamiento de la
  práctica en producción.
- La calificación de la práctica tiene un peso de un 10% en la nota
  final de prácticas.

Para realizar la entrega debes hacer lo siguiente:

- Realizar la aplicación en el repositorio creado e ir subiendo los
  commits a GitHub conforme se van realizando.
- Actualizar el fichero `README.md` con la URL del repositorio Docker
  Hub donde se ha subido la máquina Docker final.
- Realizar un breve documento técnico PDF en el que se explique la
  funcionalidad y el código añadido. Incluir en él la URL de los
  repositorios en GitHub y en Docker Hub. Incluir el documento en el
  proyecto proyecto con el nombre `doc/practica1.pdf` y subirlo a
  GitHub.
- Entregar en Moodle un ZIP con el directorio del proyecto (incluyendo el
  directorio .git con el repositorio git), después de haber hecho
  `./mvnw clean` para eliminar los binarios compilados.

Para la evaluación se tendrá en cuenta:

- Desarrollo continuo (los _commits_ deben realizarse a lo largo de
  toda la semana y no dejar todo para el último día).
- Correcto desarrollo de la metodología.
- Diseño e implementación del código y de los tests de las
  características desarrolladas.
