---
title: "gitnamespaces"
source: "https://git-scm.com/docs/gitnamespaces"
section: "guides"
status: "option-expanded"
---

# `gitnamespaces`

Este caso usa `gitnamespaces` para aislar conjuntos de referencias dentro de un repositorio servidor. Los nombres del ejemplo representan un repositorio de práctica. Sustitúyelos después de identificar qué objeto, referencia, ruta o valor de configuración representa cada uno.

La guía cubre **aislamiento de referencias**, **selección de namespace**, **servicios de transporte**, **alcance de objetos**, **operación en servidor**.

## Responsabilidad y efecto

gitnamespaces define reglas compartidas por comandos, archivos y flujos de trabajo. Recibe como entrada el estado de repositorio representado por el caso. La operación consiste en aislar conjuntos de referencias dentro de un repositorio servidor.

La guía no ejecuta cambios. Un productor que implemente el formato o regla puede escribir la salida que su contrato defina.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

La guía conecta comandos con objetos, referencias, rutas y configuración. El ejemplo sirve para observar una relación antes de nombrar la regla.

Cambia un solo elemento del caso y vuelve a observar el repositorio. La diferencia identifica la regla que controla ese elemento.

## Ejemplo mínimo

```bash
GIT_NAMESPACE=curso-a git upload-pack /srv/git/biblioteca.git
GIT_NAMESPACE=curso-b git upload-pack /srv/git/biblioteca.git
```

La invocación `gitnamespaces` ejecuta esta operación: aislar conjuntos de referencias dentro de un repositorio servidor. Después, los comandos de inspección permiten relacionar el resultado con objetos, referencias, rutas o configuración. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
GIT_NAMESPACE=<namespace> git upload-pack
GIT_NAMESPACE=<namespace> git receive-pack
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa la fuente oficial enlazada para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

aislar conjuntos de referencias dentro de un repositorio servidor. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### aislamiento de referencias

Aplicar las reglas de aislamiento de referencias. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

### selección de namespace

Aplicar las reglas de selección de namespace. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

### servicios de transporte

Aplicar las reglas de servicios de transporte. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

### alcance de objetos

Aplicar las reglas de alcance de objetos. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

### operación en servidor

Aplicar las reglas de operación en servidor. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

## Funciones y reglas

### Prefijo

Un namespace inserta un prefijo interno en las referencias visibles.

```bash
git show-ref
```

Compara `git show-ref` con y sin `GIT_NAMESPACE`. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Objetos

Los objetos se comparten aunque las referencias queden separadas.

Resuelve un hash conocido bajo dos namespaces. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Transporte

Los procesos de servidor pueden seleccionar namespace por solicitud o configuración.

Clona dos vistas desde un servidor de prueba. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### HEAD

Cada namespace puede exponer referencias distintas y requiere un HEAD coherente.

Consulta el anuncio de referencias. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Administración

Eliminar un namespace afecta sus referencias, no implica borrar de inmediato objetos compartidos.

Ejecuta fsck antes de mantenimiento. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

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

- [`gitremote-helpers`](../guides/gitremote-helpers.md)
- [`gitglossary`](../guides/gitglossary.md)
- [`gitsubmodules`](../guides/gitsubmodules.md)

## Fuente

- [gitnamespaces - Git namespaces](https://git-scm.com/docs/gitnamespaces)
