# `git checkout`

El comando `git checkout` es muy poderoso, pero también confuso, porque hace demasiadas cosas distintas:

- Cambiar de rama

- Restaurar archivos

- Moverte a un commit específico


Por eso, desde Git 2.23 (2019), se introdujeron dos comandos nuevos que separan esas funciones:

- 👉 `git switch`
- 👉 `git restore`


## Comparación con `switch`

| Acción                                           | Comando viejo (`checkout`)           | Comando nuevo recomendado                   |
| :----------------------------------------------- | :----------------------------------- | :------------------------------------------ |
| Cambiar de rama existente                        | `git checkout nombre-rama`           | ✅ `git switch nombre-rama`                  |
| Crear y moverte a una nueva rama                 | `git checkout -b nueva-rama`         | ✅ `git switch -c nueva-rama`                |
| Cambiar a un commit específico (modo detached)   | `git checkout <hash>`                | ✅ `git switch --detach <hash>`              |
| Restaurar un archivo al estado del último commit | `git checkout -- archivo.txt`        | ✅ `git restore archivo.txt`                 |
| Restaurar un archivo de un commit específico     | `git checkout <hash> -- archivo.txt` | ✅ `git restore --source <hash> archivo.txt` |


# En resumen

Usar git switch para:

- Moverte entre ramas

- Crear ramas nuevas

- Moverte a un commit específico (modo seguro)

- Usa git restore para:

- Deshacer cambios en archivos del directorio de trabajo

- Recuperar versiones anteriores de archivos

Usar `git checkout` solo si se está en un entorno viejo o se necesita compatibilidad con scripts antiguos.


# 2. `git checkout <commit-hash>`

Nos **mueve (cambia el HEAD)** al commit específico que corresponde a ese ***hash***.


## En otras palabras:
👉 Git cambia el directorio de trabajo (los archivos en tu carpeta del proyecto) para que coincidan exactamente con cómo estaban en ese commit.

Si ejecutamos

``` bash
git checkout a1b2c3d
```

## Esto hace lo siguiente:

- Git busca el commit con el hash a1b2c3d (puede ser completo o abreviado).

- Actualiza tu área de trabajo (los archivos en el disco) al estado en que estaban en ese commit.

- Cambia el HEAD para que apunte directamente a ese commit, no a una rama.

    - Esto último significa que entramos en lo que se llama un **"detached HEAD"** (cabeza separada).

# ⚠️ Qué significa **“detached HEAD”**

- Significa que estamos viendo el repositorio tal como estaba en ese commit, pero no estamos en ninguna rama.

- Si hacemos nuevos commits desde ahí, no pertenecerán a ninguna rama (se perderán si no los guardamos en una nueva rama).

# 💡 Si quieremos trabajar desde ese commit

- Podemos crear una nueva rama desde ahí:

``` bash
git checkout -b nueva-rama a1b2c3d
```

- Así, los **commits** (confirmaciones) nuevos quedarán guardados en nueva-rama.

# 🧠 Ejemplo visual

``` css
A -- B -- C -- D (main)
```

Si hacemos:

``` css
git checkout B
```

- El repositorio se moverá al estado del commit **B**, pero el **HEAD** no estará en **main**, sino directamente sobre **B**.

# 3. `git checkout HEAD~5`

- Significa “muévete al commit que está 5 padres atrás desde `HEAD`”.

## Alternativa moderna con `git switch`

    `git switch --detach HEAD~5`

# 🧠 Resumen

| Comando                      | Qué hace                                                        |
| ---------------------------- | --------------------------------------------------------------- |
| `git checkout HEAD~5`        | ✅ Cambia al commit 5 padres atrás desde el actual              |
| `git switch --detach HEAD~5` | ✅ Alternativa moderna y más clara                              |
