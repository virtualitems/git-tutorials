---
title: "git sparse-checkout"
source: "https://git-scm.com/docs/git-sparse-checkout"
section: "getting-and-creating-projects"
status: "expanded"
---

# `git sparse-checkout`

Este caso usa `git sparse-checkout` para materializar solo una parte de los archivos seguidos. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Alcance y responsabilidad

git sparse-checkout crea la base de datos local de objetos y prepara el área de trabajo. Recibe como entrada un directorio, una URL o una selección de rutas. La operación consiste en materializar solo una parte de los archivos seguidos.

La página distingue lectura, escritura y resultado:

| Elemento | Relación con la función | Comprobación |
| --- | --- | --- |
| Entrada | un directorio, una URL o una selección de rutas. | Registra los argumentos y resuelve revisiones antes de ejecutar. |
| Efecto principal | materializar solo una parte de los archivos seguidos. | Comprueba el resultado con una orden de lectura. |
| Persistencia | Puede persistir el estado implicado por esta operación: materializar solo una parte de los archivos seguidos. Las opciones pueden limitar o ampliar ese efecto. | Compara el estado antes y después. |
| Resultado | La orden comunica datos por stdout y diagnósticos por stderr. | Captura también el código de terminación. |
| Fuente de verdad | El repositorio y la configuración efectiva determinan el resultado. | Usa `git status`, `git remote -v` y `git rev-parse --show-toplevel`. |

## Requisitos y laboratorio

Usa dos directorios bajo una ruta creada con `mktemp -d`: uno como origen y otro como destino.

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

Un repositorio contiene objetos y referencias. Un área de trabajo materializa un commit para que los archivos puedan editarse.

Separa los datos del repositorio de los archivos materializados. Un repositorio bare conserva objetos y referencias sin área de trabajo.

Para comprobar el resultado: el directorio resultante contiene el repositorio y, cuando corresponde, un área de trabajo. La verificación debe observar un estado distinto del canal que produjo el cambio.

## Ejemplo mínimo

```bash
git sparse-checkout init --cone
git sparse-checkout set app docs
```

Ejecuta el bloque en orden. Conserva los nombres del laboratorio hasta confirmar el resultado. Sustituye rutas, revisiones o URL solo después de identificar su tipo y alcance.

### Resultado esperado

- La entrada queda limitada a: un directorio, una URL o una selección de rutas.
- La operación observable es: materializar solo una parte de los archivos seguidos.
- La comprobación se realiza mediante: el directorio resultante contiene el repositorio y, cuando corresponde, un área de trabajo.
- stdout contiene datos o confirmaciones; stderr contiene diagnósticos. Captura ambos canales cuando automatices.

## Sintaxis

```text
git sparse-checkout (init | list | set | add | reapply | disable | check-rules | clean) [<options>]
```

### Uso verificado con `git version 2.51.1`

```text
git sparse-checkout (init | list | set | add | reapply | disable | check-rules) [<options>]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git sparse-checkout -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Casos de uso

| Caso | Objetivo | Criterio de verificación |
| --- | --- | --- |
| Caso base | materializar solo una parte de los archivos seguidos | Ejecuta el ejemplo mínimo y registra el estado antes y después. |
| Alcance explícito | Aplicar git sparse-checkout a una referencia, rango o ruta identificada. | Resuelve cada argumento antes de ejecutar y usa `--` para rutas. |
| Validación | Comprobar el resultado de git sparse-checkout con una orden de lectura independiente. | No uses la misma salida como única prueba del cambio. |



## Selección de entradas

Las revisiones se resuelven antes que los pathspecs cuando la sintaxis las espera. Usa `--` para separar opciones y rutas. Cita los globos para decidir si los expande el shell o Git.

Comprueba cada entrada con una orden de lectura antes de una escritura. Para listas de rutas generadas por otro proceso, prefiere una interfaz terminada en NUL cuando esté disponible.

## Salida y códigos de terminación

Un código 0 indica que la operación terminó bajo el contrato solicitado. Trata cualquier código distinto de cero según la función; no deduzcas el estado solo a partir de que stdout esté vacío.

No analices mensajes destinados a personas si existe un formato de máquina. Declara los campos, desactiva color y conserva stderr para diagnóstico.

## Errores y diagnóstico

| Señal | Causa que debes comprobar | Acción |
| --- | --- | --- |
| El destino ya contiene archivos | La creación o clonación requiere una ruta compatible | Elige un directorio vacío o inicializa la ruta de forma explícita. |
| No se recibe una referencia | El remoto no la anuncia o el filtro la excluye | Ejecuta `git ls-remote <url>` y revisa los filtros. |
| Falla la autenticación | La URL o el helper de credenciales no entrega acceso | Comprueba la URL sin registrar credenciales en el historial del shell. |

Si una operación deja archivos de estado dentro de `.git`, usa `git status` y la acción de continuar, omitir o abortar definida por esa operación. No borres esos archivos para simular una cancelación.

## Automatización

1. Declara la versión mínima de Git que necesita el script.
2. Resuelve la raíz del repositorio y evita depender del directorio actual.
3. Separa opciones y rutas con `--`.
4. Captura stdout, stderr y el código de terminación.
5. Usa formatos de máquina o terminación NUL para nombres de archivo.
6. Ejecuta primero sobre el laboratorio y añade un caso sin coincidencias.

## Seguridad y recuperación

Persistencia: Puede persistir el estado implicado por esta operación: materializar solo una parte de los archivos seguidos. Las opciones pueden limitar o ampliar ese efecto. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

## Práctica guiada

Usa un directorio temporal. Compara el contenido antes y después, incluidos `.git`, HEAD y las ramas disponibles.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git clone`](../getting-and-creating-projects/clone.md)
- [`git init`](../getting-and-creating-projects/init.md)

## Fuente

- [git-sparse-checkout - Reduce your working tree to a subset of tracked files](https://git-scm.com/docs/git-sparse-checkout)
