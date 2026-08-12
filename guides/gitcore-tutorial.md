---
title: "gitcore-tutorial"
source: "https://git-scm.com/docs/gitcore-tutorial"
section: "guides"
status: "option-expanded"
---

# `gitcore-tutorial`

Este caso usa `gitcore-tutorial` para construir commits con objetos, árboles, el índice y referencias. Los nombres del ejemplo representan un repositorio de práctica. Sustitúyelos después de identificar qué objeto, referencia, ruta o valor de configuración representa cada uno.

La guía cubre **objetos blob, tree y commit**, **índice**, **referencias y `HEAD`**, **creación de commits**, **recorrido del historial**.

## Responsabilidad y efecto

gitcore-tutorial define reglas compartidas por comandos, archivos y flujos de trabajo. Recibe como entrada el estado de repositorio representado por el caso. La operación consiste en construir commits con objetos, árboles, el índice y referencias.

La guía no ejecuta cambios. Un productor que implemente el formato o regla puede escribir la salida que su contrato defina.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

La guía conecta comandos con objetos, referencias, rutas y configuración. El ejemplo sirve para observar una relación antes de nombrar la regla.

Cambia un solo elemento del caso y vuelve a observar el repositorio. La diferencia identifica la regla que controla ese elemento.

## Ejemplo mínimo

```bash
blob=$(printf 'hola\n' | git hash-object -w --stdin)
printf '100644 blob %s\tREADME.md\n' "$blob" | git mktree
```

La invocación `gitcore-tutorial` ejecuta esta operación: construir commits con objetos, árboles, el índice y referencias. Después, los comandos de inspección permiten relacionar el resultado con objetos, referencias, rutas o configuración. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
blob=$(printf 'hola\n' | git hash-object -w --stdin)
printf '100644 blob %s\tREADME.md\n' "$blob" | git mktree
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa la fuente oficial enlazada para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

construir commits con objetos, árboles, el índice y referencias. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### objetos blob, tree y commit

Aplicar las reglas de objetos blob, tree y commit. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

### índice

Aplicar las reglas de índice. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

### referencias y `HEAD`

Aplicar las reglas de referencias y `HEAD`. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

### creación de commits

Aplicar las reglas de creación de commits. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

### recorrido del historial

Aplicar las reglas de recorrido del historial. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

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

Cada apartado usa una opción en una invocación concreta. Las opciones equivalentes comparten la explicación, pero cada alias tiene su propio ejemplo. Ejecuta una opción por vez antes de combinarlas.

### `-w`

Activa w durante construir commits con objetos, árboles, el índice y referencias. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `gitcore-tutorial`, w modifica la forma en que se ejecuta construir commits con objetos, árboles, el índice y referencias. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

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

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `gitcore-tutorial` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Errores y diagnóstico

### La regla no se aplica

Comprueba esta causa: El patrón, alcance o precedencia no coincide. Consulta la regla efectiva y el archivo que la definió.

### Una revisión se interpreta como ruta

Comprueba esta causa: El nombre es ambiguo. Separa revisiones y rutas con `--`.

### El resultado cambia entre equipos

Comprueba esta causa: La regla vive en configuración no compartida. Decide qué parte debe versionarse en el repositorio.

## Automatización y recuperación

Persistencia: La guía no ejecuta cambios. Un productor que implemente el formato o regla puede escribir la salida que su contrato defina. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

Reproduce el ejemplo en un repositorio temporal. Anota qué objeto, referencia, ruta o valor de configuración explica cada resultado.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`gitcredentials`](../guides/gitcredentials.md)
- [`gitcvs-migration`](../guides/gitcvs-migration.md)

## Fuente

- [gitcore-tutorial - A Git core tutorial for developers](https://git-scm.com/docs/gitcore-tutorial)
