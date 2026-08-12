---
title: "gitweb"
source: "https://git-scm.com/docs/gitweb"
section: "graphical-tools"
status: "source-audited"
version: "2.55.0"
---

# `gitweb`

Este caso usa `gitweb` para publicar repositorios mediante una interfaz web.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

La interfaz presenta operaciones que también existen en el modelo de objetos, índice, referencias y commits. La vista cambia; el repositorio conserva el mismo estado.

Relaciona cada acción de la interfaz con índice, commit o referencia. Usa una consulta de Git para comprobar el cambio de estado.

## Ejemplo mínimo

```bash
GITWEB_CONFIG=/etc/gitweb.conf gitweb.cgi
```

La invocación `gitweb` ejecuta esta operación: publicar repositorios mediante una interfaz web. Después, los comandos de consulta confirman el mismo estado que presenta la interfaz.

## Sintaxis y formas de invocación

```text
GITWEB_CONFIG=/etc/gitweb.conf gitweb.cgi
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa la fuente oficial enlazada para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Páginas relacionadas

- [`gitk`](../graphical-tools/gitk.md)
- [`git instaweb`](../graphical-tools/instaweb.md)

## Fuente

- [gitweb - Git web interface (web frontend to Git repositories)](https://git-scm.com/docs/gitweb)
