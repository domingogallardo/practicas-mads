<!--

Configuración de Github Classroom

- Una organización por curso: mads-ua-20-21, mads-ua-21-22, etc.
- Para actualizar la organización a un plan Team gratuito usar la página:
https://education.github.com/toolbox/offers/github-org-upgrades

https://classroom.github.com/help/upgrade-your-organization

-->

# Primera aplicación con Spring Boot#

Esta es la **primera parte** de la práctica 1. En esta parte tendremos un
primer contacto con Spring Boot. También usaremos Git.

Los objetivos principales son:

- Empezar a conocer Spring Boot, ejecutando una sencilla aplicación _hola mundo_ en Spring Boot.
- Empezar a conocer el _framework_ de plantillas Thymeleaf, realizando
  pequeñas modificaciones en la aplicación que usen un formulario.
- Trabajar de forma regular, realizando pequeños commits que se deben
  subir al repositorio personal de la asignatura en GitHub.

## Instalación de software ##

Vamos a trabajar bastante con el terminal. En Linux o macOS podemos
usar el terminal que viene con el sistema. En Windows se puede usar el
terminal Git Bash que se instala en la instalación de Git para
Windows.

Es posible desarrollar la práctica en cualquier sistema
operativo. Debemos instalar el siguiente software:

- Git
- Java JDK 8 o posterior
- Maven (opcional, se puede usar el comando `./mvnw` del proyecto)
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

- Instalar Git, Java y Maven:

```
$ sudo apt install git
$ sudo apt install default-jdk
$ sudo apt install maven
```

- Instalar [IntelliJ Ultimate](https://www.jetbrains.com/idea/download/)

#### macOS ####

- Git y Java vienen instalados con el sistema operativo. Recomendamos usar
[Homebrew](https://brew.sh) para instalar Maven:

```
$ brew install maven
```

- Instalar [IntelliJ Ultimate](https://www.jetbrains.com/idea/download/)

#### Windows ####

Es recomendable instalar [git for Windows](https://gitforwindows.org),
que además de Git instala Git BASH, un terminal Bash integrado en
Windows.

Además, hay que instalar Java, Maven e [IntelliJ Ultimate](https://www.jetbrains.com/idea/download/).


### Después de la instalación básica  ###

Es fácil probar que funciona el software instalado. Basta con ejecutar
desde el terminal:

```
$ git --version
$ mvn --version (imprime la versión de Maven y de Java)
```

Es también bastante útil configurar el prompt para que aparezca la
rama del repositorio Git en que nos encontramos. Para ello se debe
añadir en el fichero `$HOME/.bashrc` (linux y Git Bash Windows) o
`$HOME/.bash_profile` (macOS) :

```
parse_git_branch() {
    git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/ (\1)/'
}
export PS1="\[\e[37m\]\A \[\e[m\]\[\033[32m\]\W\[\033[33m\]\$(parse_git_branch)\[\033[00m\] $ "
```

Podemos encontrar más opciones de configuración del prompt en muchas
páginas en Internet. Por ejemplo
[aquí](https://www.cyberciti.biz/tips/howto-linux-unix-bash-shell-setup-prompt.html).

## Repositorio GitHub ##

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
    organización [mads-ua-20-21](https://github.com/mads-ua-20-21). Es un
    repositorio privado al que tienes acceso tú y el profesor. Contiene
    el código inicial del proyecto demostración de Spring Boot (es una
    copia del repositorio
    [domingogallardo/spring-boot-demoapp](https://github.com/domingogallardo/spring-boot-demoapp)).

    <img src="imagenes/aplicacion-inicial-spring-boot.png" width="700px"></img>
    
    Es importante que tengas en cuenta que el repositorio recién
    creado no reside en tu cuenta, sino en la organización
    `mads-ua-20-21`. Puedes acceder a él desde el _dashboard_ de GitHub que
    aparece cuando te logeas o pulsando en el icono de GitHub:
   
    <img src="imagenes/dashboard-github.png" width="700px"/>

4. El profesor te invitará a formar parte de la organización `mads-ua-20-21`
   y recibirás un mensaje de correo electrónico en el que deberás
   aceptar esta invitación. También se puede aceptar la invitación
   accediendo a <https://github.com/mads-ua-20-21>.
   

## Documentación a consultar ##

Para realizar la práctica debes leer los siguientes documentos:

- [Introducción a Spring Boot](./intro-spring-boot.md)
- [Validating Form Input](https://spring.io/guides/gs/validating-form-input/)

En el caso en que necesites más información puedes encontrar la
documentación de referencia de Spring Boot y Spring en las siguientes
páginas, en la pestaña _Learn_:

- [Spring Boot](https://spring.io/projects/spring-boot)
- [Spring](https://spring.io/projects/spring-framework) 

También podemos encontrar también una extensa cantidad de tutoriales y guías
rápidas en la web de Spring, en la url
[https://spring.io/guides](https://spring.io/guides).


## Enunciado de la práctica ##

Haremos una primera práctica sencilla en la que pondremos en
marcha una aplicación inicial en Spring Boot y añadiremos alguna
funcionalidad.

### Trabajamos con la aplicación Demo de Spring Boot ###

Debemos hacer lo siguiente:

- Descargar la aplicación demo de Spring Boot que hemos creado en
  GitHub usando el comando git clone.
- Importarla en IntelliJ
- Probar que se pasan todos los tests usando Maven e IntelliJ
- Ejecutarla desde línea de comando y desde IntelliJ
- Hacer algún pequeño cambio a la aplicación. Por ejemplo, cambiar los
  mensajes de saludo.
    
### Añadimos alguna funcionalidad sencilla a la aplicación ###
    
Debemos añadir alguna funcionalidad sencilla a la aplicación que
realice lo siguiente:

- Leer datos de un formulario usando Thymeleaf y realizando alguna validación.
- Llamar a un **método de servicio** que procese los datos leídos.
- Mostrar el resultado devuelto por el servicio en una página Thymeleaf.
- Incluir al menos 2 tests:
    - 1 de la capa de servicio
    - 1 de la capa de presentación usando MockMvc y moqueando el servicio

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

## Comandos Git ##

Comandos Git necesarios para realizar la práctica:

- git clone
- git status
- git add
- git commit
- git push
- git log

Puedes encontrar más información sobre estos comandos en documento
[comandos Git](./comandos-git.md) que resume los conceptos más
importantes de Git necesarios para estas primeras prácticas de la
asignatura.


## Entrega ##

- La práctica tiene una duración de 1 semana y debe estar terminada
  el martes 22 de septiembre.
- La calificación de la práctica tiene un peso de un 3% en la nota
  final de la asignatura.

Para realizar la entrega debes hacer lo siguiente:

- Realizar la aplicación en el repositorio creado e ir subiendo los
  commits conforme se van realizando.
- Entregar en Moodle un ZIP con el directorio del proyecto (incluyendo el
  directorio .git con el repositorio git), después de haber hecho
  `./mvnw clean` para eliminar los binarios compilados.

Para la evaluación se tendrá en cuenta:

- Desarrollo continuo (los _commits_ deben realizarse a lo largo de
  toda la semana y no dejar todo para el último día).
- Correcto desarrollo de la metodología.
- Diseño e implementación del código y de los tests de las
  características desarrolladas.
