---
title: "git mailinfo"
source: "https://git-scm.com/docs/git-mailinfo"
section: "scripting-and-helpers"
status: "source-audited"
version: "2.55.0"
---

# `git mailinfo`

Este caso usa `git mailinfo` para separar metadatos, mensaje y parche de un correo.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Estos comandos resuelven una parte del flujo y suelen comunicarse mediante entrada estándar, salida estándar, configuración o códigos de salida.

Define entrada, salida y código de retorno como contrato del proceso. No dependas de texto orientado a personas cuando exista un formato para scripts.

## Ejemplo mínimo

```bash
git mailinfo mensaje.txt cambio.patch < correo.eml
```

La invocación `git mailinfo mensaje.txt cambio.patch < correo.eml` ejecuta esta operación: separar metadatos, mensaje y parche de un correo. Después, la salida y el código de retorno distinguen el caso aceptado del rechazado.

## Sintaxis y formas de invocación

```text
git mailinfo [-k|-b] [-u | --encoding=<encoding> | -n]
	       [--[no-]scissors] [--quoted-cr=<action>]
	       <msg> <patch>
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git mailinfo [<options>] <msg> <patch> < mail >info
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git mailinfo -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `-k`

Activa k durante separar metadatos, mensaje y parche de un correo. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `keep subject`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git mailinfo -k mensaje.txt cambio.patch < correo.eml
printf 'exit=%s\n' "$?"
```

### `-b`

Activa b durante separar metadatos, mensaje y parche de un correo. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `keep non patch brackets in subject`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git mailinfo -b mensaje.txt cambio.patch < correo.eml
printf 'exit=%s\n' "$?"
```

### `-u`

Activa u durante separar metadatos, mensaje y parche de un correo. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `re-code metadata to i18n.commitEncoding`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git mailinfo -u mensaje.txt cambio.patch < correo.eml
printf 'exit=%s\n' "$?"
```

### `--encoding`

Activa encoding durante separar metadatos, mensaje y parche de un correo. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git mailinfo --encoding=valor mensaje.txt cambio.patch < correo.eml
printf 'exit=%s\n' "$?"
```

### `-n`

Impide n durante esta invocación de `git mailinfo`. En Git 2.51.1, la ayuda corta expresa el contrato como `disable charset re-coding of metadata`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git mailinfo -n mensaje.txt cambio.patch < correo.eml
printf 'exit=%s\n' "$?"
```

### `--scissors`

Reconoce la línea scissors y descarta el contenido anterior según el formato de correo. En Git 2.51.1, la ayuda corta expresa el contrato como `use scissors`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git mailinfo --scissors mensaje.txt cambio.patch < correo.eml
printf 'exit=%s\n' "$?"
```

### `--quoted-cr`

Define cómo se tratan los caracteres CR que aparecen al final de líneas citadas. En Git 2.51.1, la ayuda corta expresa el contrato como `action when quoted CR is found`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git mailinfo --quoted-cr=warn mensaje.txt cambio.patch < correo.eml
printf 'exit=%s\n' "$?"
```

El ejemplo usa `warn` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-m` y `--message-id`

Añade el identificador del mensaje de correo al mensaje de commit.  La misma línea de ayuda también acepta `-m` y `-ID`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

#### Ejemplo con `--message-id`

```bash
git mailinfo --message-id mensaje.txt cambio.patch < correo.eml
printf 'exit=%s\n' "$?"
```

## Páginas relacionadas

- [`git mailsplit`](../scripting-and-helpers/mailsplit.md)
- [`git interpret-trailers`](../scripting-and-helpers/interpret-trailers.md)
- [`git merge-one-file`](../scripting-and-helpers/merge-one-file.md)

## Fuente

- [git-mailinfo - Extracts patch and authorship from a single e-mail message](https://git-scm.com/docs/git-mailinfo)
