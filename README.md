# Pequeño manual de Git

## ¿Qué es Git?
Git es un [Sistema de control de versiones](https://es.wikipedia.org/wiki/Control_de_versiones "Wikipedia").
Es un software para poder gestionar, compartir y guardar todas las etapas y versiones del código de tu proyecto.

Imagínense el código open source, o un programa elaborado por muchos programadores a la vez.
¿Cómo hacen? Bueno, utilizan sistemas como este para poder tener siempre un back-up de su código,
y tener un registro legible de todo el desarrollo.

## ¿Qué es un repositorio?
Básicamente es una carpeta que contiene un archivo `.git`.
Sería un proyecto o carpeta la cual está enlazado a esa carpeta `.git`.
Por lo tanto todos los archivos que estén dentro de esa carpeta estarán relacionadas al repositorio
, sin embargo no todos los archivos tienen que estar *trackeados* por git.
¿Cómo eligo que archivos pueden estar en mi repositorio?

### El archivo `.gitignore`
Si se darán cuenta, en algunos repositorios se encuentra un archivo oculto llamado `.gitignore`.
Este archivo contiene una lista de *extensiones* o nombres de archivos que se ignorarán en el repositorio.
Por lo tanto, si en el proyecto se incluye un elemento con alguna extensión presente en `.gitignore`
simplemente no se incluirá en el repositorio, y git no hará seguimiento de él. 
Es importante decir que si el archivo ya pertenece al repositorio, no se excluíra del mismo una vez que
se incluya en el archivo `.gitignore`.

### Ramas
Las ramas son algo escencial en git. Es también conocido como *branch*.
Un *branch* es básicamente una copia del proyecto la cual eventualmente se podrá volver a unir (o hacer un *merge*) con la rama principal, la que suele ser `main` o `master`.
Las ramas sirven para
- Que los desarrolladores puedan codear en un espacio de trabajo sin interferir con el código de los demás.
- Poder hacer copias para probar nuevas funciones
- Hacer copias para poder reparar algo

## Repositorio local y Repositorio remoto
Estos conceptos serán importantes para reconocer la diferencia entre *Git* y *GitHub*.

### Repositorio remoto
Un repositorio remoto es una copia del proyecto (que suele ser la copia principal) almacenada en una plataforma online o en algún servidor o equipo externo a nuestro equipo de trabajo. Suelen haber distintas como por ejemplo:
- *[GitHub](https://github.com/ "Página Web")*
- *[GitLab](https://about.gitlab.com/ "Página Web")*
- *[SourceForge](https://sourceforge.net/ "Página Web")*

### GitHub
*GitHub* es una plataforma en la nube que almacena, distribuye y gestiona repositorios de *Git*. Por lo tanto, será fundamental crearnos una cuenta en alguna de estas plataformas para poder compartir nuestros repositorios y/o poder trabajar con otras personas en nuestros proyectos. Sin embargo, no es necesario hacerlo para poder trabajar con *Git* y aún así ser altamente útil y eficiente.

### Repositorio local
Un *repositorio local* es una copia del proyecto la cual está almacenada en nuestra computadora, o en nuestro propio entorno de trabajo. Este repositorio puede o no estar sincronizado con un *repositorio remoto*, y esto se puede configurar a conveniencia en cualquier etapa.

---

# Iniciando en Git
Aprender Git es escencial para poder tener un flujo de trabajo óptimo en tus proyectos. ¿Qué debo hacer para poder comenzar? 

### Instalar Git en tu computadora
Instalar Git en tu computadora te permitirá trabajar con repositorios ya sean locales o remotos. Una vez instalado, los comandos de Git serán reconocidos en la terminal. *Si no tienes Git instalado lo puedes [descargar aquí](https://git-scm.com/downloads "Descargar")*.

## El comando `git status`

Una vez instalado, deberías poder abrir la terminal en cualquier carpeta, ingresar el comando `git status` y obtener algo parecido a alguna de estas opciones:

- Por un lado, si no existe un *repositorio local* en esa carpeta, verás esto

  `fatal: not a git repository (or any of the parent directories): .git`
  
  Esto no significa algo malo, simplemente el sistema te está diciendo que no existe un repositorio ahí.

- Si por otro lado, existe un repositorio en esa carpeta, verás algo similar a esto:

      On branch main
      Your branch is up to date with 'origin/main'.

      nothing to commit, working tree clean
  Esto significa que estás ubicado en la *rama main* de tu *repositorio local*, y que ese repositorio está actualizado con el *repositorio remoto* llamado *origin/main*. *Origin* es el nombre del *repositorio remoto* que puede, por ejemplo, estar almacenado en GitHub, y *main* es el nombre de la rama que existe en ese repositorio, que por cierto, está sincronizada con la rama *main* de nuestro *repositorio local*.
Por último `nothing to commit. working tree clean` significa que no hay nada que esté listo para hacer un *commit*, pero veremos eso luego.

## Iniciando un repositorio
En cierta manera pueden haber tres formas para iniciar un repositorio (o por lo menos las que yo utilizo):

1. **Iniciar un repositorio local en un proyecto vacío**

   - Debemos ir a la carpeta donde queremos almacenar nuestro proyecto y le damos al comando `git init` (siempre podemos primero utilizar `git status` para asegurarnos que todo está bien).
   
      Si todo salió bien deberías ver algo así
   
         Initialized empty Git repository in <ubicación del proyecto en tu computadora>/.git/
      Si nuevamente utilizas `git status` deberías poder ver algo similar a esto
   
         On branch main

         No commits yet

         nothing to commit (create/copy files and use "git add" to track)

2. **Iniciar un repositorio local en un proyecto avanzado**

    - En este caso sería igual que el anterior, a diferencia que como ya existen archivos, estos están listos para ser trackeados en el proyecto

          On branch main

          No commits yet
          
          Untracked files:
          (use "git add <file>..." to include in what will be committed)
               settings.py
               main.py

          nothing added to commit but untracked files present (use "git add" to track)
    - Podemos ver que nos dice `untracked files:`, esto significa que hay archivos en la carpeta que no están siendo seguidos por Git, y que podemos *trackearlos* si los agregamos al siguiente *commit*. Para agregarlos al siguiente *commit* o *trackearlos* en el proyecto utilizamos el commando `git add`.
    - En este caso si sólo quisiéramos agregar el archivo `main.py`a nuestro repositorio, tendríamos que hacer `git add main.py`.
    - Por otro lado si quisiéramos agregar todos los archivos a la vez utilizamos `git add .`.

Hay que señalar que en ambos casos (*caso 1 y 2*), el repositorio aún no está sincronizado con un *repositorio remoto*. Luego podremos hacer esto con el comando `git remote add <nombre del repositorio> <url del repositorio>`.

3. **Clonar un repositorio remoto en nuestra computadora**

    Por último podemos clonar un *repositorio remoto* alojado, por ejemplo, en *GitHub*. Esto significa hacer una copia local de este repositorio en nuestra computadora. Quizá este es el método más popular para empezar a trabajar con un repositorio. Sin embargo, creo que es bueno sólo usarlo cuando el proyecto ya existe y está alojado ahí.
    
    - Primero debemos ir a *GitHub* e ir al repositorio que queremos clonar. Debería haber un botón verde que dice *Code*, dentro podemos copiar la url de ese repositorio.
    - Una vez que copiamos la url, vamos a la carpeta donde queremos que se encuentre el proyecto y usamos el comando `git clone <url del repositorio>`. Deberiamos poder ver algo así:
     
          Cloning into 'Repositorio'...
          remote: Enumerating objects: 72, done.
          remote: Counting objects: 100% (72/72), done.
          remote: Compressing objects: 100% (50/50), done.
          remote: Total 72 (delta 27), reused 63 (delta 20), pack-reused 0 eceiving objects:  44% (Receiving objects:  95% (69/72)
          Receiving objects: 100% (72/72), 12.71 KiB | 394.00 KiB/s, done.
          Resolving deltas: 100% (27/27), done.
    - Si lograste ver eso significa que el repositorio se descargó correctamente en tu computadora, por lo tanto ya tienes un *repositorio local* de ese *repositorio remoto* que acabas de clonar. Ahora deberías también poder ver todos los archivos del proyecto en tu computadora.
---
# Flujo de trabajo en Git
Tener un flujo de trabajo es muy importante en Git. Esto es internalizar cierta secuencia de comandos para poder trabajar de una manera ordenada y lejible. Esto es útil para que cuando otra persona necesite revisar el código, sepa perfectamente que fue lo que sucedió y cómo fue evolucionando.

## Flujo básico en Git con los comando básicos
Los comandos básicos con los que se trabaja en Git son los siguientes:
- Para checkear el estado del repositorio

    `git status`
- Para preparar los archivos con cambios para el *commit*

    `git add .`
- Para realizar el *commit*

    `git commit -m "Mensaje para el commit"`
- Para enviar los cambios desde el *repositorio local* hacia el *repositorio remoto*

    `git push`.

### El comando `git add <archivo>`
Cuando uno ha realizado un cambio, luego hay que preparar esos archivos para ser integrados en un *commit*. La razón es que por ahí uno está trabajando con varios archivos simultáneamente, pero no quiere agregar todos los archivos para el *commit* ya que quizá no todos están listos. Por lo tanto, con este comando, uno elige que archivos se van a preparar para el commit. Con el comando `git add .` se agregan todos los archivos que han sufrido cambios (`.` suele significar "todo"), por otro lado, si se quiere elegir un archivo en particular para que vaya al commit, se debe ingresar el nombre en el comando de la siguiente forma `git add <nombre del archivo>`.

### El comando `git commit -m "<Mensaje para el commit>"`
La manera de trabajar consiste en que uno realiza cambios en el archivo y a medida que se realice un cambio signiticativo, funcional, o una unidad, se debe realizar un *commit*. Un ***commit*** es un checkpoint en nuestro repositorio, que nos permitirá entender de manera clara el proceso de desarrollo. Por ejemplo, si uno está programando una página web, a medida que se realiza cada cambio, sería recomendable hacer un *commit*. Por ejemplo, si se quiere integrar un formulario, cuando se escribe hay que hacer un checkpoint, luego si uno quiere integrar un *menú de navegación* debe hacer un checkpoint, por ejemplo `git commit -m "Integré un formulario en 'contacto.html'"` y luego `git commit -m "Integré menú de navegación en 'index.html'"`.
**No es recomendable ni buena idea** realizar un *commit* después de haber realizado varios cambios, ya que después será difícil entender quién hizo qué, cuándo y cómo se hizo. 

### El comando `git push`
Este comando sirve para enviar los *commit* realizados en el *repositorio local* hacia el *repositorio remoto*. Por ejemplo, uno puede hacer estos checkpoints sin interferir con la rama correspondiente en el *repositorio remoto*, y sólo cuando se ejecuta el comando `git push` estos cambios se envian hacia el *repositorio remoto*.

### Resúmen del flujo de trabajo
Por lo tanto, el flujo de trabajo sería el siguiente:

1. Ejecutar `git status` para checkear el estado del repositorio (Es recomendable ejecturarlo en cada paso del proceso, para asegurarse que todo va saliendo bien)
2. Realizar los cambios en el código
3. Luego ejecutamos el comando `git status` para ver los cambios realizados, deberíamos ver algo similar a esto:

       On branch dev
       Changes not staged for commit:
       (use "git add <file>..." to update what will be committed)
       (use "git restore <file>..." to discard changes in working directory)
       modified:   archivo.txt

       no changes added to commit (use "git add" and/or "git commit -a")
4. Preparar los archivos para el *commit* con el comando `git add <nombre del archivo>`. En este caso podría ser `git add .` o `git add archivo.txt`. Deberíamos ver algo similar a esto:

       On branch dev
       Changes to be committed:
       (use "git restore --staged <file>..." to unstage)
       modified:   archivo.txt
    En caso de arrepentirnos de preparar para el commit a un archivo, podemos volver atrás con el comando `git restore --staged <nombre del archivo>`. En este caso también se puede aplicar `git restore --staged .` para aplicar a todos los archivos.
5. Realizar el commit y agregar una pequeña descripción del cambio se realizó. Por ejemplo `git commit -m "Agregué un botón a la página principal"`. Deberíamos ver algo similar a esto:

       [dev 3f892a5] Realicé un cambio
       1 file changed, 2 insertions(+), 1 deletion(-)
6. Si ejecutamos `git status` deberíamos ver lo mismo que en el paso 1, que sería algo similar a esto:

       On branch dev
       nothing to commit, working tree clean
7. Luego se puede seguir trabajando en el *repositorio local* realizando cambios y repitiendo estos pasos
8. Cuando se quiera enviar los cambios hacia el *repositorio remoto*, se ejecuta el comando `git push`. En este paso es necesario tener los permisos necesarios para poder actualizar el repositorio. Si el repositorio es tuyo tienes que ingresar tu cuenta, y si es de otra persona, antes debería darte acceso al repositorio. 
9. Luego estos pasos se repiten indefinidamente

## Trabajando con las ramas (*branch*)
Para hacer un flujo de trabajo ordenado, vamos a tomar a la rama principal `main`o `master` como nuestra rama estable. Debería ser la rama donde siempre hay una versión del programa que funcione, y es de alguna manera la rama que va a exibirse primero cuando se abra el repositorio en *GitHub* o en tu *repositorio remoto*. Entonces a medida que vamos desarrollando, sería recomendable actualizar (o *mergear*) la rama `main` con la rama en donde se desarrollan los cambios (que suele se la *rama* `dev`) a medida que surja una versión estable, esto quiere decir, que el programa funcione sin romperse, o que el diseño esté cerrado. Aunque el proyecto no esté terminado, es recomandable que siempre la rama `main`sea una rama funcional.

También vamos a crear una nueva rama la cual vamos a llamar, por ejemplo, `dev`. *Dev* significaría "desarrollo", esta será la rama base secundaria en donde ocurrirán todos los *commits* y cambios que estén en pleno desarrollo. Una vez que se ha alcanzado un estado donde el programa es estable, la rama `dev` puede volver a unirse con la rama `main`. Luego, de sigue trabajando en la rama `dev`. 

Si se está trabajando con varias personas, o ha surgido algo que motiva a hacer una nueva rama adicional para no interferir con la rama de trabajo, es recomendable hacer una nueva rama en base a la rama `dev`. Es una buena práctica ponerle el nombre del *desarrollador* o de la función que se está tratando de implementar o reparar, como por ejemplo, `dev-juan`, `dev-fix-button`, `dev-nueva-funcion`, etc.

### Ejemplo práctico con ramas
Imáginemos que tenemos un grupo de trabajo de tres personas, **Pedro**, **Juan** y **Diego**.
- Al iniciar el repositorio sólo existirá una rama, la rama `main` o `master`. Si utilizamos `git status` veremos algo así.

      On branch master
      nothing to commit, working tree clean

- Debemos crear una nueva rama con el comando `git branch <nombre de la rama>`, en este caso sería `git branch dev` para crear la rama `dev`. Para verificar que todo salió bien, puedes utilizar el comando `git branch` para ver las *ramas locales*. Deberías ver algo similar a esto:

        dev
      * master
    Acá podemos ver que exiten dos ramas, la rama `master` en la cual estás ubicado, y la rama `dev`, que es la que acabamos de crear.
- Luego tenemos que cambiarnos desde la rama `main` a la rama `dev`. Esto lo hacemos con el comando `git checkout <nombre de la rama>`, en este caso `git branch dev`. Deberíamos ver algo así:

      Switched to branch 'dev'
- Luego podemos aplicar `git status` y ver que todo esté bien

      On branch dev
      nothing to commit, working tree clean

¡Genial! Hemos creado la rama `dev`. Si estuviéramos trabajando solos, podríamos trabajar directamente desde la rama `dev`y solo crear otra rama en caso de reparar algún error o probar algo. Sin embargo, para nuestro caso, sería recomendable que cada desarrollador haga su propia rama para hacer sus tareas, o quizá también que cada uno cree una rama para la tarea asignada. Eso depende, pero es importante de antemano saber quién va a hacer qué, simplemente para optimizar el flujo, ya que aunque así fuera, con Git siempre hay una manera de gestionar el código.

- Si cada desarrollador va a tener su rama, entonces cada uno debería ir a la rama `dev` en su *repositorio local* y luego crear su propia rama con el comando `git branch dev-pedro`, `git branch dev-juan` y `git branch diego`. Es importante considerar que al crear una nueva rama, esta será identica a la rama en la cual uno se encuentre al momento de ejecutar el comando `git branch`.
- Si van a haber ramas dependiendo la tarea, primero hay que ir a la rama `dev` y luego hacer, por ejemplo, `git branch dev-boton` o `git branch boton`.
- Una vez que se han efectuado cambios significativos en la rama `dev` y el proyecto es estable, se puede *mergear* estos cambios en la rama `main`. Esto lo hacemos con el comando `git merge <nombre de la rama >`. Cabe recalcar, que los cambios se integrarán desde la rama mencionada en el comando `git merge <rama con los cambios>`hacia la rama en la cual uno se encuentra. Por ejemplo, si estás en la rama `main`y quieres que los cambios realizados en la rama `dev`se integren hacia la rama `main`, debes primero asegurarte de estar en la rama `main`y luego desde ahí ejecutar el comando `git merge dev`. 
Si todo salió bien, deberías ver algo similar a esto: 

      Updating 1850d07..dc60e8f
      Fast-forward
      git.txt | 3 ++-
      1 file changed, 2 insertions(+), 1 deletion(-)
    Esto significa que el archivo recibió un cambio, que se agregaron 2 cambios y se borró uno. Esto depende de los cambios que hayas realizado.
- Luego, cuando la rama `main` ya esté actualizada con la rama `dev`, puedes seguir trabajando en la rama `dev`si el proyecto aún no está terminado, pero ya en la rama `main` habrá una versión estable del proyecto. 

### Borrar ramas
Para borrar las ramas hay dos comandos, uno para borrar la rama en el *repositorio local* y otro comando para borrar la rama *en el repositorio remoto*. Es decir, cuando borras una rama, tienes que hacerlo en ambos repositorios (en caso que estén con *repositorio remoto*)
El comando para borrar la rama en el *repositorio local* es `git branch --delete <nombre de la rama>`. Y para borrar la rama en el *repositorio remoto* es `git push --delete <nombre del repositorio> <nombre de la rama>`.

Acá hay un ejemplo en donde se borra una rama llamada `dev-base-de-datos`. Primero se borra en el *repositorio local* y luego en el *repositorio remoto*:
```
PS C:\Users\Usuario\PycharmProjects\Recetapp> git branch --delete dev-base-de-datos
Deleted branch dev-base-de-datos (was 209e29d).
PS C:\Users\Usuario\PycharmProjects\Recetapp> git push --delete origin dev-base-de-datos
To https://github.com/Ontos-2021/Recetapp.git
 - [deleted]         dev-base-de-datos
PS C:\Users\Kotelo\PycharmProjects\Recetapp> 
```

*PD: Para borrar una rama primero tienes que moverte a otra rama. No puedes borrar la rama en la cual te encuentras*. 

---

# Comandos
Dentro de los comandos más importantes están los siguientes:

- Para clonar el repositorio

  `git clone <link del repositorio>`

- Checkear en que estado se encuentra el repositorio

  `git status`

- Para agregar un archivo para el *commit*

  `git add <nombre del archivo>` o `git add .`para agregar todos los archivos.

- Hacer un *commit*

  `git commit -m "<mensaje para  describir el commit>"`

- Enviar los cambios al repositorio remoto

  `git push`

- Actualizar el repositorio local con el repositorio remoto

  `git pull`

- Revisar todos los *branch* que existen

  `git branch --all`

- Cambiar de rama

  `git checkout <nombre de la rama>`

- Crear una nueva rama

  `git branch <nombre de la rama>`

- Borrar un *branch*

  `git branch --delete <nombre de la rama>`

- Sincronizar el *repositorio local* con un *repositorio remoto*

  `git remote add <nombre del repositorio> <url del repositorio>`

---

# Referencias
- [Configuración de un repositorio | Atlassian - Bitbucket](https://www.atlassian.com/es/git/tutorials/setting-up-a-repository "Tutorial")
