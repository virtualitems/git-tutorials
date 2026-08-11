---
title: "git apply"
source: "https://git-scm.com/docs/git-apply"
section: "email"
canonical_file: "patching/apply.md"
status: "expanded"
---

# `git apply`

> Esta ruta conserva la clasificación `email`. La guía canónica está en [`patching/apply.md`](../patching/apply.md). Ambas documentan la misma URL del sitemap.

Este caso usa `git apply` para aplicar un parche sobre archivos o sobre el índice. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Alcance y responsabilidad

git apply aplica diffs o commits y mantiene un estado que puede continuar o abortarse. Recibe como entrada un parche, un commit o un rango que representa cambios. La operación consiste en aplicar un parche sobre archivos o sobre el índice.

La página distingue lectura, escritura y resultado:

| Elemento | Relación con la función | Comprobación |
| --- | --- | --- |
| Entrada | un parche, un commit o un rango que representa cambios. | Registra los argumentos y resuelve revisiones antes de ejecutar. |
| Efecto principal | aplicar un parche sobre archivos o sobre el índice. | Comprueba el resultado con una orden de lectura. |
| Persistencia | Puede persistir el estado implicado por esta operación: aplicar un parche sobre archivos o sobre el índice. Las opciones pueden limitar o ampliar ese efecto. | Compara el estado antes y después. |
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
git apply --check cambio.patch
git apply cambio.patch
```

Ejecuta el bloque en orden. Conserva los nombres del laboratorio hasta confirmar el resultado. Sustituye rutas, revisiones o URL solo después de identificar su tipo y alcance.

### Resultado esperado

- La entrada queda limitada a: un parche, un commit o un rango que representa cambios.
- La operación observable es: aplicar un parche sobre archivos o sobre el índice.
- La comprobación se realiza mediante: el diff y el historial muestran si cambiaron archivos, índice o commits.
- stdout contiene datos o confirmaciones; stderr contiene diagnósticos. Captura ambos canales cuando automatices.

## Sintaxis

```text
git apply [--stat] [--numstat] [--summary] [--check]
	  [--index | --intent-to-add] [--3way] [--ours | --theirs | --union]
	  [--apply] [--no-add] [--build-fake-ancestor=<file>] [-R | --reverse]
	  [--allow-binary-replacement | --binary] [--reject] [-z]
```

### Uso verificado con `git version 2.51.1`

```text
git apply [<options>] [<patch>...]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git apply -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Casos de uso

| Caso | Objetivo | Criterio de verificación |
| --- | --- | --- |
| Caso base | aplicar un parche sobre archivos o sobre el índice | Ejecuta el ejemplo mínimo y registra el estado antes y después. |
| Alcance explícito | Aplicar git apply a una referencia, rango o ruta identificada. | Resuelve cada argumento antes de ejecutar y usa `--` para rutas. |
| Salida para scripts | Producir registros con campos y separadores definidos. | Prueba nombres con espacios y saltos de línea. |
| Validación | Comprobar el resultado de git apply con una orden de lectura independiente. | No uses la misma salida como única prueba del cambio. |


## Opciones y variaciones

La tabla agrupa las opciones visibles en la sintaxis y en la ayuda corta. Una opción puede tener un significado propio cuando la página lo define; ejecuta la ayuda de tu versión antes de usarla en automatización.

| Opción | Efecto que debes controlar |
| --- | --- |
| `--stat` | Resume cambios mediante conteos por ruta. |
| `--numstat` | Activa el modo `--numstat`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--summary` | Activa el modo `--summary`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--check` | Valida sin producir el efecto principal de la orden. |
| `--index` | Incluye el índice en la operación. |
| `--intent-to-add` | Registra una entrada sin preparar todavía su contenido. |
| `--3way` | Activa el modo `--3way`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--ours` | Activa el modo `--ours`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--theirs` | Activa el modo `--theirs`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--union` | Activa el modo `--union`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--apply` | Activa el modo `--apply`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--no-add` | Desactiva el comportamiento `add` para esta invocación. |
| `--build-fake-ancestor` | Activa el modo `--build-fake-ancestor`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-R` | Activa el modo `-R`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--reverse` | Invierte el orden del recorrido o resultado. |
| `--allow-binary-replacement` | Activa el modo `--allow-binary-replacement`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--binary` | Activa el modo `--binary`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--reject` | Activa el modo `--reject`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-z` | Termina registros con NUL para evitar división por espacios o saltos de línea. |
| `--exclude` | Excluye elementos que cumplan la condición indicada. |
| `--include` | Incluye elementos adicionales dentro del alcance indicado. |
| `-p` | Activa la forma corta del modo patch o de una opción propia de la orden. |
| `--add` | Permite crear o escribir el elemento seleccionado. |
| `-N` | Activa el modo `-N`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--cached` | Usa el índice como origen o destino, sin tratar el área de trabajo de la misma forma. |
| `--unsafe-paths` | Activa el modo `--unsafe-paths`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-3` | Activa el modo `-3`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-C` | Ejecuta Git como si se hubiera iniciado en el directorio indicado. |
| `--whitespace` | Activa el modo `--whitespace`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--ignore-space-change` | Excluye elementos que cumplan la condición indicada. |
| `--ignore-whitespace` | Excluye elementos que cumplan la condición indicada. |
| `--unidiff-zero` | Activa el modo `--unidiff-zero`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--allow-overlap` | Activa el modo `--allow-overlap`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-v` | Activa la forma corta de salida con detalle o muestra versión según la orden. |
| `--verbose` | Aumenta el detalle enviado a la salida. |
| `-q` | Activa la forma corta del modo sin mensajes. |
| `--quiet` | Reduce mensajes que no representan errores. |
| `--inaccurate-eof` | Activa el modo `--inaccurate-eof`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--recount` | Activa el modo `--recount`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--directory` | Activa el modo `--directory`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--allow-empty` | Activa el modo `--allow-empty`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |

## Selección de entradas

Las revisiones se resuelven antes que los pathspecs cuando la sintaxis las espera. Usa `--` para separar opciones y rutas. Cita los globos para decidir si los expande el shell o Git.

Comprueba cada entrada con una orden de lectura antes de una escritura. Para listas de rutas generadas por otro proceso, prefiere una interfaz terminada en NUL cuando esté disponible.

## Salida y códigos de terminación

`git apply --check` devuelve un valor distinto de cero si el parche no puede aplicarse sin modificar archivos.

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

Persistencia: Puede persistir el estado implicado por esta operación: aplicar un parche sobre archivos o sobre el índice. Las opciones pueden limitar o ampliar ese efecto. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

## Práctica guiada

Trabaja en una rama de prueba. Compara `git diff`, `git diff --staged` y `git log --oneline --graph` antes y después.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git cherry-pick`](../patching/cherry-pick.md)
- [`git rebase`](../patching/rebase.md)

## Fuente

- [git-apply - Apply a patch to files and/or to the index](https://git-scm.com/docs/git-apply)
