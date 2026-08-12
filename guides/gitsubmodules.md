---
title: "gitsubmodules"
source: "https://git-scm.com/docs/gitsubmodules"
section: "guides"
status: "source-audited"
version: "2.55.0"
---

# `gitsubmodules`

Este caso usa `gitsubmodules` para entender el modelo de repositorios anidados como submódulos.

La guía cubre **gitlink y `.gitmodules`**, **inicialización**, **actualización**, **cambios locales**, **recursión y seguridad**.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

La guía conecta comandos con objetos, referencias, rutas y configuración. El ejemplo sirve para observar una relación antes de nombrar la regla.

Cambia un solo elemento del caso y vuelve a observar el repositorio. La diferencia identifica la regla que controla ese elemento.

## Ejemplo mínimo

```bash
superproyecto/.gitmodules
superproyecto/temas/base/.git
```

La invocación `gitsubmodules` ejecuta esta operación: entender el modelo de repositorios anidados como submódulos. Después, los comandos de inspección permiten relacionar el resultado con objetos, referencias, rutas o configuración.

## Sintaxis y formas de invocación

```text
.gitmodules, $GIT_DIR/config
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa la fuente oficial enlazada para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

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

## Páginas relacionadas

- [`gittutorial`](../guides/gittutorial.md)
- [`gitremote-helpers`](../guides/gitremote-helpers.md)
- [`gittutorial-2`](../guides/gittutorial-2.md)

## Fuente

- [gitsubmodules - Mounting one repository inside another](https://git-scm.com/docs/gitsubmodules)
