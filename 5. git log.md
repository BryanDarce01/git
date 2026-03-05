# `git log`

Se usa para ver el **historial de confirmaciones** (commits) de un repositorio.

## 1. Muestra una lista detallada de los commits realizados en el repositorio.
### Por defecto incluye:

- El hash (identificador único) del commit
- El autor del commit
- La fecha
- El mensaje del commit

```sql
commit 4f8c3a921bd7f1e53f15a7d5c5a5f1bb4c6a1b3c
Author: Ana López <ana@example.com>
Date:   Tue Nov 2 14:32:01 2025 -0300

    Corrige error en la función de validación
```

# 2. `git log --oneline`

Este comando muestra el mismo historial, pero en una versión resumida en una sola línea por commit:

- Muestra el hash abreviado
- Muestra el mensaje del commit

```sql
4f8c3a9 Corrige error en la función de validación
b1d9a22 Añade pruebas unitarias
7e3c0a1 Actualiza README
```


# En resumen:
| Comando             | Descripción                 | Salida                               |
| ------------------- | --------------------------- | ------------------------------------ |
| `git log`           | Muestra historial detallado | Hash completo, autor, fecha, mensaje |
| `git log --oneline` | Muestra historial resumido  | Hash corto + mensaje en una línea    |


# 3. `git log --oneline --graph`

Muestra el historial resumido con un **gráfico ASCII** que representa la estructura de ramas y fusiones (branches y merges).

```markdown
* 4f8c3a9 Corrige error en la función de validación
| * b1d9a22 Añade pruebas unitarias
|/
* 7e3c0a1 Actualiza README
```

- Esto te permite visualizar las ramas y cómo se unieron (merge).

# 4. `git log --oneline --decorate`

Muestra los commits resumidos **junto con las etiquetas, ramas o referencias** que apuntan a ellos.

```css
4f8c3a9 (HEAD -> main, origin/main) Corrige error en la función de validación
b1d9a22 Añade pruebas unitarias
7e3c0a1 Actualiza README
```

- `HEAD -> main` indica la rama actual.
- `origin/main` muestra la rama remota correspondiente.

# 5. `git log --oneline --graph --decorate`

La combinación más popular y visual:

```css
* 4f8c3a9 (HEAD -> main, origin/main) Corrige error en la función de validación
| * 1a2b3c4 (feature/login) Crea formulario de login
|/
* 7e3c0a1 Inicializa repositorio
```

- Ideal para tener una visión clara y compacta del historial de ramas y merges.

# 6. `git log --since="2 weeks ago"` / `--until="2025-10-01"`

Filtra commits por fechas:

```bash
git log --oneline --since="2 weeks ago"
```

# 7. `git log --author="Ana"`

Filtra por autor:

```bash
git log --oneline --author="Ana"
```

- Solo muestra commits hechos por una persona específica.

# 8. `git log -p`

Muestra las **diferencias (diffs)** de cada commit, o sea, qué líneas de código se cambiaron:

```bash
git log -p
```

# 9. `git log --stat`

Muestra estadísticas resumidas de los cambios (cuántas líneas y archivos se modificaron):

```less
 main.py | 12 +++++++-----
 test.py |  3 +++
 2 files changed, 10 insertions(+), 5 deletions(-)
 ```
