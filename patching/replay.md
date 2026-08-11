---
title: "git replay"
source: "https://git-scm.com/docs/git-replay"
section: "patching"
status: "expanded"
---

# `git replay`

Este caso usa `git replay` para reproducir commits sobre una base y comunicar el cambio de referencias. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Alcance y responsabilidad

git replay aplica diffs o commits y mantiene un estado que puede continuar o abortarse. Recibe como entrada un parche, un commit o un rango que representa cambios. La operación consiste en reproducir commits sobre una base y comunicar el cambio de referencias.

La página distingue lectura, escritura y resultado:

| Elemento | Relación con la función | Comprobación |
| --- | --- | --- |
| Entrada | un parche, un commit o un rango que representa cambios. | Registra los argumentos y resuelve revisiones antes de ejecutar. |
| Efecto principal | reproducir commits sobre una base y comunicar el cambio de referencias. | Comprueba el resultado con una orden de lectura. |
| Persistencia | Puede persistir el estado implicado por esta operación: reproducir commits sobre una base y comunicar el cambio de referencias. Las opciones pueden limitar o ampliar ese efecto. | Compara el estado antes y después. |
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
git replay --onto=main main..tema-portada
```

Ejecuta el bloque en orden. Conserva los nombres del laboratorio hasta confirmar el resultado. Sustituye rutas, revisiones o URL solo después de identificar su tipo y alcance.

### Resultado esperado

- La entrada queda limitada a: un parche, un commit o un rango que representa cambios.
- La operación observable es: reproducir commits sobre una base y comunicar el cambio de referencias.
- La comprobación se realiza mediante: el diff y el historial muestran si cambiaron archivos, índice o commits.
- stdout contiene datos o confirmaciones; stderr contiene diagnósticos. Captura ambos canales cuando automatices.

## Sintaxis

```text
(EXPERIMENTAL!) git replay ([--contained] --onto=<newbase> | --advance=<branch> | --revert=<branch>)
			     [--ref=<ref>] [--ref-action=<mode>] <revision-range>
```

### Uso verificado con `git version 2.51.1`

```text
(EXPERIMENTAL!) git replay ([--contained] --onto <newbase> | --advance <branch>) <revision-range>...
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git replay -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Casos de uso

| Caso | Objetivo | Criterio de verificación |
| --- | --- | --- |
| Caso base | reproducir commits sobre una base y comunicar el cambio de referencias | Ejecuta el ejemplo mínimo y registra el estado antes y después. |
| Alcance explícito | Aplicar git replay a una referencia, rango o ruta identificada. | Resuelve cada argumento antes de ejecutar y usa `--` para rutas. |
| Validación | Comprobar el resultado de git replay con una orden de lectura independiente. | No uses la misma salida como única prueba del cambio. |


## Opciones y variaciones

La tabla agrupa las opciones visibles en la sintaxis y en la ayuda corta. Una opción puede tener un significado propio cuando la página lo define; ejecuta la ayuda de tu versión antes de usarla en automatización.

| Opción | Efecto que debes controlar |
| --- | --- |
| `--contained` | Activa el modo `--contained`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--onto` | Activa el modo `--onto`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--advance` | Activa el modo `--advance`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--revert` | Activa el modo `--revert`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--ref` | Selecciona o modifica referencias dentro del alcance de la orden. |
| `--ref-action` | Selecciona o modifica referencias dentro del alcance de la orden. |

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

Persistencia: Puede persistir el estado implicado por esta operación: reproducir commits sobre una base y comunicar el cambio de referencias. Las opciones pueden limitar o ampliar ese efecto. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

## Práctica guiada

Trabaja en una rama de prueba. Compara `git diff`, `git diff --staged` y `git log --oneline --graph` antes y después.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git revert`](../patching/revert.md)
- [`git rebase`](../patching/rebase.md)
- [`git cherry-pick`](../patching/cherry-pick.md)

## Fuente

- [git-replay - EXPERIMENTAL: Replay commits on a new base, works with bare repos too](https://git-scm.com/docs/git-replay)
