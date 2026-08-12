---
title: "git credential-store"
source: "https://git-scm.com/docs/git-credential-store"
section: "scripting-and-helpers"
status: "source-audited"
version: "2.55.0"
---

# `git credential-store`

Este caso usa `git credential-store` para guardar credenciales sin cifrado en un archivo.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Estos comandos resuelven una parte del flujo y suelen comunicarse mediante entrada estándar, salida estándar, configuración o códigos de salida.

Define entrada, salida y código de retorno como contrato del proceso. No dependas de texto orientado a personas cuando exista un formato para scripts.

## Ejemplo mínimo

```bash
git config --global credential.helper store
```

La invocación `git credential-store` ejecuta esta operación: guardar credenciales sin cifrado en un archivo. Después, la salida y el código de retorno distinguen el caso aceptado del rechazado.

## Sintaxis y formas de invocación

```text
git config credential.helper 'store [<options>]'
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git credential-store [<options>] <action>
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git credential-store -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `--file`

Usa el archivo indicado en vez de la ubicación por defecto.

La opción cambia cómo `git credential-store` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git credential-store --file=archivo.txt
printf 'exit=%s\n' "$?"
```

El ejemplo usa `archivo.txt` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Páginas relacionadas

- [`git fmt-merge-msg`](../scripting-and-helpers/fmt-merge-msg.md)
- [`git credential-cache`](../scripting-and-helpers/credential-cache.md)
- [`git hook`](../scripting-and-helpers/hook.md)

## Fuente

- [git-credential-store - Helper to store credentials on disk](https://git-scm.com/docs/git-credential-store)
