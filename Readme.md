# Git y Github

Resumen de toda la información y comandos para resolver tareas.

¿Cómo saber la versión de git que tenemos?
```bash
git --init
```

¿Cuáles son las configuraciones básicas para hacer confirmaciones?
```bash
git config --global user.name "Username"
git config --global user.mail "email@email.com"
```

¿Cómo saber si **name** y **email** están almacenadas en nuestro sistema?
```bash
git config --list
```

¿Cómo iniciar un repositorio local?
```bash
git init
```
>[!NOTE]
>Otra forma de iniciar el repositorio sería
>```bash
>git init --initial-branch=main
>git init -b main
>```
>Estas formas permiten darle el nombre a la rama principal con la que estaríamos trabajando.

¿Cómo saber si un archivo se encuentra en el _staging area_?
```bash
git status
```

¿Cómo agregar archivos al _staging area_?
```bash
git add index.html
```
>[!NOTE]
>Otra forma de agregar archivos al _staging area_
>```bash
>git add .
>```
>Estas formas permiten agregar todos los archivos que hayan sido creados o modificados.

¿Cómo quitar archivos de _staging area_?
```bash
git restore --staged index.html
```

¿Cómo quitar todos los archivos del _staging area_?
```bash
git reset
```

¿Cómo confirmar los cambios que se encuentran en _staging area_?
```bash
git commit -m "mensaje descriptivo"
```
> [!TIP]
> Mientras más avancemos en nuestro flujo de trabajo más pasos debemos realizar y más difícil será corregir errores.
>```mermaid
>flowchart LR
>	 Directorio_de_trabajo-->|Fácil|Repositorio_remoto
>    Directorio_de_trabajo-->Staging_area
>    Staging_area-->Repositorio_local
>    Repositorio_local-->Repositorio_remoto
>    Repositorio_remoto-->|Difícil|Directorio_de_trabajo
>```

¿Cómo revisar los cambios realizados que se encuentran en el _staging area_ antes de realizar un _commit_?
```bash
git diff --staged
```
>[!NOTE]
>Con `git diff`podemos ver los cambios entre _hashes_ de commit ejemplo:
>```bash
>git diff 964cca7 main
>git diff 964cca7 fac675a
>```
>De esta manera podemos ver los cambios realizados entre commits

¿Cómo revisar el historial de commit?
```bash
git log
git log --oneline #Para ver en una sola línea
```

¿Cómo podemos volver a un commit anterior?
```bash
git checkout hash
git checkout 964cca7
```

¿Cómo eliminar el último commit en local y volver al commit anterior?
```bash
git reset --soft head~1
git reset --soft 964cca7 # indicar el hash del commit
```
>[!NOTE]
>`head~1` quiere decir un commit anterior `head~2` dos commit atrás, etc.
>Al realizar el `--soft`borra el `commit`sin embargo todas las modificaciones se encuentran ahí por lo que es necesario corregir todo lo necesario para volver a realizar el `commit``

¿Cómo puedo revertir un commit y traerlo al presente?
```bash
git revert 964cca7
```
>[!NOTE]
>Lo que hace es traer el cambio anterior y añadirlo a lo que tenemos actualmente por lo que genera un nuevo commit para traerlo al presente.
>```mermaid
>gitGraph
>	commit
>	commit
>	commit type: reverse
>	commit type: highlight
>```
