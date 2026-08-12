---
title: "git mailsplit"
source: "https://git-scm.com/docs/git-mailsplit"
section: "scripting-and-helpers"
status: "source-audited"
version: "2.55.0"
---

# `git mailsplit`

Este caso usa `git mailsplit` para dividir un buzón mbox o Maildir en mensajes.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Estos comandos resuelven una parte del flujo y suelen comunicarse mediante entrada estándar, salida estándar, configuración o códigos de salida.

Define entrada, salida y código de retorno como contrato del proceso. No dependas de texto orientado a personas cuando exista un formato para scripts.

## Ejemplo mínimo

```bash
mkdir mensajes
git mailsplit -o mensajes serie.mbox
```

La invocación `git mailsplit -o mensajes serie.mbox` ejecuta esta operación: dividir un buzón mbox o Maildir en mensajes. Después, la salida y el código de retorno distinguen el caso aceptado del rechazado.

## Sintaxis y formas de invocación

```text
git mailsplit [-b] [-f<nn>] [-d<prec>] [--keep-cr] [--mboxrd]
		-o<directory> [--] [(<mbox>|<Maildir>)…]
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git mailsplit [-d<prec>] [-f<n>] [-b] [--keep-cr] -o<directory> [(<mbox>|<Maildir>)...]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git mailsplit -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `-b`

Activa b durante dividir un buzón mbox o Maildir en mensajes. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git mailsplit -b -o mensajes serie.mbox
printf 'exit=%s\n' "$?"
```

### `-f`

Activa f durante dividir un buzón mbox o Maildir en mensajes. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git mailsplit -f -o mensajes serie.mbox
printf 'exit=%s\n' "$?"
```

### `-d`

Activa d durante dividir un buzón mbox o Maildir en mensajes. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git mailsplit -d -o mensajes serie.mbox
printf 'exit=%s\n' "$?"
```

### `--keep-cr`

Conserva caracteres CR al procesar mensajes de correo.

```bash
git mailsplit --keep-cr -o mensajes serie.mbox
printf 'exit=%s\n' "$?"
```

### `--mboxrd`

Activa mboxrd durante dividir un buzón mbox o Maildir en mensajes. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git mailsplit --mboxrd -o mensajes serie.mbox
printf 'exit=%s\n' "$?"
```

### `-o`

Activa o durante dividir un buzón mbox o Maildir en mensajes. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git mailsplit -o mensajes serie.mbox
printf 'exit=%s\n' "$?"
```

## Páginas relacionadas

- [`git merge-one-file`](../scripting-and-helpers/merge-one-file.md)
- [`git mailinfo`](../scripting-and-helpers/mailinfo.md)
- [`git patch-id`](../scripting-and-helpers/patch-id.md)

## Fuente

- [git-mailsplit - Simple UNIX mbox splitter program](https://git-scm.com/docs/git-mailsplit)
