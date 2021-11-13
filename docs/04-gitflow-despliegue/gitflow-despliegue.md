
# Práctica 4: Trabajo en equipo con GitFlow y despliegue en producción

## 1. Objetivos y resumen de la práctica ##

En esta práctica se pretende conseguir:

1. Crear los equipos de trabajo en GitHub.
2. Adaptar el flujo de trabajo en Git y GitHub al trabajo en equipo.
3. Desplegar la aplicación usando una base de datos de producción y
   mantener esta base de datos.
4. Implementar GitFlow:
    - Desarrollar nuevas features con GitFlow.
    - Lanzamiento de una versión nueva usando GitFlow.

## 2. Formación de equipos ##

En esta práctica comenzamos a trabajar en equipos de 3 personas.

Cada equipo trabajará con un repositorio común seleccionado de uno de
los miembros del equipo. Utilizaremos _GitHub Classroom_ para crear el
_team_ y el repositorio.

### Pasos a seguir ###

- Debéis formar equipos de **3 personas**. Enviad los componentes al
  foro de Moodle y os asignaré un nombre de equipo. Utilizad después
  el enlace de GitHub Classroom que enviaré al foro de Moodle para
  crear el equipo y apuntaros a él.
  
    El primero que use el enlace debe crear el repositorio,
    escribiendo el nombre del equipo, como se muestra en la siguiente
    imagen.

    <img src="imagenes/nombre-repo-github-classroom.png" width="600px"/>

    El equipo trabajará con un repositorio creado por GitHub Classroom
    con el nombre `todolist--NOMBRE-EQUIPO`. Al igual que en
    la práctica 2, el repositorio se creará en la organización `mads-ua-21-22`.

    <img src="imagenes/repo-creado-github-classroom.png" width="700px"/>

    Una vez que la primera persona ha creado el equipo y el
    repositorio, las siguientes personas que usan el enlace pueden
    unirse al equipo creado o crear un nuevo equipo:
    
    <img src="imagenes/unirse-repo-github-classroom.png" width="700px"/>

- Una vez creado el repositorio debéis crear en él un tablero para
  gestionar las tarjetas con los _issues_ y los pull
  requests. Creadlos con las mismas columnas que en las prácticas 2 y 3.

- Escoged el proyecto que vais a usar como punto de partida de estas
  dos últimas prácticas de entre los proyectos de los miembros del
  equipo. Intentad que se un proyecto con código limpio y fácilmente
  ampliable.

    Subidlo al nuevo repositorio, cambiando la URL del `origin` del
    repositorio local y haciendo un push:

    ```
    $ git remote set-url origin https://github.com/mads-ua-21-22/todolist-NOMBRE-EQUIPO.git
    $ git push -u origin main
    ```
    Por último, los otros miembros del equipo deberán clonar el
    repositorio para que los tres podáis trabajar con él en local.

- Cambiad el nombre del proyecto (en el fichero `POM.xml` y en el
  `about.html` a `todolist-equipo-XX`.

    Haced un commit directamente en `main` con estos
    cambios. Comprobad que GitHub Actions sigue funcionando
    correctamente. 

## 3. Nuevo flujo de trabajo para los _issues_ ##

Debemos adaptar el flujo de trabajo en GitHub al trabajo en equipo. En
cuanto a la gestión de los _issues_ y tablero del proyecto cambiaremos
lo siguiente:

- **Selección del _issue_**: Al pasar un _issue_ de `To do`a `In
  progress` se debe asignar un responsable del desarrollo del _issue_.
- **Nueva rama con el _issue_**: El responsable seleccionado será el que abra una
  rama nueva para el desarrollo del ticket y la subirá a
  GitHub.
- **Desarrollo**: Se trabaja en la rama. Cualquier compañero puede
  unirse al ticket y trabajar junto con el responsable, trabajando
  sobre la rama.
- **Pull request**: Cuando el ticket se ha terminado, el responsable
  abre un pull request en GitHub y pone la tarjeta en la columna
  `In pull request`.
- **Revisión de código**: Los miembros del equipo revisan el código en
  el pull request (consultar documentación en GitHub: [Reviewing
  proposed changes in a pull
  request](https://help.github.com/articles/reviewing-proposed-changes-in-a-pull-request/)). Al
  menos uno de los miembros del equipo deben dar el OK, añadiendo una
  reacción. Debéis configurar la opción de GitHub que obliga a que
  haya un [mínimo de revisores](https://docs.github.com/en/free-pro-team@latest/github/administering-a-repository/enabling-required-reviews-for-pull-requests) en el pull request.
- **Integración del pull request**: Cuando un miembro da el OK, el
  responsable de la tarea integra el pull request.

Para implementar el trabajo en equipo será necesario trabajar sobre
ramas remotas compartidas. A continuación explicamos con más detalle
algunos aspectos comandos de Git necesarios.

### Comandos Git ###

Veamos algunos comandos de Git relacionados con el trabajo compartido
en repositorios y ramas remotas.

- Subir una rama al repositorio remoto:

    ```
    $ git checkout -b nueva-rama
    $ git push -u origin nueva-rama
    ```

- Descargar por primera vez una rama del repositorio remoto y moverse
  a ella

    ```
    $ git fetch
    $ git checkout nueva-rama 
    ```

    El comando `git fetch` se descarga todos los cambios pero no los
    mezcla con las ramas locales. Los deja en ramas locales conectadas
    con las remotas (ramas _remote tracking_) a las que les da el
    nombre del servidor y la rama (`origin/nueva-rama`). Estas ramas
    _remote tracking_ son de solo lectura y no podemos hacer commits
    en ellas. Para trabajar con ellas hay que crear una rama local
    conectada a ella (normalmente tendrá el mismo nombre, por ejemplo
    `nueva-rama`). 

    En el caso del comando anterior, el comando
    
    ```
    $ git checkout nueva-rama
    ```
    
    es equivalente a 
    
    ```
    $ git checkout -b nueva-rama origin/nueva-rama
    ```
    
    Se está creando una rama local `nueva-rama` conectada a la rama
    `origin/nueva-rama`.

- Actualizar una rama con cambios que otros compañeros han subido al
  repositorio remoto:

    ```
    $ git checkout nueva-rama
    $ git pull
    ```

    El comando `git pull` es equivalente a un `git fetch` seguido de
    un `git merge`. El comando `git fetch` actualiza la rama local
    conectada con la _remote tracking_ `origin/nueva-rama`. El comando `git pull`
    es equivalente a hacer:

    ```
    $ git checkout nueva-rama
    $ git fetch
    $ git merge origin/nueva-rama
    ```

- Subir cambios de la rama actual:

    ```
    (estando en la rama que queremos subir)
    $ git push
    ```

    Si somos nosotros los que hemos creado la rama, hay que
    configurarla para que funcione correctamente el `git push`
    haciendo:
    
    ```
    $ git push -u origin nueva-rama
    ```
        
- Comprobar el estado de las ramas locales:

    ```
    $ git branch -vv
    ```

    Con la opción `-a` (`git branch -vva`) se muestra también el
    estado de las ramas _remote tracking_ de solo lectura (en rojo, y
    precedidas con el nombre `remotes/`):
    
    ```
    $  git branch -vva
      main                  dd867ac [origin/main] Colocados esquemas en su directorio
    * prueba                8d2d093 [origin/prueba] Corrección
      remotes/origin/HEAD   -> origin/main
      remotes/origin/main   dd867ac Colocados esquemas en su directorio
      remotes/origin/prueba 8d2d093 Corrección
    ```
    
    Este comando no accede directamente al servidor, sino que muestra
    la información de la última vez que se accedió a él. Si queremos
    la información actualizada podemos hacer un `git fetch --all`
    antes:

    ```
    $ git fetch --all
    $ git branch -vva
    ```

    Es importante recordar que `git fetch` (a diferencia de `git
    pull`) no modifica los repositorios locales, sino que actualiza
    las ramas _remote tracking_.

- Información de los repositorios remotos:

    ```
    $ git remote show origin
    ```

    Proporciona información del repositorio remoto, todas sus ramas,
    del local y de la conexión entre ambos.

    ```
    $ git remote -v update
    ```

    Proporciona información del estado de las ramas remotas y locales
    (si están actualizadas o hay cambios en algunas no bajadas o
    subidas).

- Borrado de ramas remotas desde el terminal:

    ```
    $ git push origin --delete nueva-rama
    $ git remote prune origin
    ```

- Si necesitamos en la rama de _feature_ código que se haya añadido en
  la rama `main`.
  
    Podemos hacer un _merge_ de la rama `main` en la rama de
    _feature_ para incorporar los avances de código que se han hecho
    en `main` y que necesitamos en nuestra nueva rama:
    
    ```
    $ git checkout nueva-rama
    $ git merge main
    ```


- Solución de conflictos en un _pull request_:

    Recordamos lo que hemos visto en teoría sobre la solución de
    conflictos detectados en un _pull request_.
    
    Supongamos que hay un conflicto entre la nueva rama y
    `main`. GitHub detectará el conflicto en la página de _pull
    request_. Para arreglar el conflicto:
    
    ```
    $ git checkout main
    $ git pull
    $ git checkout nueva-rama
    $ git merge main
    # arreglar el conflicto
    $ git push
    # ya se puede hacer el merge en GitHub
    ```
    
### Pasos a seguir ###

1. Añadid el milestone 1.3.0 y etiquetad todos los próximos issues con
  él. Probad el nuevo flujo de trabajo descrito anteriormente creando
  un nuevo _issue_ denominado `Actualizar la página Acerca de`. En la
  descripción de _issue_ comentad que se debe modificar la página para
  que muestren todos los miembros del equipo y el nuevo número de
  versión de la aplicación (`1.3.0-SNAPSHOT`).

2. Escoged una persona del equipo como responsable del _issue_. El
  responsable del _issue_ será el responsable de integrarlo en
  `main` y de solucionar los conflictos que puedan surgir.

3. Probad los comandos Git anteriores en una rama en la que se
  resuelva el _issue_. Cada miembro del equipo deberá descargar esa
  rama y realizar un commit en el que se añada su nombre a la lista de
  autores de la aplicación.

4. Cread el pull request en GitHub, poniendo como responsable del PR al
  mismo responsable del _issue_.

5. Provocad un conflicto y arregladlo. Para ello se debe añadir un
  commit en `main` que entre en conflicto con los cambios realizados
  en la rama. Después se arreglará el conflicto y se subirá la
  solución al pull request.

6. Por último, revisad el código, aceptadlo e integrad el PR en
   _main_.


## 4. Contenedor con la aplicación ToDoList ##

Una de las cosas que vamos a hacer en esta práctica (en el siguiente
apartado) es poner en producción en el servidor de la asignatura la
aplicación ToDoList conectándola con la base de datos. En las
prácticas 1 y 2 ya hemos construido el contenedor Docker de la
aplicación, con el siguiente fichero Dockerfile:

```docker
FROM openjdk:8-jdk-alpine
COPY target/*.jar app.jar
ENTRYPOINT ["java","-Djava.security.egd=file:/dev/urandom","-jar","/app.jar"]
```

Este Dockerfile tiene un problema importante. El comando de ejecución
es fijo y no permite definir ningún parámetro de ejecución. No es
posible, por ejemplo, definir el perfil de Postgres, ni definir
ningún parámetro de configuración.

Debemos cambiarlo de la siguiente forma:

```docker hl_lines="3"
FROM openjdk:8-jdk-alpine
COPY target/*.jar app.jar
ENTRYPOINT ["sh","-c","java -Djava.security.egd=file:/dev/urandom -jar /app.jar ${0} ${@}"]
```

De esta forma podremos llamar al comando docker añadiendo al final
parámetros que se van a pasar al comando java. La forma de añadir
variables de entorno a ese comando java es precediéndolos con dos
guiones `--`. Por ejemplo:

```
$ docker run --rm <usuario>/mads-todolist-equipoXX --spring.profiles.active=postgres --POSTGRES_HOST=host-prueba 
```

Vamos a probarlo, creando y subiendo la nueva imagen a
DockerHub y desplegándola en el servidor de la asignatura.

### Pasos a seguir ###

Debéis hacer lo siguiente:

1. Creamos un issue llamado `Configuración imagen docker` y
   trabajamos en la rama `imagen-docker`.

2. Cambiad el fichero Dockerfile de la aplicación tal y como se indica en el listado
   anterior:
   
    **Fichero `Dockerfile`**:

    ```docker
    FROM openjdk:8-jdk-alpine
    COPY target/*.jar app.jar
    ENTRYPOINT ["sh","-c","java -Djava.security.egd=file:/dev/urandom -jar /app.jar ${0} ${@}"]
    ```

3. Cread la nueva imagen Docker con el nombre
   `mads-todolist-equipoXX` y la etiqueta `1.3.0-snapshot`. El usuario puede ser cualquier miembro
   del equipo, no es necesario que sea el autor del proyecto original.
   
    ```
    $ ./mvnw package
    $ docker build -t <usuario-docker>/mads-todolist-equipoXX:1.3.0-snapshot . 
    ```

3. Probad que funcionan correctamente los parámetros de configuración
   en la imagen Docker. Una forma sencilla de hacerlo es comprobar que
   se puede definir el perfil de Postgres y modificar alguno de sus
   parámetros. Deberá aparecer un mensaje de error de que no se puede
   conectar con la base de datos (lo que está bien, porque significa
   que sí que se ha cargado el perfil).
   
    ```
    $ docker run --rm <usuario>/mads-todolist-equipoXX:1.3.0-snapshot --spring.profiles.active=postgres --POSTGRES_HOST=host-prueba 
    ```

    <img src="imagenes/perfil-contenedor.png" width="700px" />
    <img src="imagenes/error-contenedor.png" width="700px" />

4. Subid, por último, la imagen a Docker Hub y cerrad el PR y el issue.
   
    ````
    $ docker login
    $ docker push <usuario-docker>/mads-todolist-equipoXX:1.3.0-snapshot
    ````


## 5. Despliegue en producción con BD ##

Vamos a ver cómo ejecutar en producción el contenedor con la
aplicación de forma que se conecte con una base de datos postgres.

En las prácticas 1 y 2 vimos cómo construir una versión en forma de
contenedor de nuestra aplicación Spring Boot y en la práctica 3 vimos
como usar un contenedor de Postgres para definir un servicio de base
de datos con el que conectar la aplicación.

En esta práctica vamos a definir la configuración en producción
definitiva de nuestra aplicación. Veremos cómo poner en marcha dos
contenedores y conectarlos entre si. En nuestro caso un contenedor
tendrá la base de datos postgres y el otro la aplicación Spring Boot.

<img src="imagenes/contenedores-produccion.png" width="600px"/>

La imagen anterior muestra los dos contenedores conectados por una
red. Desde el contenedor con la aplicación se accederá a la dirección
`postgres:5432` para conectarse con la base de datos. Veremos los
comandos de docker para definir una red y para lanzar el contenedor de
base de datos en esa dirección de la red.

El contenedor de base de datos montará el directorio actual del host
en el directorio `/mi-host` del contenedor. De esta forma, cualquier
fichero que coloquemos en ese directorio del contenedor será visible
en el directorio actual del host (y viceversa). Usaremos este
directorio para guardar datos de la base de datos, como copias de
seguridad o ficheros de migración.

El contenedor de base de datos implementará la base de datos en
producción. 

!!! Note "Base de datos de producción"
    La base de datos de producción es la que mantiene los datos
    introducidos por los usuarios de la misma. Hay que prestar una
    atención especial a esta base de datos y definir políticas de
    respaldo y de control de cambios para evitar que se produzca
    cualquier pérdida de información. Veremos que una
    de las cuestiones que hay que asegurar es que la aplicación no
    puede modificar el esquema de datos de esta base de datos. 
    
    Habrá que definir también un flujo de trabajo para actualizar la base de
    datos de producción con los cambios del modelo de datos
    introducidos por la nuevas funcionalidades (nuevas tablas y nuevas
    relaciones).

### Pasos a seguir ###

Veamos paso a paso cómo crear la configuración anterior. En muchos
casos tendremos que usar el nombre de nuestro equipo. En los ejemplos
hemos usado `equipo01`. Debéis cambiarlo por el nombre de vuestro equipo.

1. Nos conectamos al servidor de la asignatura con uno de los usuarios
   del equipo. La dirección IP está en un mensaje enviado al foro de
   la asignatura.

    ```
    $ ssh alu02@<direccion-IP>
    ```

2. Creamos una red gestionada por Docker:

    ```
    $ docker network create network-equipo01
    ```

3. Lanzamos el contenedor con la base de datos usando la red creada
  anteriormente y con el nombre `db-equipo01`. Definimos el nombre del
  host creado en el contenedor como `postgres` con el modificador
  `--network-alias`.

    ```
    $ docker run -d --network network-equipo01 --network-alias postgres -v ${PWD}:/mi-host --name db-equipo01 -e POSTGRES_USER=mads -e POSTGRES_PASSWORD=mads -e POSTGRES_DB=mads postgres:13
    ```

    El modificador `-v` permite montar el directorio actual en el
    directorio `/mi-host` del contenedor. Vamos a probar que funciona
    correctamente. 

4. Nos conectamos al contenedor lanzando un `bash`
   interactivo. Estando en el contenedor creamos un fichero en el
   directorio `/mi-host`, salimos del contenedor y comprobamos que
   está en el directorio actual

    ```
    $ docker exec -it db-equipo01 bash
    root@e470db191dc6:/# cd /mi-host
    root@e470db191dc6:/mi-host# echo "Hola" > prueba.txt
    root@e470db191dc6:/mi-host# exit
    $ ls
    prueba.txt
    $ more prueba.txt
    Hola
    ```

5. Con esto ya tenemos configurado y en marcha el contenedor con la
   base de datos Postgres. Esta va a ser nuestra base de datos de
   producción. Vamos ahora a poner en marcha la aplicación.

    Descargamos la última versión de nuestra aplicación y lanzamos el
    contenedor usando la red definida anteriormente. Los modificadores
    `--spring.profiles.active` y `--POSTGRES_HOST` permiten pasar al
    contenedor esas variables del entorno.

    ```
    $ docker pull <usuario>/mads-todolist-equipo01:1.3.0-snapshot
    $ docker run --rm --name spring-boot-equipo01 --network network-equipo01 -p8080:8080 <usuario>/mads-todolist-equipo01:1.3.0-snapshot --spring.profiles.active=postgres --POSTGRES_HOST=postgres
    ```

    ¡¡¡Enhorabuena!!! ¡Ya tenemos la aplicación en producción
    trabajando con la base de datos!

    Podremos conectarnos a la aplicación usando la dirección IP del
    servidor de la asignatura y el puerto 8080.

    Probamos la aplicación y creamos algún usuario de prueba. Por último
    paramos el contenedor y lo volvemos a arrancar para comprobar que los
    datos son persistentes.

6. Para comprobar que la base de datos está funcionando correctamente
   podemos conectarnos al contenedor y examinar la base de datos
   `mads` y alguna de sus tablas:

    ```
    $ docker exec -it db-equipo01 bash
    # psql -U mads -W mads (nos pedirá la contraseña: mads)
    # \l (lista las bases de datos)
    # \dt (lista las tablas)
    # SELECT * FROM usuarios;
    ```

    La base de datos se mantendrá mientras que no borremos el
    contenedor. Podemos pararlo y volver a ponerlo en marcha y seguiremos
    conservando los datos:

    ```
    $ docker stop db-equipo01
    $ docker start db-equipo01
    ```

## 6. Perfil de producción y mantenimiento de la base de datos de producción ##

### Perfil de producción ###

Una vez que vamos a trabajar en producción con una base de datos, esta
base de datos será un elemento clave de la aplicación. No debemos,
bajo ningún concepto, perder datos que se hayan introducido en ella,
ya que son datos de nuestros usuarios y clientes.

Es imprescindible para ello cambiar el modo con el que la aplicación
construye las tablas de la base de datos. Sabemos que nuestra
aplicación está trabajando con JPA/Hibernate y que las tablas de la
base de datos se construyen de forma automática. Si hay algún cambio
en las entidades (se añade algún atributo o alguna nueva entidad)
Spring Boot actualiza las tablas de la base de datos de forma
automática cuando se lanza la aplicación. Esto es razonable si estamos
trabajando en un entorno de desarrollo, pero está **totalmente
desaconsejado** en un entorno de producción.

El parámetro `spring.jpa.hibernate.ddl-auto` es el que determina el
funcionamiento de la actualización de las tablas de la base de
datos. Su valor puede ser:

- `CREATE`: El esquema de datos se crea de nuevo cada vez que se lanza
  la aplicación. Una vez creado, se añaden los datos definidos en el
  fichero `spring.datasource.data` si el
  `spring.datasource.initialization-mode` tiene como valor
  `always`. Esta es la forma de funcionar de los tests.

- `UPDATE`: El esquema de datos de la base de datos se actualiza
  automáticamente cuando hay un cambio en las entidades de la
  aplicación. Así es como tenemos configurado el perfil por defecto de
  nuestra aplicación. Si estamos trabajando con la base de datos
  Postgres, se actualizará el esquema de datos. Pero esto no es
  recomendable para producción, porque no tenemos control de las
  instrucciones de actualización y pueden resultar en alguna pérdida
  de datos.

- `VALIDATE`: El esquema de datos de la base de datos se valida con
  respecto al esquema de datos definido por las entidades JPA. Si hay
  alguna diferencia, salta una excepción. Este es el valor que hay que
  usar cuando lanzamos la aplicación en producción.
  
Vamos a definir en la aplicación un nuevo perfil de ejecución, llamado
`postgres-prod`, en el que pondremos el valor del parámetro
`spring.jpa.hibernate.ddl-auto` a `VALIDATE`. Y será este el perfil
que usaremos para lanzar la aplicación en el servidor de producción.


### Mantenimiento de la base de datos de producción ###

En una aplicación en producción se deben configurar políticas
estrictas de realización de copias de seguridad y de integridad de los
datos. También en la gestión de las versiones y en la actualización
del esquema de datos. 

Esto último se denomina una _migración_ de la base de datos y
representa un elemento fundamental del mantenimiento en producción de
una aplicación, sobre todo cuando estamos trabajando de una forma ágil
e incremental. Es un tema avanzado muy importante, pero que no podemos
abordar en la asignatura por falta de tiempo. Un par de referencias
que os pueden ser de utilidad son el artículo [Evolutionary Database
Design](https://martinfowler.com/articles/evodb.html) y herramientas
como
[Flyway](https://www.baeldung.com/database-migrations-with-flyway) que
permiten automatizar las migraciones de la base de datos.

En la práctica vamos a trabajar con la base de datos de producción de
dos formas:

1. Realizaremos una copia de seguridad antes de instalar una nueva
   versión.
2. Actualizaremos el esquema de datos aplicando un fichero de
   migración que construiremos manualmente.

#### Copias de seguridad ####


Si eliminamos el contenedor con la base de datos se perderán todos los
datos. Para evitar perder los datos, con el contenedor en marcha
podemos hacer una copia de seguridad de la base de datos `mads` en el
directorio compartido:

```
$ docker exec -it db-equipo01 bash
# pg_dump -U mads --clean mads > /mi-host/backup03092021.sql
```

La copia de seguridad se guarda en el directorio compartido. Podemos
poner la fecha en el nombre del fichero. Por ejemplo, la copia
anterior ha sido creada el 3 de septiembre del 2021.

Para restaurar una copia de seguridad basta con ejecutar el fichero
SQL en la base de datos:

```
$ docker exec -it db-equipo01 bash
# psql -U mads mads < /mi-host/backup03092021.sql
# exit
```

#### Migración de la base de datos ####

Podemos obtener el esquema de datos de la aplicación (la definición de
las tablas, sin los datos) conectándonos al contenedor y ejecutando el
siguiente comando para guardar el fichero en el directorio compartido:

```
$ docker exec -it db-equipo01 bash
# pg_dump -U mads -s mads > /mi-host/schema.sql
# exit
```

Tendremos el esquema de datos en el directorio actual, que hemos
montado en el contenedor con la instrucción -V.

Los esquemas son instrucciones SQL en texto plano. Supongamos que
tenemos una nueva versión de la aplicación (`1.3.0`) en la que hemos
añadido el atributo `descripcion` a la entidad `Equipo`.

Si generamos el esquema de datos de esta nueva versión y lo llamamos
`schema-1.3.0.sql` lo podemos comparar con el esquema anterior usando
el comando de linux `diff`:

```
% diff sql/schema-1.3.0.sql sql/schema-1.2.0.sql 
41,42c41
<     nombre character varying(255),
<     descripcion character varying(255)
---
>     nombre character varying(255)
```

Por ejemplo, en el ejemplo mostrado, el fichero `schema-1.3.0.sql` tiene un
campo adicional que el fichero `schema-1.2.0.sql`. Se trata del
campo `descripcion`. En la versión anterior (`schema-1.2.0.sql`) la
tabla `equipo` se define como:

```sql
CREATE TABLE public.equipos (
    id bigint NOT NULL,
    nombre character varying(255)
);
```

Mientras que en la versión nueva (`schema-1.3.0.sql`) se define como:

```sql
CREATE TABLE public.equipos (
    id bigint NOT NULL,
    nombre character varying(255),
    descripcion character varying(255)
);
```

Si queremos migrar la base de datos de producción de una versión a
otra, debemos crear un script de migración en el que modifiquemos
únicamente el esquema de datos anterior para adaptarlo al nuevo.

En este caso el script lo llamaremos `schema-1.2.0-1.3.0.sql` y
contendrá únicamente la siguiente instrucción:

```sql
ALTER TABLE public.equipos
ADD COLUMN descripcion character varying(255)
```

Para actualizar la base de datos de producción sólo tenemos que
ejecutar el script anterior:

```
$ docker exec -it db-equipo01 bash
$ psql -U mads mads < /mi-host/schema-1.2.0-1.3.0.sql
ALTER TABLE
$ exit
```

De esta forma habremos añadido manualmente un campo en la tabla
`equipos`.

La aplicación deberá funcionar ahora perfectamente si la lanzamos en
modo producción, definiendo la variable que hemos mencionado antes con
el modo `validate`:

```
spring.jpa.hibernate.ddl-auto=validate
```

### Pasos a seguir ###

1. Creamos un issue llamado `Esquema de datos y perfil de producción` y trabajamos
   en la rama `esquema-datos` y en el pull request equivalente.
   
    ```
    $ git checkout -b esquema-datos
    $ git push -u origin esquema-datos
    ```

2. Lanzamos la aplicación en local con el modo `postgres`, trabajando
   sobre la base de datos. Previamente hemos lanzado el contenedor postgres
   montando el directorio actual en su directorio `/mi-host/`:
   
    ```
    $ docker run -d -p 5432:5432 -v ${PWD}:/mi-host --name postgres-develop -e POSTGRES_USER=mads -e POSTGRES_PASSWORD=mads -e POSTGRES_DB=mads postgres:13
    $ ./mvnw spring-boot:run -D profiles=postgres
    ```

3. Al lanzar la aplicación se habrá creado en la base de datos el
   esquema de datos. Lo generamos y lo salvamos en el directorio
   actual:
   
    ```
    $ docker exec -it postgres-develop bash
    # pg_dump -U mads -s mads > /mi-host/schema-1.2.0.sql
    # exit
    ```
   
4. Comprobamos que el esquema de datos se ha creado correctamente y lo
   movemos al directorio `sql` en el directorio raíz:
   
    ```
    $ ls -l
    Dockerfile
    README.md
    mvnw
    mvnw.cmd
    pom.xml
    schema-1.2.0.sql
    src
    target
    $ mkdir sql
    $ mv schema-1.2.0.sql sql
    ```

5. Creamos un commit con el nuevo fichero con el esquema de datos.

6. Creamos un nuevo fichero con el perfil de producción:

    **Fichero `/src/main/resources/application-postgres-prod.properties`**:
    
    ```
    POSTGRES_HOST=localhost
    POSTGRES_PORT=5432
    DB_USER=mads
    DB_PASSWD=mads
    spring.datasource.url=jdbc:postgresql://${POSTGRES_HOST}:${POSTGRES_PORT}/mads
    spring.datasource.username=${DB_USER}
    spring.datasource.password=${DB_PASSWD}
    spring.jpa.properties.hibernate.dialect = org.hibernate.dialect.PostgreSQL9Dialect
    spring.datasource.initialization-mode=never
    spring.jpa.hibernate.ddl-auto=validate
    ```
    
    Contiene exactamente la misma configuración del perfil postgres,
    excepto la propiedad `spring.jpa.hibernate.ddl-auto` que tiene el
    valor `validate`.

7. Probamos en local que el perfil funciona correctamente, lanzándolo:

    ```
    $ ./mvnw spring-boot:run -D profiles=postgres-prod
    ```

    Probamos que realmente valida el esquema de datos, en lugar de
    actualizarlo. Para ello, paramos y borramos el contenedor postgres
    y lo lanzamos de nuevo. Esto creará una base de datos vacía:
    
    ```
    $ docker container stop docker-develop
    $ docker container rm docker-develop
    $ docker run -d -p 5432:5432 -v ${PWD}:/mi-host --name postgres-develop -e POSTGRES_USER=mads -e POSTGRES_PASSWORD=mads -e POSTGRES_DB=mads postgres:13
    ```
    
    Si ahora lanzamos la aplicación en modo `postgres-prod`
    obtendremos un error:
    
    ```
    $ ./mvnw spring-boot:run -D profiles=postgres-prod
    org.springframework.beans.factory.BeanCreationException: Error
    creating bean with name 'entityManagerFactory' defined in class
    path resource  [org/springframework/boot/autoconfigure/orm/jpa/HibernateJpaConfiguration.class]: 
    Invocation of init method failed; nested exception is
    javax.persistence.PersistenceException: [PersistenceUnit: default]
    Unable to build Hibernate SessionFactory; nested exception is 
    org.hibernate.tool.schema.spi.SchemaManagementException: 
    Schema-validation: missing table [equipo_usuario]
    ```
    
8. Si queremos volver a construir la base de datos, no tenemos más que
   lanzar la aplicación con el perfile `postgres`, que tiene la
   propiedad `spring.jpa.hibernate.ddl-auto` con el valor
   `update`.

9. Hacemos un commit con el nuevo perfil, subimos los cambios y
   cerramos el pull request y el issue.

10. Nos conectamos al servidor de la asignatura y ponemos en marcha la
    base de datos de producción y hacemos una copia de seguridad tal y
    como se explica anteriormente. Dejamos el fichero en el servidor
    de la asignatura, indicando la fecha en el nombre del mismo. Por
    ejemplo `backup10112021.sql`.


## 7. Desarrollo de la nueva versión con GitFlow ##

El flujo de trabajo Git que vamos a seguir es muy similar al flujo de
trabajo GitFlow (recordad la [clase de
teoría](https://github.com/domingogallardo/apuntes-mads/blob/main/apuntes/08-git-workflows/git-workflow.md#gitflow))

### Ramas de largo recorrido ###

En GitFlow se publican las distintas versiones del proyecto en la rama
_long-lived_ `main` y se hace el desarrollo en la rama
`develop`. A partir de ahora no desarrollaremos directamente en
`main` sino en `develop`.

En la página de configuración del repositorio en GitHub en `Settings >
Branches > Default branch` se puede configurar la rama por defecto
contra la que se realizarán los commits y la que aparecerá en la
página del proyecto. Tendréis que definir `develop`.

### Ramas de feature ###

Desde el comienzo de trabajo con Git en las prácticas 2 y 3 estamos
haciendo un desarrollo basado en ramas de corto recorrido,
equivalentes a las ramas de _features_ de GitFlow. 

Tal y como se comenta en GitFLow estas ramas saldrán de `develop` y se
integrarán en `develop`. La diferencia es que en GitFlow estas ramas
se integran con la rama de desarrollo manualmente haciendo `merge`,
mientras que nosotros las integramos haciendo un pull request.

### Pasos a seguir ###

1. Cread la rama **`develop`** y configurarla como rama principal del
  proyecto en GitHub. Todos los otros miembros deberán descargarla y
  moverse a ella en sus repositorios locales. Esta rama pasará a ser
  la de desarrollo principal.

2. Cread tres _issues_ distintos, simulando tres nuevas
  funcionalidades. Deben ser issues sencillos, que no cuesten
  demasiado de implementar (mejorar algún defecto de la aplicación,
  cambiar algún elemento de alguna de las vistas, o algo
  similar). **Uno de los cambios debe afectar a alguna entidad**, por
  ejemplo añadir un campo de descripción a los equipos y actualizar
  las vistas correspondientes para permitir su inicialización y su
  actualización.

    Cada uno de los miembros del equipo será el responsable de
    uno de los issues.
  
3. Configurad el repositorio GitHub para obligar a que cualquier _pull
  request_ tenga que tener la revisión de una persona distinta del
  responsable del PR.
  
4. Desarrollad e integrar los issues en `develop` siguiendo el flujo de
  trabajo planteado anteriormente. Debéis ir actualizando el tablero
  de GitHub se actualiza correctamente.

### Rama de release ###

Hasta ahora hemos hecho los _releases_ en la rama `main`. A partir
de ahora seguiremos la estrategia de GitFlow y haremos ramas de
_release_ que salen de `develop` y se integran en `main` y en
`develop`.

Haremos también la integración haciendo pull request.

Una cosa importante que tendremos que hacer en el release es crear el
guardar el de datos de la nueva versión y crear el script de migración
de la base de datos.

### Pasos a seguir ###

Vamos a probar el lanzamiento de una release usando el flujo de
trabajo GitFlow.

1. Cread un _issue_ con la tarea _Lanzar release 1.3.0_.

2. Siguiendo las indicaciones de GitFlow, crear la rama local
   `release-1.3.0` a partir de `develop`.
   
3. En esta rama se deben realizar los cambios específicos de la
   versión. En nuestro caso:
   
    - Cambiar en la página `Acerca de` "Versión 1.3.0-SNAPSHOT" a
          "Versión 1.3.0" y añadir la fecha de publicación.
    - Cambiar el fichero `pom.xml`.
    - Generad el **esquema de datos** de la base de datos postgres
      y guardarlo en `sql/schema-1.3.0.sql`. 
    - Comparar este esquema con el esquema anterior y crear el script
      de migración con las instrucciones `ALTER TABLE` necesarias para
      actualizar la base de datos de producción de la versión 1.2.0 a
      la 1.3.0. Guardar el script en `sql/schema-1.2.0-1.3.0.sql`.
    
4. Publicad la rama `release-1.3.0` en GitHub y hacer un pull
   request sobre `main`. Una vez mezclado el PR añadir la
   etiqueta con la nueva versión `1.3.0` en `main` creando la
   página de release en GitHub.

5.  Mezclar también la rama de release con `develop` (se puede hacer
    también con un PR).

6. Subir la nueva versión de la imagen de docker a Docker Hub.

7. Una vez hecho esto ya se puede borrar la rama `release-1.3.0` y las
  ramas `main` y `develop` estarán actualizadas a la nueva
  versión. Hacer por último un commit en `develop` (no hace falta PR)
  cambiando la versión a `1.4.0-SNAPSHOT`.

8. Debemos comprobar que GitHub Actions pasa correctamente todos los
   tests de las nuevas características que se añaden.


## 8. Despliegue de la nueva versión y actualización de la BD de producción  ##

Deberéis desplegar la nueva versión de la aplicación en el servidor de
la asignatura, actualizando la base de datos de producción con los
cambios introducidos.

### Pasos a seguir ###

1. Conectarse al servidor de la asignatura.
2. Descargar la nueva versión de la aplicación.
3. Hacer una copia de seguridad de la base de datos, tal y como se
   explica en el apartado _Mantenimiento de la base de datos de
   producción_. Dejar el fichero de copia de seguridad en el
   directorio raíz del usuario `alu` con el que se está conectado al
   servidor de la asignatura.
4. Hacer una migración de la base de datos tal y como se explica en el
   mismo apartado anterior.
5. Lanzar el contenedor de la aplicación con el perfil `postgres-prod`
   y comprobar que funciona correctamente la aplicación en producción.

<!--

## 9. Nuevas funcionalidades para la aplicación  ##

Cambiamos totalmente de asunto. Tenemos ahora que dejar de pensar como
desarrolladores y pensar como **responsables del producto**. Tenemos
que pensar en las próximas funcionalidades a implementar en la
aplicación. Las desarrollaremos en las 3 semanas que durará la
práctica 4.

Deberéis reuniros y pensar en cómo hacer el producto más interesante
para los usuarios. Pensad que queréis poner la aplicación en
producción y que estáis buscando funcionalidades que la hagan
interesante para que los usuarios se suscriban a ella.

Tenéis que poneros **en el lugar de los usuarios** y pensar en
funcionalidades que les puedan ser útiles, resolver algún problema. No
es cuestión de añadir funcionalidades porque sí, sino que tenéis que
intentar hacer en 3 semanas un producto lo más coherente y útil
posible. 

Si os quedáis sin ideas, podéis mirar la aplicación
[todoist](https://todoist.com/features). Se trata de una aplicación
completa de gestión de tareas pendientes similar a la que estamos
desarrollando (aunque ellos tienen muchos más desarrolladores y
presupuesto que nosotros 😀).

El resultado será un tablero Trello con columnas denominadas _Backlog
(1)_ y _Backlog (2)_: en la que se encuentren las descripciones de las
funcionalidades candidatas a implementarse en la siguiente práctica,
ordenadas de más interesante a menos (de arriba a abajo y de izquierda
a derecha) y etiquetadas con su tamaño. La imagen de abajo es un
ejemplo, con los títulos de la mayoría de las funcionalidades borradas
para no dar demasiadas ideas.

<img src="imagenes/tablero.png" width="700px"/>

En la primera semana de la práctica 5 el profesor se reunirá con el
equipo y podrá pediros alguna aclaración sobre las propuestas y la
estimación de tamaño de las funcionalidades antes de validarlas.

### Pasos a seguir ###

- Haced una reunión, generar ideas en un _brainstorming_, organizarlas
  y estimar su dificultad. Sólo podréis definir funcionalidades de
  tamaño de uno y dos puntos. Si alguna funcionalidad es mayor,
  deberéis descomponerla en otras más pequeñas.

    Los puntos indican un tamaño relativo. Si estimáis una historia de
    usuario en 2 puntos es porque pensáis que tardaréis el doble en
    terminarla que otra de 1 punto.

    Para estimar la dificultad podéis usar _planning pocker_: se
    explica la funcionalidad y cada miembro del equipo elige un
    número: 1, 2, más de 2. Se enseñan simultáneamente y se explican
    las diferencias. Se siguen haciendo rondas hasta que hay un
    consenso.
          
- Debéis seleccionar historias que sumen entre 12 y 15 puntos para
  implementar en la siguiente práctica 5. Para los equipos de 2
  personas seleccionar entre 8 y 10 puntos. La práctica 4 tendrá una
  duración de 3 semanas.
  
    Seleccionar las historias que penséis que hacen un producto
    atractivo, coherente y útil para el usuario. Ordenar las historias
    según su valor. Para estimar el valor podéis hacer algo similar al
    _planning pocker_ pero usando los números 1, 2 y 3 como forma de
    identificar la utilidad o valor de cada historia.

- Cread un tablero Trello compartido e invitad al profesor
  (`domingo.gallardo@ua.es`). Cread las etiquetas `1` y `2` con
  distintos colores que indican el tamaño de cada funcionalidad.

- Añadir historias de usuario, ordenadas de mayor a menor importancia
  (arriba a la izquierda la más importante y abajo a la derecha la
  menos). Cada tarjeta de Trello debe contener:

    - **Título**. Aparece en la tarjeta.
    - **Descripción**. Muy breve, al estilo de las historias de
      XP. Podéis usar el estándar "Como XXX quiero XXX para XXX", o
      cualquier otro estilo. Pero siempre debe quedar claro que la
      característica debe ser una nueva funcionalidad que pueda usar o
      que note un usuario de la aplicación.
    - **Borrador de la interfaz de usuario**. Puede ser un dibujo
      hecho a mano o un mockup hecho con alguna aplicación. No hace
      falta mucho detalle, sólo para que el cliente (el profesor)
      entienda la historia.
    - **Condiciones de satisfacción**: condiciones que deben cumplirse
      para considerar que la historia está terminada. Son
      fundamentales a la hora de definir pruebas automáticas y
      manuales. Las pruebas se definen a partir de estas condiciones
      de satisfacción.
  
En la primera semana de la práctica 5 el profesor se reunirá con el
equipo y podrá pediros alguna aclaración sobre las propuestas y la
estimación de tamaño de las funcionalidades antes de validarlas.


-->

<!--


## Despliegue en producción con Docker ##


Este apartado lo realizará el **responsable de integración continua**,
pero todos los miembros del equipo deben conocer y entender todos los
pasos.


### Sobreescribir propiedades desde la línea de comando ###

Hemos visto que al lanzar la aplicación Spring Boot podemos
seleccionar el perfil activo. Por ejemplo para lanzar la aplicación
usando como perfil activo el fichero `application-mysql.properties`:

```
mvn spring-boot:run -Dspring.profiles.active=mysql
```

También hemos visto que podemos seleccionar este perfile para lanzar los tests:

```
mvn test -Dspring.profiles.active=mysql
```

La opción `-D` permite sobreescribir una propiedad del fichero de
propiedades. Por ejemplo, podemos lanzar la aplicación modificando el
usuario y la contraseña de una conexión a una base de datos con el
siguiente comando:

```
mvn spring-boot:run -Dspring.datasource.username=root -Dspring.datasource.password=12345678
```

También es posible definir variables en el propio fichero de
propiedades para proporcionar nombres más cortos o reutilizar un mismo
valor en varias propiedades.

Por ejemplo, en el siguiente fichero `application.properties`
definimos el [nivel de
logging](https://stackoverflow.com/a/37167120/540801) (que puede ser
`off`, `fatal`, `error`, `warn`, `info`, `debug`, `trace`, `all`) y
usamos el mismo nivel para los distintos paquetes de la aplicación:

```
logging=info
logging.level.org.springframework=${logging}
logging.level.root=${logging}
logging.level.org.hibernate=${logging}
logging.level.sql=${logging}
```

Podríamos entonces modificar el nivel de logs modificando la variable
`logging` al lanzar los tests de la aplicación, para que sólo muestre
los mensajes de error:

```
mvn test -Dloggin=error
```

En la aplicación vamos a usar esta variable y también otras que nos
van a permitir configurar las propiedades relacionadas con la conexión
con la base de datos.

### Pasos a seguir ###

- Abre un _issue_ denominado `Dockerización de la aplicación` en el
  que vas a configurar la aplicación para lanzarla con
  `docker-compose`. Como siempre, desarrolla el _issue_ en una rama
  propia.

- Modifica los ficheros de propiedades de ejecución para que queden de
  la siguiente forma:

    **Fichero `src/main/resources/application.properties`**

        spring.datasource.url=jdbc:h2:mem:dev
        spring.jpa.properties.hibernate.dialect = org.hibernate.dialect.H2Dialect
        spring.jpa.hibernate.ddl-auto=update
        spring.datasource.data=classpath:datos-dev.sql
        spring.datasource.initialization-mode=always
        spring.h2.console.enabled=true
        spring.h2.console.path=/h2-console


        logging=info
        logging.level.org.springframework=${logging}
        logging.level.root=${logging}
        logging.level.org.hibernate=${logging}
        logging.level.sql=${logging}

    **Fichero `src/main/resources/application-mysql.properties`**

        db_ip=localhost:3306
        db_user=root
        db_passwd=
        spring.datasource.url=jdbc:mysql://${db_ip}/mads
        spring.datasource.username=${db_user}
        spring.datasource.password=${db_passwd}
        spring.jpa.properties.hibernate.dialect = org.hibernate.dialect.MySQL5InnoDBDialect
        spring.jpa.hibernate.ddl-auto=update
        spring.datasource.initialization-mode=never

- Probamos que funcionan bien las variables de
  configuración. Para ello, lanzamos mysql en un puerto distinto, el 3316:
  
        docker run -d -p 3316:3306 --name mysql-otro-puerto -e MYSQL_ALLOW_EMPTY_PASSWORD=yes -e MYSQL_DATABASE=mads mysql:5 
  
    y probamos a lanzar la aplicación modificando la variable `db_ip`
    para que se conecte a ese nuevo puerto:
  
        mvn spring-boot:run -Dspring.profiles.active=mysql -Ddb_ip=localhost:3316

    La aplicación debe arrancar correctamente, conectándose a la base
    de datos en el nuevo puerto.

    Por último, borramos el contenendor de prueba creado:
    
         docker container stop mysql-otro-puerto
         docker container rm mysql-otro-puerto

- Realiza un commit con los nuevos ficheros de propiedades.

!!! Note "Nota"
    Es posible utilizar la variable `db_ip` para facilitar la conexión
    de la aplicación a un contenedor Docker de MySQL lanzado en
    Windows con _Docker Toolbox_. En este caso hay que especificar la
    dirección IP en la que se está ejecutando el contenedor Docker.


### Imagen Docker de la aplicación ###

Hemos visto [en teoría](https://github.com/domingogallardo/apuntes-mads/blob/master/sesiones/08-integracion-entrega-continua/integracion-entrega-continua.md#demostración-de-docker) cómo crear imágenes Docker. Vamos a crear una
imagen con nuestra aplicación `mads-todolist`.

El fichero `Dockerfile` es el responsable de construir la máquina
Docker. Usaremos el siguiente `Dockerfile`:

```
#### Stage 1: Build the application
FROM openjdk:8-jdk-alpine as build
    
# Set the current working directory inside the image
WORKDIR /app

# Copy maven executable to the image
COPY mvnw .
COPY .mvn .mvn

# Copy the pom.xml file
COPY pom.xml .

# Build all the dependencies in preparation to go offline.
# This is a separate step so the dependencies will be cached unless
# the pom.xml file has changed.
RUN ./mvnw dependency:go-offline -B

# Copy the project source
COPY src src

# Package the application
RUN ./mvnw package -DskipTests
RUN mkdir -p target/dependency && (cd target/dependency; jar -xf ../*.jar)

#### Stage 2: A minimal docker image with command to run the app
FROM openjdk:8-jre-alpine

# Copy project dependencies from the build stage
COPY --from=build /app/target/dependency/BOOT-INF/lib /app/lib
COPY --from=build /app/target/dependency/META-INF /app/META-INF
COPY --from=build /app/target/dependency/BOOT-INF/classes /app

# Define environment variables
ENV PROFILE=
ENV DB_IP=
ENV DB_USER=
ENV DB_PASSWD=
ENV LOGGING=

CMD java -Dspring.profiles.active=$PROFILE -Ddb_ip=$DB_IP -Ddb_user=$DB_USER \
    -Ddb_passwd=$DB_PASSWD -Dlogging=$LOGGING -cp app:app/lib/* madstodolist.Application
```


Se trata de un fichero que construye la imagen docker en dos fases. En
una primera fase compila la aplicación y guarda todos los `jars` en el
directorio `target`. En la segunda fase crea la máquina resultante, basada en
`openjdk:8-jre-alpine`, con las librerías compiladas previamente.

Docker permite definir variables de entorno que pueden ser modificadas
al lanzar la máquina. Definimos las mismas variables que hemos
definido en el fichero de propiedades de spring boot:

- `PROFILE`: perfil a usar al lanzar la aplicación.
- `DB_IP`: dirección IP y puerto de la base de datos con la que se
  debe conectar la aplicación.
- `DB_USER`: usuario de la base de datos con el que la aplicación se
  conecta con la base de datos.
- `DB_PASSWD`: contraseña del usuario de la base de datos.
- `LOGGING`: nivel de logging que va a realizar la aplicación.

Para lanzar una imagen docker definiendo un valor de una variable de
entorno hay que utilizar el flag `-e VARIABLE=valor`. 


### Pasos a seguir ###

- Crea una cuenta en [DockerHub](https://hub.docker.com). En esta
  cuenta se publicará la imagen docker de la aplicación.

- Crea el fichero `Dockerfile` anterior en el directorio principal de
  la aplicación.
  
- Construye la máquina docker. Utiliza como _usuario_ el usuario que
  has creado en DockerHub.

        docker build -t USUARIO/mads-todolist-equipo-XX .

    Prueba a ejecutar la aplicación trabajando con la base de datos en
    memoria y con logs de nivel `INFO`:
    
        docker run --rm -it -p 8080:8080 -e LOGGING=error USUARIO/mads-todolist-equipo-XX

    El flag `-it` permite visualizar en el terminal de forma
    interactiva la salida estándar de la aplicación Play y terminarla
    haciendo un `CTRL-C`.

    Y prueba por último a ejecutar la aplicación funcionando con la imagen docker
    con la base de datos MySQL:

        $ docker run -d -p 3306:3306 --name mysql-develop -e MYSQL_ALLOW_EMPTY_PASSWORD=yes -e MYSQL_DATABASE=mads mysql:5 
        $ docker run --rm -it --link mysql-develop -p 8080:8080 \
          -e PROFILE=mysql -e DB_IP=mysql-develop:3306 -e DB_USER=root -e LOGGING=info \
          USUARIO/mads-todolist-equipo-XX


- Cuando compruebes que todo funciona correctamente, sube a _docker hub_
  la imagen compilada:
  
        $ docker login
        # introduce tus credenciales en docker hub
        $ docker push USUARIO/mads-todolist-equipo-XX
      
- Comprueba en _docker hub_ que la imagen se ha subido
  correctamente. Uno de los compañeros debe probar que la imagen
  funciona correctamente, ejecutando las dos instrucciones
  anteriores en su máquina:

        $ docker run -d -p 3306:3306 --name mysql-develop -e MYSQL_ALLOW_EMPTY_PASSWORD=yes -e MYSQL_DATABASE=mads mysql:5 
        $ docker run --rm -it --link mysql-develop -p 8080:8080 \
          -e PROFILE=mysql -e DB_IP=mysql-develop:3306 -e DB_USER=root -e LOGGING=info \
          USUARIO/mads-todolist-equipo-XX
  
    Comprobad que se descarga correctamente la máquina
    `USUARIO/mads-todolist-equipo-XX` y que la aplicación se lanza sin
    errores.

- Por último, modifica el script de Travis para que sea Travis quien
  construya y publique la máquina docker. Antes de que se ejecute el
  script deberás configurar en los ajustes del repositorio en Travis
  (_travis-ci.com > USUARIO/mads-todolist-equipo-XX > Settings >
  Environment Variables_) las variables: `DOCKER_USERNAME` y
  `DOCKER_PASSWORD`, para que Travis pueda publicar en tu cuenta de
  DockerHub.
  
    <img src="imagenes/variables-entorno-travis.png" width="700px"/>
  
    Líneas a añadir al final del fichero `.travis.yml`:
    
        after_success:
          - docker build -t USUARIO/mads-todolist-equipo-XX:$TRAVIS_BUILD_NUMBER .
          - if [ "$TRAVIS_EVENT_TYPE" != "pull_request" ]; then
            docker login -u="$DOCKER_USERNAME" -p="$DOCKER_PASSWORD";
            docker push USUARIO/mads-todolist-equipo-XX:$TRAVIS_BUILD_NUMBER;
            docker tag USUARIO/mads-todolist-equipo-XX:$TRAVIS_BUILD_NUMBER USUARIO/mads-todolist-equipo-XX:latest;
            docker push USUARIO/mads-todolist-equipo-XX:latest;
            fi

    Fíjate en el script `after_success`. Es lo que Travis hará después
    de ejecutar con éxito los tests:
    
    - Construir la máquina docker de nuestra aplicación, asignándole
    como etiqueta el número de build actuar.
    - Si la ejecución de Travis es debida a un evento que no es un
    _pull request_ (o sea, cuando sea un build disparado por el commit
    de merge con la rama en la que se integra el PR) se logea en
    docker hub con el usuario y la contraseña definidas en las
    variables. Una vez logeado, publica la imagen usando como número
    de _tag_ el número de build. Y esta última imagen también se
    vuelve a etiquetar como `latest` y se vuelve a subir.
  
    Por ejemplo, cuando se realice el build `#28` se publicará la
    imagen resultante de este build con las etiquetas `28` y `latest`:
    `USUARIO/mads-todolist-equipo-XX:28` y
    `USUARIO/mads-todolist-equipo-XX:latest`.


- Por último, añade el siguiente fichero `docker-compose.yml` en el
  directorio raíz de la aplicación. La aplicación `docker-compose`
  permite automatizar la puesta en funcionamiento y conexión de más de
  un contenedor docker. En nuestro caso, servirá para poner en marcha
  con un único comando el contenedor de base de datos y nuestra
  aplicación.

    Fichero `docker-compose.yml`:
        
        version: '3.7'

        # Define services
        services:

          # App backend service
          mads-todolist:
            image: USUARIO/mads-todolist-equipo-XX
            ports:
              - "8080:8080" # Forward the exposed port 8080 on the container to port 8080 on the host machine
            restart: always
            depends_on:
              - db # This service depends on mysql. Start that first.
            environment: # Pass environment variables to the service
              PROFILE: mysql
              DB_IP: db:3306
              DB_USER: root
              LOGGING: info
            networks: # Networks to join (Services on the same network can communicate with each other using their name)
              - backend

          # Database Service (Mysql)
          db:
            image: mysql:5
            ports:
              - "3306:3306"
            restart: always
            environment:
              MYSQL_DATABASE: mads
              MYSQL_ALLOW_EMPTY_PASSWORD: 'yes'
            volumes:
              - db-data:/var/lib/mysql
            networks:
              - backend

        # Volumes
        volumes:
          db-data:

        # Networks to be created to facilitate communication between containers
        networks:
          backend:
  
  - Prueba que funciona correctamente `docker-compose` ejecutando el
    comando `docker-compose up`. Para asegurarte de que la imagen que
    ejecutas es la que se descarga de docker hub debes borrar
    previamente la imagen que tengas en tu ordendador:
    
    ```
    $ docker container prune
    $ docker image rm USUARIO/mads-todolist-equipo-XX
    $ docker-compose up
    ```
    
    Verás cómo se ponen en marcha el contenedor `mysql` y el
    contenedor con nuestra aplicación. Prueba a conectarte a la
    aplicación y comprobar que todo funciona correctamente.
    Puedes terminar la ejecución
    haciendo `CTRL-C` o lanzando desde otra terminal el comando
    
    ```
    docker-compose down
    ```

  - En el script de `docker-compose` el contenedor `mysql` utiliza un
    [volumen](https://docs.docker.com/storage/volumes/). Esto permite
    conservar los datos que se introduzcan en la ejecución del
    programa, aunque el contenedor se borre. También sería posible
    hacer un backup de estos datos a partir del volumen.
    
    Para listar los volúmenes mantenidos por docker:
    
    ```
    docker volume ls
    ```
    
    Para eliminar un volumen:
    
    ```
    docker volume rm nombre-volumen
    ```
    
    Y para elminar todos los volúmenes:
    
    ```
    docker volume prune
    ```

- Haz un commit y sube los cambios a GitHub. 
- Crea el pull request que cierra el _issue_ y ciérralo, comprobando
  que Travis construye la máquina docker y la publica en docker hub.

    <img src="imagenes/imagenes-docker-hub.png" width="700px"/>

- Por último un compañero debe probar el comando `docker-compose up` y
  comprobar si se ponen en marcha las imágenes docker y nuestra
  aplicación funciona correctamente. 

-->


## 9. Documentación, entrega y evaluación ##

Deberéis añadir una página de documentación `/doc/practica4.md` en la
que deberéis incluir:

- Breve documentación técnica de los cambios introducidos en la
  aplicación.
- Detalles del despliegue de producción: usuario `alu` con el que se
  ha realizado la puesta en producción, así como directorio y fichero
  en el que se encuentra (en el servidor de la asignatura) el backup
  de la base de datos de producción. Script de migración de la base de
  datos.
  

- La práctica tiene una duración de 2 semanas y debe estar terminada
  el martes 23 de noviembre.
- La calificación de la práctica tiene un peso de un 15% en la nota
  final de prácticas.
- 
- Para realizar la entrega uno de los miembros del equipo debe subir a
  Moodle un ZIP que contenga todo el proyecto, incluyendo el
  directorio `.git` que contiene la historia Git. Para ello comprime
  tu directorio local del proyecto después de haber hecho un `mvn
  clean` para eliminar el directorio `target` que contiene los
  binarios compilados.

Para la evaluación se tendrá en cuenta:

- Desarrollo continuo (los _commits_ deben realizarse a lo largo de
  las semanas y no dejar todo para la última).
- Correcto desarrollo de la metodología.
- Diseño e implementación del código y de los tests de las
  características desarrolladas.
- Documentación.

