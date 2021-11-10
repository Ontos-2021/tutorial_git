# Pequeño manual de Git

## ¿Qué es Git?
Git es un [Sistema de control de versiones](https://es.wikipedia.org/wiki/Control_de_versiones "Wikipedia").
Es un software para poder gestionar, compartir y guardar todas las etapas y versiones del código de tu proyecto.

Imagínense el código open source, o un programa elaborado por muchos programadores a la vez.
¿Cómo hacen? Bueno, utilizan sistemas como este para poder tener siempre un back-up de su código,
y tener un registro legible de todo el desarrollo.

## ¿Qué es un repositorio?
Básicamente es un carpeta que contiene un archivo `.git`.
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
Estos coneceptos serán importantes para reconocer la diferencia entre *Git* y *GitHub*.

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

# Flujo de trabajo
Git es escencial para poder tener un flujo de trabajo óptimo. ¿Qué debo hacer para poder comenzar? 

## Instalar Git en tu computadora
Instalar Git en tu computadora te permitirá trabajar con repositorios ya sean locales o remotos. Una vez instalado, los comandos de Git serán reconocidos en la terminal. *Si no tienes Git instalado lo puedes [descargar aquí](https://git-scm.com/downloads "Descargar")*.

### El comando `git status`

Una vez instalado, deberías poder abrir la terminal en cualquier carpeta, ingresar el comando `git status` y obtener algo parecido a alguna de estas opciones:

- Por un lado, si no existe un *repositorio local* en esa carpeta, verás esto

  `fatal: not a git repository (or any of the parent directories): .git`
  
  Esto no significa algo malo, simplemente el sistema te está diciendo que no existe un repositorio ahí.

- Si por otro lado, existe un repositorio en esa carpeta, verás algo similar a esto:

      On branch main
      Your branch is up to date with 'origin/main'.

      nothing to commit, working tree clean
  Esto significa que estás ubicado en la *rama main* de tu *repositorio local*, y que ese repositorio está actualizado con el *repositorio remoto* llamado *origin/main*. *Origin* es el nombre del *repositorio remoto* que puede, por ejemplo, estar almacenado en GitHub, y *main* es el nombre de la rama que existe en ese repositorio, que por cierto, está sincronizada con la rama *main* de nuestro *repositorio local*.
  Por último `nothing to commit. working tree clean` significa que no hay nada que esté listo para hacer un `commit`, pero veremos eso luego.

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

Hay que señalar que en ambos casos (*caso 1 y 2*), el repositorio aún no está sincronizado con un *repositorio remoto*. Luego podremos hacer esto con el comando `git remote add <nombre del repositorio> <url del repositorio>>`.

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
