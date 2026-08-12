---
title: "gitmodules"
source: "https://git-scm.com/docs/gitmodules"
section: "guides"
status: "source-audited"
version: "2.55.0"
---

# `gitmodules`

Este caso usa `gitmodules` para declarar la ruta, URL y comportamiento de submódulos.

La guía cubre **declaración del submódulo**, **ruta y URL**, **rama**, **políticas de actualización**, **seguridad de configuración**.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

La guía conecta comandos con objetos, referencias, rutas y configuración. El ejemplo sirve para observar una relación antes de nombrar la regla.

Cambia un solo elemento del caso y vuelve a observar el repositorio. La diferencia identifica la regla que controla ese elemento.

## Ejemplo mínimo

```ini
[submodule "temas/base"]
    path = temas/base
    url = https://example.com/equipo/tema.git
```

La invocación `gitmodules` ejecuta esta operación: declarar la ruta, URL y comportamiento de submódulos. Después, los comandos de inspección permiten relacionar el resultado con objetos, referencias, rutas o configuración.

## Sintaxis y formas de invocación

```text
[submodule "temas/base"]
    path = temas/base
    url = https://example.com/equipo/tema.git
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa la fuente oficial enlazada para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

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

## Páginas relacionadas

- [`gitrepository-layout`](../guides/gitrepository-layout.md)
- [`gitmailmap`](../guides/gitmailmap.md)
- [`gitrevisions`](../guides/gitrevisions.md)

## Fuente

- [gitmodules - Defining submodule properties](https://git-scm.com/docs/gitmodules)
