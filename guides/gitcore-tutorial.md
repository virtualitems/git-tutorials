---
title: "gitcore-tutorial"
source: "https://git-scm.com/docs/gitcore-tutorial"
section: "guides"
status: "source-audited"
version: "2.55.0"
---

# `gitcore-tutorial`

Este caso usa `gitcore-tutorial` para construir commits con objetos, árboles, el índice y referencias.

La guía cubre **objetos blob, tree y commit**, **índice**, **referencias y `HEAD`**, **creación de commits**, **recorrido del historial**.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

La guía conecta comandos con objetos, referencias, rutas y configuración. El ejemplo sirve para observar una relación antes de nombrar la regla.

Cambia un solo elemento del caso y vuelve a observar el repositorio. La diferencia identifica la regla que controla ese elemento.

## Ejemplo mínimo

```bash
blob=$(printf 'hola\n' | git hash-object -w --stdin)
printf '100644 blob %s\tREADME.md\n' "$blob" | git mktree
```

La invocación `gitcore-tutorial` ejecuta esta operación: construir commits con objetos, árboles, el índice y referencias. Después, los comandos de inspección permiten relacionar el resultado con objetos, referencias, rutas o configuración.

## Sintaxis y formas de invocación

```text
blob=$(printf 'hola\n' | git hash-object -w --stdin)
printf '100644 blob %s\tREADME.md\n' "$blob" | git mktree
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa la fuente oficial enlazada para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Funciones y reglas

### Blob

El blob guarda contenido y no guarda el nombre de ruta.

```bash
git hash-object -w
```

Crea un blob con `git hash-object -w` y consulta su tipo. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Tree

El tree asocia nombre y modo con otro objeto.

```bash
git ls-tree
```

Usa `git ls-tree` sobre el tree de `HEAD`. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Índice

El índice prepara las entradas que `write-tree` convierte en un tree.

```bash
git ls-files --stage
```

Compara `git ls-files --stage` con `git ls-tree HEAD`. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Commit

El commit apunta a un tree, padres y metadatos.

```bash
git cat-file -p HEAD
```

Ejecuta `git cat-file -p HEAD`. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Referencia

Una referencia conserva un nombre que resuelve a un objeto; `HEAD` puede ser simbólica.

```bash
git symbolic-ref HEAD
```

Compara `git symbolic-ref HEAD` y `git rev-parse HEAD`. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `-w`

Activa w durante construir commits con objetos, árboles, el índice y referencias. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
blob=$(printf 'hola\n' | git hash-object -w --stdin)
printf 'exit=%s\n' "$?"
```

El ejemplo usa `--stdin)` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--stdin`

Lee registros o nombres desde la entrada estándar.

La opción cambia cómo `gitcore-tutorial` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
gitcore-tutorial --stdin
printf 'exit=%s\n' "$?"
```

## Páginas relacionadas

- [`gitcredentials`](../guides/gitcredentials.md)
- [`gitcvs-migration`](../guides/gitcvs-migration.md)

## Fuente

- [gitcore-tutorial - A Git core tutorial for developers](https://git-scm.com/docs/gitcore-tutorial)
