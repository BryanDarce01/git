# fast-forward

Es una forma de hacer un **merge** (fusión) sin crear un commit nuevo, simplemente moviendo el puntero de la rama.

## ¿Qué significa exactamente?

Imaginemos esto:

```

A---B---C   (main)
         \
          D---E   (feature)

```
Si estamos en main y hacemos:

```

git merge feature

```
- Git ve que `main` no tiene cambios nuevos desde que creamos `feature`, entonces puede hacer un `fast-forward`:

```

A---B---C---D---E   (main, feature)

```

Lo único que pasó fue:

- `main` avanzó (se “movió”) hasta donde está feature

- No se creó un `commit` de `merge`

## Cuándo ocurre un fast-forward?

Ocurre cuando:

- La rama destino (`main`) no tiene `commits` nuevos

- Todo el historial es lineal

En otras palabras: **no hay conflictos ni caminos separados**

## ¿Cuándo NO ocurre?

Si tenemos esto:

```

A---B---C   (main)
     \
      D---E   (feature)

```

Y además `main` avanzó:

```

A---B---C---F   (main)
     \
      D---E   (feature)

```
Ahora si hacemos `merge`:

```

git merge feature

```
- Git NO puede hacer `fast-forward`, entonces crea un `commit`de `merge`:

```

A---B---C---F-------G   (main)
     \         /
      D---E---         (feature)

```