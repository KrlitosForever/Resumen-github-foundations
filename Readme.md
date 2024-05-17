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
>
>```bash
>git init --initial-branch=main
>git init -b main
>```
>
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
>
>```bash
>git add .
>```
>
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
>
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
>
>```bash
>git diff 964cca7 main
>git diff 964cca7 fac675a
>```
>
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
>
>```mermaid
>gitGraph
>	commit
>	commit
>	commit type: reverse
>	commit type: highlight
>```

¿Cómo se crea una rama en git?

```bash
git branch nombre-rama
```

¿Cómo consultar todas las ramas incluidas las del remoto?

```bash
git branch --all
# La forma corta sería
git branch -a
```

¿Cómo crear una rama y moverse a ella inmediatamente?

```bash
git checkout -b nombre-rama
```

¿Cómo eliminar una rama?

```bash
git branch -d nombre-rama
```

>[!NOTE]
>Si eliminas una rama y esta tiene cambios que no se han fusionado a alguna rama. Git no dejará eliminar con `git branch -d nombre-rama` solo si estas seguro te dejará realizarlo de la siguiente manera `git branch -D nombre-rama`

¿Cómo ver de manera gráfica y resumida el historial?

```bash
git log --all --decorate --oneline --graph
```

¿Cómo ver de manera gráfica el historial?

```bash
git log --all --decorate --graph
```

¿Cómo crear un copia de mi repositorio local en mi repositorio remoto?

```bash
git push origin main
#Tener en cuenta que nuestro remoto se llama origin y la rama que estamos pusheando es main. Estos valores podrían cambiar según en la rama que te encuentres.
```

¿Cómo traigo los cambios en mi repositorio local del remoto?

```bash
git pull origin main
```

> [!CAUTION]
> Siempre es importante mantener tu rama protegida por lo que es importante considerar este punto. Recomiendo activar los cambios a traves de PR y que los mantenedores no se salten esta regla para tener un buen control.

## Git stash

Git stash es una función muy útil en git que te permite guardar temporalmente cambios locales en tu directorio de trabajo sin comprometerlos con un commit esto es útil en varios casos.

1. Cambios de contexto
2. Interrupciones inesperadas
3. Resolución de conflicto
4. Experimentación temporal
5. Preparación para _pull_ o _merge_

```bash
# Para guardar sin comprometer
git stash

# Para listar los stash
git stash list

# Para traer los cambios
git stash pop

# Para eliminar el stash
git stash drop
```
