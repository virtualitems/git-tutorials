---
title: "git url-parse"
source: "https://git-scm.com/docs/git-url-parse"
section: "scripting-and-helpers"
status: "source-audited"
version: "2.55.0"
---

# `git url-parse`

Este caso usa `git url-parse` para extraer componentes de una URL aceptada por Git.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Estos comandos resuelven una parte del flujo y suelen comunicarse mediante entrada estándar, salida estándar, configuración o códigos de salida.

Define entrada, salida y código de retorno como contrato del proceso. No dependas de texto orientado a personas cuando exista un formato para scripts.

## Ejemplo mínimo

```bash
git url-parse -c host https://example.com/equipo/biblioteca.git
```

La invocación `git url-parse -c host https://example.com/equipo/biblioteca.git` ejecuta esta operación: extraer componentes de una URL aceptada por Git. Después, la salida y el código de retorno distinguen el caso aceptado del rechazado.

## Sintaxis y formas de invocación

```text
git url-parse [-c <component>] [--] <url>…
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git url-parse -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `-c`

Aplica una clave de configuración solo a esta invocación.

```bash
git url-parse -c host https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

### `--help`

Muestra la ayuda correspondiente a la versión instalada.

```bash
git url-parse --help
printf 'exit=%s\n' "$?"
```

### `--component` y `-c`

Extraen un componente de cada URL: `scheme`, `user`, `password`, `host`, `port` o `path`. Cada resultado ocupa una línea; si la URL carece del componente, la línea queda vacía. Sin esta opción, el comando solo valida y no escribe salida.

```bash
git url-parse --component host \
  'https://usuario@example.com:8443/equipo/proyecto.git'
```

La salida es `example.com`. Usa `--component port` con la misma URL para obtener `8443`.

## Páginas relacionadas

- [`git stripspace`](../scripting-and-helpers/stripspace.md)
- [`git sh-setup`](../scripting-and-helpers/sh-setup.md)

## Fuente

- [git-url-parse - Parse and extract git URL components](https://git-scm.com/docs/git-url-parse)
