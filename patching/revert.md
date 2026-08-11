---
title: "git revert"
source: "https://git-scm.com/docs/git-revert"
section: "patching"
status: "expanded"
---

# `git revert`

Este caso usa `git revert` para crear un commit que invierte el efecto de otro commit. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Alcance y responsabilidad

git revert aplica diffs o commits y mantiene un estado que puede continuar o abortarse. Recibe como entrada un parche, un commit o un rango que representa cambios. La operación consiste en crear un commit que invierte el efecto de otro commit.

La página distingue lectura, escritura y resultado:

| Elemento | Relación con la función | Comprobación |
| --- | --- | --- |
| Entrada | un parche, un commit o un rango que representa cambios. | Registra los argumentos y resuelve revisiones antes de ejecutar. |
| Efecto principal | crear un commit que invierte el efecto de otro commit. | Comprueba el resultado con una orden de lectura. |
| Persistencia | Puede persistir el estado implicado por esta operación: crear un commit que invierte el efecto de otro commit. Las opciones pueden limitar o ampliar ese efecto. | Compara el estado antes y después. |
| Resultado | La orden comunica datos por stdout y diagnósticos por stderr. | Captura también el código de terminación. |
| Fuente de verdad | El repositorio y la configuración efectiva determinan el resultado. | Usa `git status`, `git diff --check` y `git log --oneline --decorate -n 10`. |

## Requisitos y laboratorio

Trabaja sobre una rama de prueba y crea una etiqueta o rama de respaldo antes de aplicar una serie.

```bash
lab_dir="$(mktemp -d)"
git init "$lab_dir/proyecto"
git -C "$lab_dir/proyecto" config user.name "Persona de prueba"
git -C "$lab_dir/proyecto" config user.email "prueba@example.test"
printf 'línea base\n' > "$lab_dir/proyecto/archivo.txt"
git -C "$lab_dir/proyecto" add archivo.txt
git -C "$lab_dir/proyecto" commit -m "base"
cd "$lab_dir/proyecto"
```

Antes de ejecutar el ejemplo, confirma la raíz con `git rev-parse --show-toplevel` cuando exista un repositorio. Registra `git status --short` y las referencias que puedan cambiar.

## Modelo de funcionamiento

Un parche representa diferencias de contenido. Aplicarlo puede modificar archivos, el índice o producir commits nuevos, según el comando.

Determina si la operación aplica diferencias a archivos, al índice o al historial. Esa elección define cómo se comprueba y cómo se revierte el resultado.

Para comprobar el resultado: el diff y el historial muestran si cambiaron archivos, índice o commits. La verificación debe observar un estado distinto del canal que produjo el cambio.

## Ejemplo mínimo

```bash
git revert a1b2c3d
```

Ejecuta el bloque en orden. Conserva los nombres del laboratorio hasta confirmar el resultado. Sustituye rutas, revisiones o URL solo después de identificar su tipo y alcance.

### Resultado esperado

- La entrada queda limitada a: un parche, un commit o un rango que representa cambios.
- La operación observable es: crear un commit que invierte el efecto de otro commit.
- La comprobación se realiza mediante: el diff y el historial muestran si cambiaron archivos, índice o commits.
- stdout contiene datos o confirmaciones; stderr contiene diagnósticos. Captura ambos canales cuando automatices.

## Sintaxis

```text
git revert [--[no-]edit] [-n] [-m <parent-number>] [-s] [-S[<keyid>]] <commit>…
git revert (--continue | --skip | --abort | --quit)
```

### Uso verificado con `git version 2.51.1`

```text
git revert [--[no-]edit] [-n] [-m <parent-number>] [-s] [-S[<keyid>]] <commit>...
   or: git revert (--continue | --skip | --abort | --quit)
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git revert -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Casos de uso

| Caso | Objetivo | Criterio de verificación |
| --- | --- | --- |
| Caso base | crear un commit que invierte el efecto de otro commit | Ejecuta el ejemplo mínimo y registra el estado antes y después. |
| Alcance explícito | Aplicar git revert a una referencia, rango o ruta identificada. | Resuelve cada argumento antes de ejecutar y usa `--` para rutas. |
| Sesión interrumpida | Continuar o cancelar una secuencia después de revisar el estado. | Consulta `git status` antes de elegir la acción. |
| Validación | Comprobar el resultado de git revert con una orden de lectura independiente. | No uses la misma salida como única prueba del cambio. |


## Opciones y variaciones

La tabla agrupa las opciones visibles en la sintaxis y en la ayuda corta. Una opción puede tener un significado propio cuando la página lo define; ejecuta la ayuda de tu versión antes de usarla en automatización.

| Opción | Efecto que debes controlar |
| --- | --- |
| `--edit` | Abre la representación editable que define la orden antes de aplicarla. |
| `-n` | Activa la forma corta documentada por la sintaxis; en muchas órdenes corresponde a simulación o límite numérico. |
| `-m` | Activa el modo `-m`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-s` | Activa el modo `-s`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-S` | Activa el modo `-S`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--continue` | Reanuda una secuencia pausada después de resolver su estado. |
| `--skip` | Omite el elemento actual y continúa la secuencia. |
| `--abort` | Cancela la secuencia y restaura el punto que la orden registró al comenzar. |
| `--quit` | Sale de la secuencia y conserva el estado que la documentación define. |
| `--cleanup` | Activa el modo `--cleanup`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--no-commit` | Desactiva el comportamiento `commit` para esta invocación. |
| `--commit` | Activa el modo `--commit`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-e` | Activa el modo `-e`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--signoff` | Activa el modo `--signoff`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--mainline` | Activa el modo `--mainline`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--rerere-autoupdate` | Activa el modo `--rerere-autoupdate`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--strategy` | Selecciona el algoritmo o estrategia que procesa la entrada. |
| `-X` | Activa el modo `-X`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--strategy-option` | Selecciona el algoritmo o estrategia que procesa la entrada. |
| `--gpg-sign` | Activa el modo `--gpg-sign`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--reference` | Activa el modo `--reference`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |

## Selección de entradas

Las revisiones se resuelven antes que los pathspecs cuando la sintaxis las espera. Usa `--` para separar opciones y rutas. Cita los globos para decidir si los expande el shell o Git.

Comprueba cada entrada con una orden de lectura antes de una escritura. Para listas de rutas generadas por otro proceso, prefiere una interfaz terminada en NUL cuando esté disponible.

## Salida y códigos de terminación

Un código 0 indica que la operación terminó bajo el contrato solicitado. Trata cualquier código distinto de cero según la función; no deduzcas el estado solo a partir de que stdout esté vacío.

No analices mensajes destinados a personas si existe un formato de máquina. Declara los campos, desactiva color y conserva stderr para diagnóstico.

## Errores y diagnóstico

| Señal | Causa que debes comprobar | Acción |
| --- | --- | --- |
| Un parche no aplica | El contexto no coincide con el contenido actual | Inspecciona los rechazos o resuelve el conflicto antes de continuar. |
| La secuencia queda en pausa | Git espera una resolución o una decisión | Consulta `git status` y usa `--continue`, `--skip` o `--abort`. |
| El resultado contiene commits vacíos | Los cambios ya existen o se resolvieron sin diferencias | Revisa el diff y aplica la política de commits vacíos de la orden. |

Si una operación deja archivos de estado dentro de `.git`, usa `git status` y la acción de continuar, omitir o abortar definida por esa operación. No borres esos archivos para simular una cancelación.

## Automatización

1. Declara la versión mínima de Git que necesita el script.
2. Resuelve la raíz del repositorio y evita depender del directorio actual.
3. Separa opciones y rutas con `--`.
4. Captura stdout, stderr y el código de terminación.
5. Usa formatos de máquina o terminación NUL para nombres de archivo.
6. Ejecuta primero sobre el laboratorio y añade un caso sin coincidencias.

## Seguridad y recuperación

Persistencia: Puede persistir el estado implicado por esta operación: crear un commit que invierte el efecto de otro commit. Las opciones pueden limitar o ampliar ese efecto. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

## Práctica guiada

Trabaja en una rama de prueba. Compara `git diff`, `git diff --staged` y `git log --oneline --graph` antes y después.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git replay`](../patching/replay.md)
- [`git rebase`](../patching/rebase.md)

## Fuente

- [git-revert - Revert some existing commits](https://git-scm.com/docs/git-revert)
