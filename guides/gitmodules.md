---
title: "gitmodules"
source: "https://git-scm.com/docs/gitmodules"
section: "guides"
status: "option-expanded"
---

# `gitmodules`

Este caso usa `gitmodules` para declarar la ruta, URL y comportamiento de submódulos. Los nombres del ejemplo representan un repositorio de práctica. Sustitúyelos después de identificar qué objeto, referencia, ruta o valor de configuración representa cada uno.

La guía cubre **declaración del submódulo**, **ruta y URL**, **rama**, **políticas de actualización**, **seguridad de configuración**.

## Responsabilidad y efecto

gitmodules define reglas compartidas por comandos, archivos y flujos de trabajo. Recibe como entrada el estado de repositorio representado por el caso. La operación consiste en declarar la ruta, URL y comportamiento de submódulos.

La guía no ejecuta cambios. Un productor que implemente el formato o regla puede escribir la salida que su contrato defina.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

La guía conecta comandos con objetos, referencias, rutas y configuración. El ejemplo sirve para observar una relación antes de nombrar la regla.

Cambia un solo elemento del caso y vuelve a observar el repositorio. La diferencia identifica la regla que controla ese elemento.

## Ejemplo mínimo

```ini
[submodule "temas/base"]
    path = temas/base
    url = https://example.test/equipo/tema.git
```

La invocación `gitmodules` ejecuta esta operación: declarar la ruta, URL y comportamiento de submódulos. Después, los comandos de inspección permiten relacionar el resultado con objetos, referencias, rutas o configuración. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
[submodule "temas/base"]
    path = temas/base
    url = https://example.test/equipo/tema.git
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa la fuente oficial enlazada para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

declarar la ruta, URL y comportamiento de submódulos. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### declaración del submódulo

Aplicar las reglas de declaración del submódulo. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

### ruta y URL

Aplicar las reglas de ruta y URL. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

### rama

Aplicar las reglas de rama. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

### políticas de actualización

Aplicar las reglas de políticas de actualización. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

### seguridad de configuración

Aplicar las reglas de seguridad de configuración. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

## Funciones y reglas

### Sección

Cada submódulo tiene una sección con nombre y una ruta única.

```bash
git config -f .gitmodules --get-regexp
```

Ejecuta `git config -f .gitmodules --get-regexp`. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### URL

La URL puede ser absoluta o relativa a la ubicación del superproyecto.

Resuelve la URL desde un clone de prueba. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Rama

La clave branch orienta qué rama seguir en operaciones que lo solicitan.

Compara con el gitlink registrado. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Update

La política update controla cómo se materializa el commit del gitlink.

Prueba checkout en un submódulo sin cambios. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Seguridad

Configuración que ejecuta comandos no se copia de `.gitmodules` a configuración sin validación.

Inspecciona la configuración local después de init. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

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

- [`gitrepository-layout`](../guides/gitrepository-layout.md)
- [`gitmailmap`](../guides/gitmailmap.md)
- [`gitrevisions`](../guides/gitrevisions.md)

## Fuente

- [gitmodules - Defining submodule properties](https://git-scm.com/docs/gitmodules)
