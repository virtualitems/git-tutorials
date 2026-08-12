---
title: "git fast-import"
source: "https://git-scm.com/docs/git-fast-import"
section: "external-systems"
status: "option-expanded"
---

# `git fast-import`

Este caso usa `git fast-import` para crear historial y referencias a partir de un flujo de importación. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Responsabilidad y efecto

git fast-import traduce historial, referencias e identidades entre Git y otro sistema. Recibe como entrada la ubicación y los nombres que deben traducirse desde el sistema de origen. La operación consiste en crear historial y referencias a partir de un flujo de importación.

Puede persistir el estado implicado por esta operación: crear historial y referencias a partir de un flujo de importación. Las opciones pueden limitar o ampliar ese efecto.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). La posición de opciones, revisiones y rutas sigue las [convenciones de la interfaz de Git](../guides/gitcli.md#convenciones-de-la-cli). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

La integración traduce identidades, ramas y cambios entre dos modelos de control de versiones. Una migración se valida comparando historial, contenido y referencias en el destino.

Define una regla para autores, ramas, etiquetas y finales de línea antes de importar. Valida cada regla con un conjunto que contenga ese caso.

## Ejemplo mínimo

```bash
git init destino
cd destino
git fast-import < ../historial.fi
```

La invocación `git fast-import < ../historial.fi` ejecuta esta operación: crear historial y referencias a partir de un flujo de importación. Después, el destino conserva el contenido, autores, ramas y etiquetas que admita la conversión. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
frontend | git fast-import [<options>]
```

### Uso verificado con `git version 2.51.1`

```text
git fast-import [--date-format=<f>] [--max-pack-size=<n>] [--big-file-threshold=<n>] [--depth=<n>] [--active-branches=<n>] [--export-marks=<marks.file>]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git fast-import -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

crear historial y referencias a partir de un flujo de importación. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### Alcance explícito

Aplicar git fast-import a una referencia, rango o ruta identificada. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Resuelve cada argumento antes de ejecutar y usa `--` para rutas.

### Validación

Comprobar el resultado de git fast-import con una orden de lectura independiente. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. No uses la misma salida como única prueba del cambio.

## Opciones

Cada apartado usa una opción en una invocación concreta. Las opciones equivalentes comparten la explicación, pero cada alias tiene su propio ejemplo. Ejecuta una opción por vez antes de combinarlas.

### `--date-format`

Activa fecha formato durante crear historial y referencias a partir de un flujo de importación. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git fast-import --date-format < ../historial.fi
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fast-import` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--max-pack-size`

Establece un límite numérico para la selección o el recorrido.

En `git fast-import`, máximo pack size modifica la forma en que se ejecuta crear historial y referencias a partir de un flujo de importación. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git fast-import --max-pack-size < ../historial.fi
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fast-import` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--big-file-threshold`

Selecciona un archivo de entrada o salida según la posición indicada en la sintaxis.

La opción cambia cómo `git fast-import` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git fast-import --big-file-threshold < ../historial.fi
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fast-import` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--depth`

Establece un límite numérico para la selección o el recorrido.

En `git fast-import`, profundidad modifica la forma en que se ejecuta crear historial y referencias a partir de un flujo de importación. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git fast-import --depth < ../historial.fi
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fast-import` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--active-branches`

Selecciona o modifica referencias dentro del alcance de la orden.

La opción limita o amplía el conjunto sobre el que se ejecuta crear historial y referencias a partir de un flujo de importación. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git fast-import --active-branches < ../historial.fi
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fast-import` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--export-marks`

Activa export marks durante crear historial y referencias a partir de un flujo de importación. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git fast-import`, export marks modifica la forma en que se ejecuta crear historial y referencias a partir de un flujo de importación. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git fast-import --export-marks < ../historial.fi
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fast-import` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Errores y diagnóstico

### Faltan revisiones

Comprueba esta causa: El rango, rama o marcador de importación las excluye. Compara conteos y el último identificador importado.

### La identidad cambia

Comprueba esta causa: No existe una regla de mapeo estable. Define el mapa antes de repetir la importación.

### La sincronización duplica cambios

Comprueba esta causa: Se perdió el marcador entre sistemas. Restaura el punto de control y prueba sobre una copia.

## Automatización y recuperación

Persistencia: Puede persistir el estado implicado por esta operación: crear historial y referencias a partir de un flujo de importación. Las opciones pueden limitar o ampliar ese efecto. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

Importa un conjunto de prueba con dos autores, dos ramas y una etiqueta. Compara cantidades, nombres y contenido en el destino.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git p4`](../external-systems/p4.md)
- [`git fast-export`](../external-systems/fast-export.md)
- [`git quiltimport`](../external-systems/quiltimport.md)

## Fuente

- [git-fast-import - Backend for fast Git data importers](https://git-scm.com/docs/git-fast-import)
