# Terminal – apuntes

## Orientarse
- `pwd` → muestra la carpeta en la que estoy.
- `ls` → lista el contenido; `ls -la` incluye ocultos y detalles.
-`man` → se utiliza para ver el manual de un comando.

## Moverse
- `cd ruta` → Entra en una subcarpeta de la ubicación actual.
-`cd ..` → Sube un nivel hacia atrás de donde te encuentras.
-`cd -` → Regresa a la última carpeta donde estuviste.
- Ruta absoluta: La ruta empieza por / o ~ y funciona estés donde estés te lleva directamente hasta la carpeta del usuario si usas cd ~ y si usas cd / te lleva a la raíz del sistema.
- Ruta relativa: partes desde donde te encuentras.

## Directorios
-`mkdir` → crea nuevos directorios en el directorio que te encuentras.
-`rmdir` → Borra directorios que no contengan archivos.

## Copiar/Borrar/Mover
-`cp` → Copiar.
-`mv`→ Mover/Renombrar.
-`rm`→ Borrar.

## Ficheros
-`touch fichero.md` → Crea un fichero en la ruta indicada.  
- `echo 'texto' > carpeta o ruta` → Borra el contenido del fichero y añade el nuevo  `echo 'texto' >> carpeta o ruta` → No borra el contenido del fichero y añade el nuevo contenido.
- `rm` → borra sin papelera. ¡Cuidado!
- `open fichero.txt` abre archivos. 

## Errores que he cometido
- Confundí ruta absoluta y relativa: No sabía la diferencia entre ruta absoluta y ruta relativa;
No sabía la diferencia entre > y >> en los ficheros.

## Respuesta ejercicio 10
-En BW una ruta absoluta se puede ver en el servidor de aplicaciones, donde tienes una carpeta principal y dentro de ella tienes subcarpetas donde puedes almacenar los ficheros de cargas, luego se extraen mediante un DTP usando la ruta relativa que es la ruta final del fichero.
-En la transacción AL11 te devuelve a la ruta absoluta y .. te devuelve un nivel más de donde te encuentras.

## ¿qué pasaría si usaras > en lugar de >> en echo 'eval "$(…brew shellenv zsh)"' >> /Users/guille/.zprofile
- Se borraría todo el contenido de zprofile para añadir solamente 'eval "$(…brew shellenv zsh)"' perdiendo la información definitivamente.