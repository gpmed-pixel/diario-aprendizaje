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
-`add` sin `commit` no guarda nada en el historial, y sin historial no hay nada que publicar. El orden es siempre `add` → `commit` → `push`. Es lo mismo que comprobaste en el ejercicio 6, pero al revés.

##Publicar en Git Hub:
-Conectar la terminal con la cuenta en Git Hub usando `gh auth login` hará varias preguntas. Mover con las flechas y confirmar con Enter:
Where do you use GitHub? → GitHub.com
Preferred protocol? → HTTPS
Authenticate Git with your GitHub credentials? → Yes
How would you like to authenticate? → Login with a web browser
Te muestra un código de 8 caracteres. Cópialo, pulsa Enter, se abre el navegador, inicia sesión en GitHub, pega el código y autoriza.
-Comprobar el estatus de la conexión con `gh auth status`.
-`gh repo create diario-aprendizaje --public --source=. --push` → Crear repositorio en Git Hub 
     `--public`: visible para cualquiera. Es tu portfolio.
     `--source=.`: usa la carpeta actual.
     `--push`: sube tus commits.
Deberías ver: una URL tipo https://github.com/TU_USUARIO/diario-aprendizaje.

##Entender la conexión:
-`git remote -v` muestra la conexión comenzando por "origin" al parecer la ruta origen del repositorio creado.

##Crear fichero README.MD:
-Para crear en VS Code `code README.md`. Se guarda el cambio con Cmd + S.
-Para subir `git add README.md`, se genera el commit `git commit -m "Añado README.md", se publica con `git push`.
-Abrir la web https://github.com/TU_USUARIO/diario-aprendizaje para ver que se ha subido.

##Nota 1:
-`add` sin `commit` no guarda nada en el historial, y sin historial no hay nada que publicar. El orden es siempre `add` → `commit` → `push`. Es lo mismo que comprobaste en el ejercicio 6, pero al revés.

## Error al modificar el repositorio en la web de Git Hub directamente:
- Texto: 
To https://github.com/gpmed-pixel/diario-aprendizaje.git
 ! [rejected]        main -> main (fetch first)
error: failed to push some refs to 'https://github.com/gpmed-pixel/diario-aprendizaje.git'
hint: Updates were rejected because the remote contains work that you do not
hint: have locally. This is usually caused by another repository pushing to
hint: the same ref. If you want to integrate the remote changes, use
hint: 'git pull' before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.

- GitHub tiene commits que en local no están. Git se niega a hacer el push porque, si lo hiciera, borraría esos cambios de GitHub. Es una protección, no un fallo.
### Cómo arreglarlo?
-1. Mirar que hay en Git Hub que no en local:
`git fetch` → descarga la información de GitHub pero no toca tus ficheros.
`git log --oneline main..origin/main` → lista los commits que están en GitHub y no en local.

-2. Trae esos cambios y poner los del local encima:
`git pull --rebase` → coloca tus commits después de los de GitHub, como si los hubieras hecho más tarde, y deja un historial lineal.

-3. Se sube:
`git push`

Si en el paso 2 sale “CONFLICT” significa que en local y en GitHub se han cambiado las mismas líneas del mismo fichero. Por ejemplo se ha borrado un fichero en Git Hub pero estás realizando una subida desde local de ese mismo fichero.

Git no puede decidir solo si el fichero debe existir o desaparecer, así que te pide que decidas tú. Por eso se llama conflicto de tipo modify/delete.

Estás a mitad de un rebase: Git ha pausado el proceso y espera tu decisión. Nada se ha perdido. Si en algún momento te lías:
`git rebase --abort` → te devuelve exactamente a como estabas antes del `git pull --rebase`.

Solución (quedarte con tu fichero)

-1. Comprueba que tu versión está ahí:
 `cat apuntes/git.md`

-2. Dile a Git que el fichero se queda:

`git add apuntes/git.md`

Recuerda que `add` sirve para meter algo en la “orden de transporte”. Aquí además le dice a Git: “conflicto resuelto, quiero esta versión”.

-3. Continúa el rebase:

`git rebase --continue`

Es probable que se abra vim (el editor raro de la Terminal) para que confirmes el mensaje del commit. Para guardar y salir sin cambiar nada, pulsa Esc, escribe `:wq` y pulsa Enter. Esta vez es `:wq` (guardar y salir), no `:q!` (salir sin guardar).

-4. Comprueba:

`git status`
`git log --oneline`
`git status` ya no debe decir rebase in progress.
En el log debe aparecer arriba Delete apuntes/git.md y encima tus commits.

-5.Sube:

`git push`

##Nota2:
-Regla: trabaja solo en local, al menos durante este road map. Cada cambio en la web crea un commit que tu Mac no tiene, y acabas en situaciones como esta.
Si alguna vez editas en la web: haz git pull antes de tocar nada en local.
Tu commit bad8865 se llama “Corrección de Branch”. ¿Qué corregiste? Si el mensaje no lo explica, dentro de un mes no lo sabrás. Un buen mensaje dice qué cambia: por ejemplo, “Corrijo explicación de ramas en git.md”.