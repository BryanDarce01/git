# `git restore`

Es un comando **moderno** introducido en Git 2.23 para reemplazar la parte “ambigua” de `git checkout` cuando se trata de **restaurar archivos**.

`git restore` se enfoca solo en:

- ✔️ Restaurar contenido de archivos.

- ✔️ Restaurar el estado del working directory
- ✔️ Restaurar el staging area (index)

Es decir, sirve para descartar cambios.

# 🧩 ¿Por qué existe git restore?

Históricamente:

``` bash
git checkout <commit> <file>
git checkout -- <file>
```
hacía demasiadas cosas: cambiar de rama, restaurar archivos, crear ramas…

Esto confundía a miles de desarrolladores.


Por eso el equipo de Git creó:

`git switch` → cambiar ramas / commits

`git restore` → restaurar archivos

# 🧠 Comportamiento por defecto

Todo lo que restaure se hace desde `HEAD`, a menos que se indique otro commit.

# 🛠️ CASO 1 — Restaurar un archivo al último commit (descartar cambios locales)

``` bash
git restore <file>
```

Esto hace:

- Reemplaza el contenido del archivo por el del último commit.

- Si había cambios sin commitear → se pierden.

Es equivalente a:

``` bash
git checkout HEAD <file>
```

# 🛠️ CASO 2 — Restaurar un archivo desde otro commit o rama

``` bash
`git restore --source=HEAD <file>`
```

Ejemplos:

``` bash
git restore --source=HEAD~2 app.js
git restore --source=main config.yml
git restore --source=4f2a7c3 src/utils.py
```

# 🛠️ CASO 3 — Borrar el archivo del staging (quitar `git add`)

Restaurar el archivo **solo en el staging area** (index):

``` bash
git restore --staged <file>
```

Ejemplo:

``` bash
git add .
git restore --staged package.json
```

Lo devuelve al working directory como si nunca lo hubieras añadido.

# 🛠️ CASO 4 — Restaurar archivo en staging y en working directory

``` bash
git restore --staged --worktree <file>
```
Aunque normalmente solo se hace:

``` bash
git restore --staged <file>
git restore <file>
```
# 🛠️ CASO 5 — Restaurar todos los archivos modificados

``` bash
git restore .
```
o

``` bash
git restore --staged .
```

# 🧱 ¿Qué restaura cada opción?

| Opción                | Significa                                  | Zona afectada             |
| --------------------- | ------------------------------------------ | ------------------------- |
| `--staged`            | Restaurar lo que está en staging           | Index                     |
| (sin flags)           | Restaurar lo que está en working directory | Working Directory         |
| `--source=<ref>`      | De dónde sacar la versión del archivo      | Commit / rama / tag       |
| `--worktree`          | Restaurar en el árbol de trabajo           | Working Directory         |
| `--staged --worktree` | Restaurar ambos                            | Index + working directory |


# 🧠 Resumen sencillo

- `git restore` descarta cambios.

- Si se quiere ver o cambiar commits, usar `git switch`.

Si se quiere revertir commits ya hechos, usar `git revert` o `git reset`.