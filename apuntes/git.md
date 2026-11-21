##Configuración Inicial
-`git config --global user.name "Guillermo Apellido"` → Define un nombre usuario para firmar el commit.
-`git config --global user.email "tu-email"` → Define el email para el usuario.
-`git config --global init.defaultBranch main` → Define la rama principal como main como en Git Hub.
-Para comprobar los cambios se usa `git config --global --list`.

##Trabajo con repositorios
-Para crear un repositorio en git se abre la carpeta y luego se ejecuta `git init`(debería verse Initialized empty Git repository in /../../.git/.
- Se comprueba que se ha creado la carpeta .git dentro del directorio seleccionado anteriormente  mediante `ls -la`.

###Ejercicio 1: ¿qué crees que guarda .git? Anótalo.
- Para mi en la carpeta .git se guarda la configuración y versiones creadas en git(No he accedido aún al contenido).

##Estado:
-`git status` → vemos el estado del contenido de la carpeta. Deberías ver: notas.txt en rojo, debajo Untracked files. Significa que Git ve el fichero pero todavía no lo controla.
-`git add notas.txt` → prepara el fichero antes de liberarlo con `commit` ( el nombre del fichero se resalta en verde bajo Changes to be committed. Has metido el objeto en la “orden de transporte”, pero aún no la has liberado).

##Commit:
-git commit -m "Primer commit: añado notas.txt" → libera la versión y le asigna el texto luego debería aparecer un resumen del commit y "nothing to commit, working tree clean" (Si escribes git commit sin -m "…", se abre un editor raro en la Terminal (vim). Para salir sin guardar, pulsa Esc y escribe :q! + Enter). 
-`git log --oneline` → Se usa para visualizar el historial de commit que han subido correctamente.

###Ejercicio 5: git log --oneline Deberías ver: dos líneas, cada una con un código y tu mensaje ¿qué es ese código?
- Ese código es un id que define la versió subida con el commit.


###Ejercicio 6: Commit sin add
echo "cuarta línea" >> notas.txt
git commit -m "Intento sin add"¿qué pasa? ¿Por qué? Commit sin add
- Sin add el cambio no se libera y no se puede realizar el commit.


##.DS_Store:
-.DS_Store es un fichero que crea macOS para recordar cómo ves la carpeta en Finder (iconos, orden…). No aporta nada a tu proyecto y no debe subirse.
-`echo ".DS_Store" > .gitignore` → Debería verse: .DS_Store ha desaparecido de la lista y ha aparecido .gitignore. La carpeta .gitignore es la lista de ficheros que Git debe ignorar.

## Commit de una carpeta entera:
- `git add .` → añade todo lo de la carpeta actual, antes de realizar el commit hay que revisar con `git status` que va a entrar.




