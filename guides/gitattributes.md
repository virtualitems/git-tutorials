---
title: "gitattributes"
source: "https://git-scm.com/docs/gitattributes"
section: "guides"
status: "option-expanded"
---

# `gitattributes`

Este caso usa `gitattributes` para asignar atributos a rutas para diff, merge, exportación y filtros. Los nombres del ejemplo representan un repositorio de práctica. Sustitúyelos después de identificar qué objeto, referencia, ruta o valor de configuración representa cada uno.

La guía cubre **patrones y alcance**, **atributos `text` y `eol`**, **drivers de diff y merge**, **filtros `clean` y `smudge`**, **`export-ignore` y `export-subst`**.

## Responsabilidad y efecto

gitattributes define reglas compartidas por comandos, archivos y flujos de trabajo. Recibe como entrada el estado de repositorio representado por el caso. La operación consiste en asignar atributos a rutas para diff, merge, exportación y filtros.

La guía no ejecuta cambios. Un productor que implemente el formato o regla puede escribir la salida que su contrato defina.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

La guía conecta comandos con objetos, referencias, rutas y configuración. El ejemplo sirve para observar una relación antes de nombrar la regla.

Cambia un solo elemento del caso y vuelve a observar el repositorio. La diferencia identifica la regla que controla ese elemento.

## Ejemplo mínimo

```ini
# .gitattributes
*.txt text eol=lf
*.bin binary
docs/*.md diff=markdown
```

La invocación `gitattributes` ejecuta esta operación: asignar atributos a rutas para diff, merge, exportación y filtros. Después, los comandos de inspección permiten relacionar el resultado con objetos, referencias, rutas o configuración. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
# .gitattributes
*.txt text eol=lf
*.bin binary
docs/*.md diff=markdown
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa la fuente oficial enlazada para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

asignar atributos a rutas para diff, merge, exportación y filtros. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### patrones y alcance

Aplicar las reglas de patrones y alcance. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

### atributos `text` y `eol`

Aplicar las reglas de atributos `text` y `eol`. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

### drivers de diff y merge

Aplicar las reglas de drivers de diff y merge. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

### filtros `clean` y `smudge`

Aplicar las reglas de filtros `clean` y `smudge`. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

### `export-ignore` y `export-subst`

Aplicar las reglas de `export-ignore` y `export-subst`. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

## Funciones y reglas

### Patrones

Un patrón selecciona rutas; un patrón de directorio no recorre su contenido por sí solo.

```bash
git check-attr -a -- ruta
```

Ejecuta `git check-attr -a -- ruta`. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Texto

`text` controla normalización y `eol` fija el final de línea en checkout.

```bash
git show :ruta
```

Añade el archivo y compara el blob con `git show :ruta`. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Diff y merge

`diff=<driver>` y `merge=<driver>` asignan drivers configurados por nombre.

Consulta el atributo y provoca un diff o merge en el laboratorio. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Filtros

`filter=<driver>` conecta las acciones clean y smudge; clean afecta el contenido que entra al índice.

Compara archivo, índice y blob después de añadir. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Exportación

`export-ignore` excluye rutas y `export-subst` sustituye marcadores durante `git archive`.

```bash
git archive --format=tar HEAD > salida.tar
```

Lista el archivo generado por `git archive`. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

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

- [`gitcli`](../guides/gitcli.md)
- [`gitworkflows`](../guides/gitworkflows.md)
- [`githooks`](../guides/githooks.md)

## Fuente

- [gitattributes - Defining attributes per path](https://git-scm.com/docs/gitattributes)
