---
title: "git fast-export"
source: "https://git-scm.com/docs/git-fast-export"
section: "external-systems"
status: "source-audited"
version: "2.55.0"
---

# `git fast-export`

Este caso usa `git fast-export` para emitir historial y referencias en un flujo para migración.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

La integración traduce identidades, ramas y cambios entre dos modelos de control de versiones. Una migración se valida comparando historial, contenido y referencias en el destino.

Define una regla para autores, ramas, etiquetas y finales de línea antes de importar. Valida cada regla con un conjunto que contenga ese caso.

## Ejemplo mínimo

```bash
git fast-export --all > historial.fi
```

La invocación `git fast-export --all > historial.fi` ejecuta esta operación: emitir historial y referencias en un flujo para migración. Después, el destino conserva el contenido, autores, ramas y etiquetas que admita la conversión.

## Sintaxis y formas de invocación

```text
git fast-export [<options>] | git fast-import
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git fast-export [<rev-list-opts>]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git fast-export -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `--progress`

Muestra progreso aunque la salida no sea un terminal.

```bash
git fast-export --progress=5 --all > historial.fi
printf 'exit=%s\n' "$?"
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--signed-tags`

Selecciona o modifica referencias dentro del alcance de la orden.

```bash
git fast-export --signed-tags=all --all > historial.fi
printf 'exit=%s\n' "$?"
```

El ejemplo usa `all` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--signed-commits`

Define firmado commits para esta ejecución de `git fast-export`. En Git 2.51.1, la ayuda corta expresa el contrato como `select handling of signed commits`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git fast-export --signed-commits=all --all > historial.fi
printf 'exit=%s\n' "$?"
```

El ejemplo usa `all` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--tag-of-filtered-object`

Selecciona o modifica referencias dentro del alcance de la orden.

```bash
git fast-export --tag-of-filtered-object=all --all > historial.fi
printf 'exit=%s\n' "$?"
```

El ejemplo usa `all` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--reencode`

Define reencode para esta ejecución de `git fast-export`. En Git 2.51.1, la ayuda corta expresa el contrato como `select handling of commit messages in an alternate encoding`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git fast-export --reencode=all --all > historial.fi
printf 'exit=%s\n' "$?"
```

El ejemplo usa `all` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--export-marks`

Activa export marks durante emitir historial y referencias en un flujo para migración. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `dump marks to this file`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia cómo `git fast-export` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git fast-export --export-marks=rutas.txt --all > historial.fi
printf 'exit=%s\n' "$?"
```

El ejemplo usa `rutas.txt` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--import-marks`

Activa import marks durante emitir historial y referencias en un flujo para migración. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `import marks from this file`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia cómo `git fast-export` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git fast-export --import-marks=rutas.txt --all > historial.fi
printf 'exit=%s\n' "$?"
```

El ejemplo usa `rutas.txt` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--import-marks-if-exists`

Activa import marks if exists durante emitir historial y referencias en un flujo para migración. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `import marks from this file if it exists`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia cómo `git fast-export` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git fast-export --import-marks-if-exists=rutas.txt --all > historial.fi
printf 'exit=%s\n' "$?"
```

El ejemplo usa `rutas.txt` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--fake-missing-tagger`

Activa fake missing tagger durante emitir historial y referencias en un flujo para migración. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `fake a tagger when tags lack one`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git fast-export --fake-missing-tagger --all > historial.fi
printf 'exit=%s\n' "$?"
```

### `--full-tree`

Incluye full tree en la salida o cambia cómo `git fast-export` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `output full tree for each commit`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git fast-export --full-tree --all > historial.fi
printf 'exit=%s\n' "$?"
```

### `--use-done-feature`

Define use done feature para esta ejecución de `git fast-export`. En Git 2.51.1, la ayuda corta expresa el contrato como `use the done feature to terminate the stream`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git fast-export --use-done-feature --all > historial.fi
printf 'exit=%s\n' "$?"
```

### `--data`

Selecciona la relación indicada por data; la ayuda de Git la define respecto de otra forma equivalente u opuesta. En Git 2.51.1, la ayuda corta expresa el contrato como `opposite of --no-data`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git fast-export --data --all > historial.fi
printf 'exit=%s\n' "$?"
```

### `--refspec`

Activa refspec durante emitir historial y referencias en un flujo para migración. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `apply refspec to exported refs`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git fast-export --refspec=main --all > historial.fi
printf 'exit=%s\n' "$?"
```

El ejemplo usa `main` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--anonymize`

Incluye anonymize en la salida o cambia cómo `git fast-export` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `anonymize output`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git fast-export --anonymize --all > historial.fi
printf 'exit=%s\n' "$?"
```

### `--anonymize-map`

Incluye anonymize map en la salida o cambia cómo `git fast-export` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `convert <from> to <to> in anonymized output`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git fast-export --anonymize-map=valor --all > historial.fi
printf 'exit=%s\n' "$?"
```

### `--reference-excluded-parents`

Activa reference excluded parents durante emitir historial y referencias en un flujo para migración. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `reference parents which are not in fast-export stream by object id`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git fast-export --reference-excluded-parents --all > historial.fi
printf 'exit=%s\n' "$?"
```

### `--show-original-ids`

Incluye información adicional en la salida.

```bash
git fast-export --show-original-ids --all > historial.fi
printf 'exit=%s\n' "$?"
```

### `--mark-tags`

Selecciona o modifica referencias dentro del alcance de la orden.

```bash
git fast-export --mark-tags --all > historial.fi
printf 'exit=%s\n' "$?"
```

## Páginas relacionadas

- [`git fast-import`](../external-systems/fast-import.md)
- [`git cvsserver`](../external-systems/cvsserver.md)
- [`git p4`](../external-systems/p4.md)

## Fuente

- [git-fast-export - Git data exporter](https://git-scm.com/docs/git-fast-export)
