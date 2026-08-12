---
title: "gitsubmodules"
source: "https://git-scm.com/docs/gitsubmodules"
section: "guides"
status: "option-expanded"
---

# `gitsubmodules`

Este caso usa `gitsubmodules` para entender el modelo de repositorios anidados como submódulos. Los nombres del ejemplo representan un repositorio de práctica. Sustitúyelos después de identificar qué objeto, referencia, ruta o valor de configuración representa cada uno.

La guía cubre **gitlink y `.gitmodules`**, **inicialización**, **actualización**, **cambios locales**, **recursión y seguridad**.

## Responsabilidad y efecto

gitsubmodules define reglas compartidas por comandos, archivos y flujos de trabajo. Recibe como entrada el estado de repositorio representado por el caso. La operación consiste en entender el modelo de repositorios anidados como submódulos.

La guía no ejecuta cambios. Un productor que implemente el formato o regla puede escribir la salida que su contrato defina.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

La guía conecta comandos con objetos, referencias, rutas y configuración. El ejemplo sirve para observar una relación antes de nombrar la regla.

Cambia un solo elemento del caso y vuelve a observar el repositorio. La diferencia identifica la regla que controla ese elemento.

## Ejemplo mínimo

```bash
superproyecto/.gitmodules
superproyecto/temas/base/.git
```

La invocación `gitsubmodules` ejecuta esta operación: entender el modelo de repositorios anidados como submódulos. Después, los comandos de inspección permiten relacionar el resultado con objetos, referencias, rutas o configuración. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
.gitmodules, $GIT_DIR/config
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa la fuente oficial enlazada para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

entender el modelo de repositorios anidados como submódulos. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### gitlink y `.gitmodules`

Aplicar las reglas de gitlink y `.gitmodules`. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

### inicialización

Aplicar las reglas de inicialización. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

### actualización

Aplicar las reglas de actualización. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

### cambios locales

Aplicar las reglas de cambios locales. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

### recursión y seguridad

Aplicar las reglas de recursión y seguridad. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

## Funciones y reglas

### Gitlink

El superproyecto registra el commit del submódulo como una entrada de modo 160000.

```bash
git ls-tree HEAD ruta
```

Usa `git ls-tree HEAD ruta`. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Declaración

`.gitmodules` aporta ruta, URL y configuración compartida.

```bash
git config -f
```

Consulta el archivo con `git config -f`. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Inicialización

Init copia configuración permitida a la configuración local.

Compara valores antes y después. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Actualización

Update materializa el commit del gitlink, no cualquier tip remoto.

Compara `rev-parse HEAD` dentro del submódulo con `ls-tree`. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Recursión

Las opciones recurse-submodules propagan operaciones bajo reglas de cada comando.

Prueba un submódulo con cambios locales. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

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

- [`gittutorial`](../guides/gittutorial.md)
- [`gitremote-helpers`](../guides/gitremote-helpers.md)
- [`gittutorial-2`](../guides/gittutorial-2.md)

## Fuente

- [gitsubmodules - Mounting one repository inside another](https://git-scm.com/docs/gitsubmodules)
