# `git switch`
Es un comando moderno (introducido en Git 2.23) que sirve para moverse **entre ramas o commits**, de una manera más clara y segura que git checkout.

# ⚙️ Sintaxis general

``` bash
git switch [opciones] <nombre-rama>
```

# 🚀 Usos más comunes

# 1. Cambiar a una rama existente

``` bash
git switch main
```

- Mueve el HEAD y el área de trabajo a la rama **main**.

- **Git** actualiza los archivos para que coincidan con el último commit de esa rama.

# 2. Crear y moverte a una nueva rama

``` bash
git switch -c nombre-nueva-rama
```

- Equivale a ` git checkout -b nombre-nueva-rama`.

## Ejemplo:

``` bash
git switch -c feature/login
```

- Crea la rama `feature/login` y te cambia a ella de inmediato.

# 3. Cambiar a un commit específico (modo **“detached HEAD”**)

``` bash
git switch --detach <commit-hash>
```

- Esto te mueve a un commit específico sin estar en una rama.

- Equivale a ` git checkout <hash> `

``` bash
git switch --detach a1b2c3d
```

**HEAD** ahora apunta directamente a ese commit (modo **“detached”**), útil para inspeccionar versiones anteriores.

# 4. Cambiar de rama y crearla desde otra base

Se puede especificar desde qué commit o rama que se quiera crear:

``` bash
git switch -c nueva-rama base-rama-o-commit
```

## Ejemplo:

``` bash
git switch -c hotfix/login bugfix
```

- Crea `hotfix/login` a partir de la rama `bugfix`.

# 5. Forzar el cambio de rama ignorando cambios locales

Si tienhayes cambios sin confirmar y Git no deja cambiar de rama:

``` bash
git switch -f otra-rama
```

👉 Esto descarta los cambios locales que entren en conflicto.

⚠️ **Cuidado**: se puede perder trabajo no guardado.

# 6. Volver a la rama anterior rápidamente

``` bash
git switch -
```

- Nos lleva de vuelta a la última rama en la que estabas (como un “volver atrás”).

- Muy útil si saltas entre dos ramas a menudo.

# 🧠 En resumen:

| Acción                                    | Comando                        |
| :---------------------------------------- | :----------------------------- |
| Cambiar de rama                           | `git switch <rama>`            |
| Crear y cambiar a una nueva rama          | `git switch -c <rama>`         |
| Cambiar a un commit específico (detached) | `git switch --detach <hash>`   |
| Crear rama desde otra base                | `git switch -c <nueva> <base>` |
| Forzar cambio descartando cambios         | `git switch -f <rama>`         |
| Volver a la última rama                   | `git switch -`                 |


# 💬 Consejo práctico

- Usar `git switch` para moverse entre contextos de trabajo (ramas o commits).

- Usa `git restore` si quiremos revertir archivos o descartar cambios locales.

- Evitar `git checkout` salvo que trabajemos con versiones antiguas de Git.