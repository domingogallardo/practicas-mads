# Práctica 5: Sprint final

## Objetivos y resumen de la práctica

En esta práctica seguiremos trabajando con los mismos equipos y
proyecto que en la práctica 4.

Durante las semanas de la práctica el equipo realizará una iteración
para desarrollar un sprint completo de Scrum con el que obtener un
incremento de la aplicación `TodoList`. Usaremos el mismo flujo de
trabajo de la práctica 4 para desarrollar sobre la rama `develop`:

- Una tarjeta en el tablero de Trello para cada historia de
  usuario. Cada historia de usuario continuará la numeración que
  comenzamos en la práctica 3. 
- La historia de usuario se puede descomponer en mas de un issue en
  GitHub o hacerla en un único issue si es corta. En cualquier caso,
  se deberán etiquetar los issues con la etiqueta asociada a la
  historia de usuario.
- Cada issue se resuelve en una rama y se integra en `develop` con un
  pull request.
- En el tablero en GitHub se representan el estado de los issues.
- El repositorio está conectado a GitHub Actions para hacer la integración
  continua. Se comprueban de forma automática los tests en las
  integraciones de los pull requests en `develop`.

Al final de la práctica se lanzará una nueva versión (`1.4.0`), usando
el mismo flujo de trabajo que en la práctica anterior, y se presentará
la aplicación resultante en una demostración en clase.

## Nuevas funcionalidades para la aplicación  ##

Tenemos que diseñar, como **responsables del producto** (_Product
Owners_), las próximas funcionalidades a implementar en la
aplicación. Las refinaremos y desarrollaremos durante el resto de la práctica.

Deberéis reuniros y pensar en cómo hacer el producto más interesante
para los usuarios. Pensad que queréis poner la aplicación en
producción y que estáis buscando funcionalidades que la hagan
interesante para que los usuarios se suscriban a ella.

Podéis coger ideas del [tablero
Trello](https://trello.com/b/Q35xhgzo/todolist-mads) resultante de
ideas de cursos pasados y también de una aplicación web muy completa
que hace algo similar a lo que estamos construyendo nosotros:
[todoist](https://todoist.com/features) (mirad, por ejemplo, el
[vídeo](https://youtu.be/8ZKq0r-g87M) explicando sus funcionalidades
más importantes).

Tenéis que poneros **en el lugar de los usuarios** y pensar en
funcionalidades que les puedan ser útiles, resolver algún problema. No
es cuestión de añadir funcionalidades porque sí, sino que tenéis que
intentar hacer en pocas semanas un producto lo más coherente y útil
posible. 

El resultado será un tablero Trello con columnas denominadas _Backlog
(1)_ y _Backlog (2)_: en la que se encuentren las descripciones de las
funcionalidades candidatas a implementarse en la siguiente práctica,
ordenadas de más interesante a menos (de arriba a abajo y de izquierda
a derecha) y etiquetadas con su tamaño. La imagen de abajo es un
ejemplo, con los títulos de la mayoría de las funcionalidades borradas
para no dar demasiadas ideas.

<img src="imagenes/tablero.png" width="700px"/>

El profesor podrá pediros alguna aclaración sobre las funcionalidades
propuestas y la estimación de tamaño de las funcionalidades. También
se valorará el alcance de las funcionalidades escogidas en la
presentación final de la práctica, en donde se dará una puntuación extra
a los proyectos en base a las funcionalidades implementadas, su
coherencia y usabilidad. 

### Pasos a seguir ###

- Haced una reunión en la que reviséis el [tablero
Trelllo](https://trello.com/b/Q35xhgzo/todolist-mads) con ejemplos de
funcionalidades de cursos pasados y la aplicación web
[todoist](https://todoist.com/features). Usad esas funcionalidades como ejemplo,
podéis proponer vosotros nuevas funcionalidades. Debéis definir las que
vais a incorporar a vuestra aplicación y estimar su dificultad. Tenéis que pensar en
funcionalidades que puedan ser útiles y, sobre todo, definir un producto
coherente, fácil de usar y que puede representar un _mínimo producto viable_.

    En cuanto a la estimación de la dificultad o tamaño de la funcionalidad,
    sólo podréis definir funcionalidades de tamaño de 1 y 2 puntos. Si alguna
    funcionalidad es mayor, deberéis descomponerla en otras más pequeñas. 

    Los puntos indican un tamaño relativo. Si estimáis una historia de
    usuario en 2 puntos es porque pensáis que tardaréis el doble en
    terminarla que otra de 1 punto.

    Para estimar el tamaño podéis usar _planning pocker_: se
    explica la funcionalidad y cada miembro del equipo elige un
    número: 1, 2, más de 2. Se enseñan simultáneamente y se explican
    las diferencias. El hecho de que haya diferencias normalmente se
    debe a que existe disparidad en los detalles de la implementación
    o del alcance de la funcionalidad. Se ponen en común las
    diferencias, se llegan a acuerdos y se vuelve a hacer otra ronda
    de _planning pocker_. Se siguen haciendo rondas hasta que hay un
    consenso.
          
- Debéis seleccionar historias que sumen entre 12 y 15 puntos para
  implementar en la práctica. Para los equipos de 2 personas
  seleccionar entre 8 y 10 puntos. La práctica tendrá una duración de
  4 semanas, por lo que cada miembro del equipo deberá implementar
  alrededor de 1 punto por semana.
  
    Seleccionad las historias que penséis que hacen un producto
    atractivo, coherente y útil para el usuario. Ordenad las historias
    según su valor. Para estimar el valor podéis hacer algo similar al
    _planning pocker_ pero usando los números 1 y 2 como forma de
    identificar la utilidad o valor de cada historia.

- Cread un tablero Trello y poned un enlace a él en el README del
  repositorio. Cread las etiquetas `1` y `2` con distintos colores que
  indican el tamaño de cada funcionalidad.

- Añadid historias de usuario, ordenadas de mayor a menor importancia
  (arriba a la izquierda la más importante y abajo a la derecha la
  menos). Cada tarjeta de Trello debe contener:

    - **Título**. Aparece en la tarjeta.
    - **Descripción**. Muy breve, al estilo de las historias de
      XP. Podéis usar el estándar "Como XXX quiero XXX para XXX", o
      cualquier otro estilo. Pero siempre debe quedar claro que la
      característica debe ser una nueva funcionalidad que pueda usar o
      que note un usuario de la aplicación.
    - **Detalles**. Detalles que consideréis importantes anotar y que
      explican más el alcance de la historia.
    - **Condiciones de satisfacción**. Condiciones que deben cumplirse
      para considerar que la historia está terminada. Son
      fundamentales a la hora de definir pruebas automáticas y
      manuales. Las pruebas se definen a partir de estas condiciones
      de satisfacción.
  
El profesor podrá pediros alguna aclaración sobre las propuestas y la
estimación de tamaño de las funcionalidades.

## Artefactos del sprint ##

El equipo utilizará un tablero Trello para documentar el backlog del
producto y el tablero de GitHub para el backlog del sprint.

### Tablero Trello ###

El tablero Trello contendrá el **backlog del producto** y servirá para
trabajar con estas historias de usuario en formato de tarjeta,
escribirlas rápidamente, estimarlas y ordenarlas.

Cada tarjeta Trello contendrá lo que ya habéis hecho anteriormente:

- Título de la historia de usuario
- Descripción 
- Detalles
- Estimación del tamaño de la historia (definido con una etiqueta)

Utilizaremos un tablero en formato Kanban, definiendo cinco columnas
que representarán las fases por las que pasará cada historia de
usuario: `Backlog`, `Seleccionadas`, `En marcha`, `En prueba` y `Terminadas`.

|Tipo de columna | Características de las historias                                                                 |
|----------------|--------------------------------------------------------------------------------------------------|
| **Backlog**    | Estimado el tamaño de la historia y pendiente de elaborar detalles.                              |
| **Seleccionadas**  | Se están elaborando todos los detalles de la historia (página Google Docs).                         |
| **En marcha**  | Se ha abierto el primer _issue_ en GitHub y el equipo ha comenzado a desarrollar la historia.    |
| **En prueba**  | La historia está completamente integrada en `develop` (todos sus PR se han mezclado en la rama). En la tarjeta se debe añadir un enlace al commit en la rama `develop` en el que podamos compilar la aplicación y probar completamente todas las condiciones de satisfacción la historia. |
| **Terminadas** | Se han comprobado las condiciones de satisfacción de la historia.         |


### Pasos a seguir ###

Durante el desarrollo del sprint, se deberá añadir en el tablero Trello:

- Responsable de la historia de usuario: miembro del equipo que
  liderará el desarrollo de la historia. Puede que más de una persona
  intervenga en el desarrollo de la historia, pero una persona será la
  responsable. Se debe añadir en la ficha de la historia de usuario,
  en forma de etiqueta.
  
    Todos los miembros del equipo deberán
    realizar un trabajo equitativo, y se repartirán las historias de
    forma que queden también equilibrados los tamaños totales de las
    historias asignadas a cada uno.

- **Antes de comenzar el desarrollo de una historia** su responsable
  crearáa una **página Google Docs** de acceso público en la copiará,
  y ampliará y/o modificará sus detalles. La descripción en Trello hay
  que dejarla tal cual, sin modificar. En la página de Google Docs, el
  responsable de la historia de usuario deberá incluir, **cuando la
  seleccione**, los siguientes ítems:
    - Título de historia de usuario
    - Descripción y detalles
    - Borrador del aspecto de la interfaz de usuario resultante. No es
      necesario que sea muy detallado ni que se use ninguna
      herramienta de mockups, se puede hacer escaneando un dibujo
      hecho a mano.
    - Condiciones de satisfacción (COS). Estas condiciones de
      satisfacción son esenciales a la hora de determinar el alcance
      de la historia y de darla por acabada. Deben estar lo
      suficientemente claras como para poder elaborar a partir de
      ellas las **pruebas manuales** de la historia de usuario.

    !!! Danger "Importante"
        Los detalles de la historia de usuario en Google Docs se
        escribirán **sólo cuando la historia haya sido seleccionada** y esté
        en la columna `Seleccionadas`. Es recomendable que el paso de una
        historia a seleccionada se haga cuando se haya terminado la
        historia anterior con la que se estaba trabajando. De esta forma, cuando escribamos los detalles de la
        siguiente historia seleccionada ya tendremos el proyecto más
        avanzado y podremos elaborar mejor los detalles de la nueva
        historia. 
    
    Es posible cambiar cosas en la página de Google Docs con respecto a la descripción
    de la tarjeta en Trello. Dejad la descripción sin modificar, para
    tener una referencia de la evolución del diseño del proyecto.

- Una vez creado el documento Google de la historia de usuario ya se
puede comenzar a realizar la implementación de la misma abriendo el o
los issues en GitHub y añadiendo al mismo el responsable de su
desarrollo.

    !!! Danger "Importante"
        Aunque parezca evidente, lo resalto: hay que pasar las fases de
        forma ordenada. No podemos empezar a desarrollar una historia de
        usuario antes de haber terminado todos sus detalles en la página
        de Google Docs.

- Se debe documentar la evolución del tablero realizando 4 capturas de
pantalla y registrando la fecha de cada una.


### Tablero GitHub ###

El tablero GitHub contendrá el **backlog del sprint** en el que se
visualizarán los _issues_ con los trabajos que está realizando el
equipo de desarrollo. 

En los issues podremos tener:

- Desarrollo de historias de usuario (en parte o completas)
- Bugs y refactorizaciones
- Desarrollos técnicos necesarios no relacionados con una historia de
  usuario en concreto

Usaremos las etiquetas para definir el tipo de issue:

- Código de historia de usuario
- Bug
- Refactorización
- Mejora técnica

Los primeros tipos de issue serán obligatorios y los tres siguientes
serán opcionales, dependiendo de si el proyecto lo requiere.

En cuanto a las columnas, definiremos el tablero como un tablero
Kanban. Usaremos las mismas columnas que hasta ahora, con los
issues_ moviéndose por ellas según se vayan
desarrollando.

| Tipo de columna    | Características de los issues |
|--------------------|-------------------------------|
| **Sprint backlog** | Issues esperando a ser desarrollados. |
| **In progress**    | El issue tiene asignado un responsable y se ha abierto una rama para su desarrollo. |
| **In pull request**| El issue tiene un pull request abierto. |
| **Done**           | El pull request que se ha resuelto y el issue está integrado en `develop`.|

Al igual que el tablero de Trello, se debe documentar la evolución del
tablero de issues realizando 4 capturas de pantalla y registrando la
fecha de cada una.


## Desarrollo del sprint

Se deberán realizar los siguientes eventos, tomando nota y redactando
un informe con la fecha de la reunión, su duración y su desarrollo:

1. 2 sesiones de _pair programming_ con turnos de 20 minutos (en cada
   sesión se deben hacer 4 turnos). Se podrán hacer estas sesiones en
   clase de prácticas.
2. Retrospectiva del sprint: análisis de qué cosas han funcionado
   regular y hay que mejorar y qué cosas han funcionado bien durante
   el sprint.

### Desarrollo de issues e historias ###

- Cada miembro del equipo selecciona el issue a desarrollar. Lo normal
  es que cada miembro desarrolle un único issue de forma concurrente,
  aunque podría darse el caso de ser más (por ejemplo, si algún issue
  no puede terminarse por estar bloqueado por otro).

- Se deben crear ramas para los issues y pull requests con revisión de
  código para integrar los pull requests en `develop`. Es suficiente con
  que haya una única aprobación para integrar el pull request.

- Seguimos usando GitHub Actions  para la integración continua.

- Como hemos hecho hasta ahora, cada issue debe contener **tests
  automáticos** que prueben los cambios.
  
- Una vez terminados todos los issues de una historia de usuario, el
  responsable de la historia moverá su tarjeta en el tablero Trello a
  `En prueba`, se añadirá en la tarjeta el enlace al commit de develop
  en el que se ha realizado la integración y otro miembro del equipo
  realizará las **pruebas manuales** especificadas en sus COS
  **utilizando la base de datos Postgres**. Cuando se hayan superado
  todas las pruebas se pasará la historia a `Terminada`. Si se
  detectara algún fallo, se volverá la historia a `En marcha` y se
  abrirá un issue de tipo `bug` para resolver el problema.

### Publicación de nueva versión y migración de la base de datos  ###

Al final del desarrollo se deberá lanzar una nueva release (1.4.0) en
la rama `main` usando los mismos pasos que en la práctica anterior. Se
debe obtener el esquema de datos de la nueva versión y crear el script
de migración de la base de datos de producción.

Como se hizo en la práctica anterior, se debe hacer una copia de
seguridad de algunos datos en producción **antes** de actualizar la
base de datos, aplicar el script de migración a la base de datos de
producción, comprobar que la aplicación funciona correctamente con las
nuevas funcionalidades añadiendo algunos nuevos datos y hacer otra
copia de seguridad de los datos **después** de probar la aplicación y
añadir los nuevos datos.

Como en la práctica anterior, ambas copias de seguridad se deben
incluir en el directorio `sql` del repositorio.

### Documentación del desarrollo ###

- Documentar las sesiones de _pair programming_.
- Documentar la evolución de los tableros Trello y GitHub capturando 4
  instantáneas y registrando su fecha.

## Entrega y evaluación

La práctica tiene una duración de 4 semanas (por motivos de calendario se ha
modificado a 3 semanas)

- Se realizará una **revisión del sprint** de 15 minutos en las
  **clases de prácticas y teoría del 20 de diciembre**. La revisión
  constará de:
    - Presentación con diapositivas en la que se explicará la
      **metodología seguida** en el sprint, las **nuevas
      funcionalidades** introducidas y la puesta en producción de la
      nueva versión.
    - Demostración de las nuevas funcionalidades utilizando la última
      versión puesta en producción.

    !!! Danger "El proyecto debe estar terminado el 20 de diciembre"
        En la fecha de la presentación debe estar completo el nuevo
        release 1.4.0 del proyecto y debe estar puesto en
        producción. Después de la presentación **no podréis añadir más
        código** al proyecto. El tiempo restante hasta el 25 de enero
        es para que terminéis la documentación.

- En la fecha límite del **25 de enero** (podéis entregarlo antes) deberá
  terminarse la documentación y tener disponible:
    - Directorio `doc` en el repositorio del proyecto en el que se
      incluirá la documentación de la práctica y un PDF con las diapositivas
      presentadas en la demo.
      
      En la documentación de la práctica debéis incluir un PDF con todo el
      **Sprint Backlog**: las historias de usuario escogidas para el sprint, su
      descripción, condiciones de satisfacción y el borrador inicial de interfaz 
      de usuario tal y como aparecen en los documentos subidos a GoogleDocs.
          
      Además del backlog, debéis documentar en el PDF anterior, o en un fichero
      markdown:
      
      - **Funcionalidades implementadas**: breve descripción para el
          usuario y breve descripción técnica.
      - **Puesta en producción**: script de migración de la base de
          datos y breve informe de la puesta en producción.
      - **Informe sobre la evolución del desarrollo**: instantáneas
          de los tableros y alguna métrica o gráfica sobre el desarrollo
          (número de pull requests cada semana, por ejemplo).
      - **Informe sobre las sesiones de pair programming**: breve informe de
          cada sesión de pair programming explicando cómo se ha desarrollado la
          sesión y vuestra impresión personal de la práctica de pair programming
          después de haberla probado.
      - **Resultado de la retrospectiva**: qué ha ido bien en el
          sprint y qué se podría mejorar en el siguiente sprint.
          
    - El repositorio GitHub deberá incluir el tablero con el backlog
      del sprint con los issues completados.
    - El tablero de Trello deberá incluir el backlog del producto con
      las historias de usuario que se debían implementar en el sprint
      y los enlaces a los documentos Google Docs con sus detalles.
    - Entrega en Moodle la última versión del proyecto subida a
      GitHub.

La calificación de la práctica tiene un peso de un 25% en la nota
final de prácticas (1 punto en la nota final).

La evaluación se basará en: 

- Desarrollo continuo de los issues
- Complejidad de las funcionalidades añadidas
- Corrección del código
- Correcto funcionamiento
- Informe de la práctica
- Si el trabajo de algún miembro del equipo es significativamente de
  menor calidad y/o cantidad que el del resto, se penalizará su
  calificación

<!-- A la nota anterior se le sumará una **puntación extra de hasta 0,5
puntos** en la nota final que se basará en la demostración realizada,
las funcionalidades implementadas, su coherencia y usabilidad. 

Al final de la sesión de presentaciones se publicará esta puntuación
extra, que se sumará directamente a la nota final de la asignatura de
todos los miembros de los equipos.
-->
