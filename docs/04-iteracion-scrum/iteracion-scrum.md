# Práctica 4: Sprint 

## Objetivos y resumen de la práctica

En esta práctica seguiremos trabajando con los mismos equipos y
proyecto que en la práctica 3.

Durante las 3 semanas de la práctica el equipo realizará una iteración
para desarrollar un incremento de la aplicación
`TodoList`. Usaremos el mismo flujo de trabajo de la práctica 3 para
desarrollar sobre la rama `develop`:

- Una tarjeta en el tablero de Trello para cada historia de
  usuario. Cada historia de usuario continuará la numeración que
  comenzamos en la práctica 2. 
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
el mismo flujo de trabajo que en la práctica anterior.

## Artefactos del sprint ##

El equipo utilizará un tablero Trello para documentar el backlog del
producto y el tablero de GitHub para el backlog del sprint.

### Tablero Trello ###

El tablero Trello contendrá el **backlog del producto** y servirá para
trabajar con estas historias de usuario en formato de tarjeta,
escribirlas rápidamente, estimarlas y ordenarlas.

Cada tarjeta Trello contendrá lo que ya habéis hecho para la práctica 3:

- Título de la historia de usuario
- Descripción 
- Estimación del tamaño de la historia (definido con una etiqueta)
  
Y se deberá añadir

- Responsable de la historia de usuario (otra etiqueta) : miembro del
  equipo que liderará el desarrollo de la historia. Puede que más de
  una persona intervenga en el desarrollo de la historia, pero una
  persona será la responsable.
- Enlace a una **página Google Docs** con los **detalles de la historia de
  usuario** realizada por el responsable de la historia de usuario en
  la que se ampliarán los detalles de la historia. La descripción en
  Trello hay que dejarla tal cual, sin modificar.
    - Título de historia de usuario
    - Descripción y detalles
    - Borrador del aspecto de la interfaz de usuario resultante
    - Condiciones de satisfacción (COS). Estas condiciones de
      satisfacción son esenciales a la hora de determinar el alcance
      de la historia y de darla por acabada. Deben estar lo
      suficientemente claras como para poder elaborar a partir de
      ellas las **pruebas manuales** de la historia de usuario.

!!! Important "Importante"
    Los detalles de la historia de usuario en Google Docs se
    escribirán sólo cuando la historia haya sido seleccionada y esté
    en la columna `Seleccionadas`. Es recomendable que el paso de una
    historia a seleccionada se haga cuando se haya terminado la
    anterior. De esta forma, cuando escribamos los detalles de la
    siguiente historia seleccionada ya tendremos el proyecto más
    avanzado y podremos elaborar mejor los detalles de la nueva
    historia. 
    
    Es posible cambiar cosas en la página de Google Docs con respecto a la descripción
    de la tarjeta en Trello. Dejad la descripción sin modificar, para
    tener una referencia de la evolución del diseño del proyecto.


Utilizaremos un tablero en formato Kanban, definiendo cinco columnas
que representarán las fases por las que pasará cada historia de
usuario: `Backlog`, `Seleccionadas`, `En marcha`, `En prueba` y `Terminadas`.

|Tipo de columna | Características de las historias                                                                 |
|----------------|--------------------------------------------------------------------------------------------------|
| **Backlog**    | Estimado el tamaño de la historia y pendiente de elaborar detalles.                              |
| **Seleccionadas**  | Se están elaborando todos los detalles de la historia (página Google Docs).                         |
| **En marcha**  | Se ha abierto el primer _issue_ en GitHub y el equipo ha comenzado a desarrollar la historia.    |
| **En prueba**  | La historia completa está integrada en `develop`. En la tarjeta se debe añadir un enlace al commit. |
| **Terminadas** | Se han comprobado las condiciones de satisfacción de la historia.         |

Se debe documentar la evolución del tablero realizando 4 capturas de
pantalla y registrando la fecha de cada una.

!!! Important "Importante"
    Aunque parezca evidente, lo resalto: hay que pasar las fases de
    forma ordenada. No podemos empezar a desarrollar una historia de
    usuario antes de haber terminado todos sus detalles en la página
    de Google Docs.

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
- Refactor
- Mejora técnica

Los primeros tipos de issue serán obligatorios y los tres siguientes
serán opcionales, dependiendo de si el proyecto lo requiere.

En cuanto a las columnas, definiremos el tablero como un tablero
Kanban. Usaremos las mismas columnas que hasta ahora, con los
issues/_pull requests_ moviéndose por ellas según se vayan
desarrollando.

| Tipo de columna    | Características de los issues |
|--------------------|-------------------------------|
| **Sprint backlog** | Issues esperando a ser desarrollados. |
| **In progress**    | El issue tiene asignado un responsable y se ha abierto una rama para su desarrollo. |
| **In pull request**| El issue tiene un pull request abierto (se archivará la tarjeta del issue y se dejará sólo la tarjeta del pull request).|
| **Done**           | El pull request que se ha resuelto y el issue está integrado en `develop`.|

Al igual que el tablero de Trello, se debe documentar la evolución del
tabler de issues realizando 4 capturas de pantalla y registrando la
fecha de cada una.


## Reunión de revisión del backlog ##

Al comienzo de la práctica el equipo habrá definido un backlog formado
por historias de usuario con tamaños de 1 y 2 puntos. Los puntos
indican un tamaño relativo. Si una historia se estima en 2 puntos es
porque se piensa que se tardará el doble en terminarla que otra de 1
punto.

La puntación total de las historias a desarrollar será entre 12 y 15
puntos (entre 4 y 5 puntos por persona).

Las historias deben consistir en nuevas funcionalidades que construyan
un producto atractivo, coherente y útil para el usuario. Estarán
ordenadas por importancia en la columna de backlog.

En la primera semana de la esta práctica el profesor se reunirá con el
equipo y podrá pediros alguna aclaración sobre las propuestas y la
estimación de tamaño de las funcionalidades antes de validarlas.

El profesor añadirá una nota en el tablero Trello con el resultado de
esta validación, pudiendo realizar alguna aclaración sobre el alcance
de las historias de usuario.

## Responsables de historia de usuario ##

Una vez realizada la validación los miembros del equipo elegirán
responsables para cada historia, se creará su página Google Docs, y se
detallará allí las condiciones de satisfacción y el borrador de la
interfaz de usuario definitivas. No debéis borrar lo escrito en la
tarjeta de Trello. Utilizad el documento Google Docs para ampliar o
detallar más aquellos elementos que consideréis oportuno.

Una vez creado el documento Google de la historia de usuario ya se
puede comenzar a realizar la implementación de la misma abriendo el o
los issues en GitHuab y añadiendo al mismo el responsable de su
desarrollo.

Todos los miembros del equipo deberán realizar un trabajo equitativo,
y se repartirán las historias de forma que queden también equilibrados
los tamaños totales de las historias asignadas a cada uno.

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
  código para integrar los pull requests en `main`. Es suficiente con
  que haya una única aprobación para integrar el pull request.

- Seguimos usando GitHub Actions  para la integración continua.

- Como hemos hecho hasta ahora, cada issue debe contener **tests
  automáticos** que prueben los cambios.
  
- Una vez terminados todos los issues de una historia de usuario, el
  responsable de la historia moverá su tarjeta en el tablero Trello a
  `En prueba`, se añadirá en la tarjeta el enlace al commit de develop
  en el que se ha realizado la integración y otro miembro del equipo
  realizará las **pruebas manuales** especificadas en sus COS
  **utilizando la base de datos MySQL**. Cuando se hayan superado
  todas las pruebas se pasará la historia a `Terminada`. Si se
  detectara algún fallo, se volverá la historia a `En marcha` y se
  abrirá un issue de tipo `bug` para resolver el problema.

### Publicación de nueva versión  ###

Al final del desarrollo se deberá lanzar una nueva release (1.4.0) en
la rama `main`.

### Documentación del desarrollo ###

- Documentar las sesiones de _pair programming_.
- Documentar la evolución de los tableros Trello y GitHub capturando 4
  instantáneas y registrando su fecha.

## Entrega y evaluación

La práctica tiene una duración de 4 semanas.

- Se realizará una **revisión del sprint** de 15 minutos en las
  **clases de prácticas del 23 de diciembre**. La revisión
  constará de:
    - Presentación con diapositivas en la que se explicará la
      **metodología seguida** en el sprint y las **nuevas funcionalidades** introducidas.
    - Demostración de las nuevas funcionalidades utilizando la última
      versión subida a GitHub.

- En la fecha límite del **10 de enero** deberá entregar la práctica y
  tener disponible:
    - Directorio `doc` en el repositorio del proyecto en el que se
      incluirá un documento PDF con la memoria de la
      práctica y un PDF con las diapositivas presentadas en la
      demo. En la memoria de la práctica se incluirá:
        - **Sprint Backlog**: historias de usuario escogidas para el
          sprint (copiar la descripción, las condiciones de
          satisfacción y el borrador de interfaz de usuario tal y
          como aparecen en la Wiki).
        - **Funcionalidades implementadas**: breve descripción para el
          usuario y breve descripción técnica.
        - **Informe sobre la evolución del desarrollo**: instantáneas
          de los tableros y alguna métrica o gráfica sobre el desarrollo
          (número de pull requests cada semana, por ejemplo).
        - **Informe sobre las sesiones de pair programming**
        - **Resultado de la retrospectiva**: qué ha ido bien en el
          sprint y qué se podría mejorar en el siguiente sprint.
    - El repositorio GitHub deberá incluir el tablero con el backlog
      del sprint con los PR completados.
    - El tablero de Trello deberá incluir el backlog del producto con
      las historias de usuario que se debían implementar en el sprint
      y los enlaces a los documentos Google Docs con sus detalles.
    - Entrega en Moodle la última versión del proyecto subida a
      GitHub.

La calificación de la práctica tiene un peso de un 13% en la nota
final de la asignatura.

Para la evaluación se tendrá en cuenta:

- Desarrollo continuo de los issues
- Corrección del código
- Correcto funcionamiento
- Informe de la práctica
- Si el trabajo de algún miembro del equipo es significativamente de
  menor calidad y/o cantidad que el del resto, se penalizará su
  calificación
