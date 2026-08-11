---
title: "git unpack-file"
source: "https://git-scm.com/docs/git-unpack-file"
section: "plumbing-read"
status: "expanded"
---

# `git unpack-file`

Este caso usa `git unpack-file` para crear un archivo temporal con el contenido de un blob. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Alcance y responsabilidad

git unpack-file consulta objetos, referencias, índices, packs y relaciones entre commits. Recibe como entrada objetos, referencias, árboles o entradas del índice que debe leer la consulta. La operación consiste en crear un archivo temporal con el contenido de un blob.

La página distingue lectura, escritura y resultado:

| Elemento | Relación con la función | Comprobación |
| --- | --- | --- |
| Entrada | objetos, referencias, árboles o entradas del índice que debe leer la consulta. | Registra los argumentos y resuelve revisiones antes de ejecutar. |
| Efecto principal | crear un archivo temporal con el contenido de un blob. | Comprueba el resultado con una orden de lectura. |
| Persistencia | Crea un archivo temporal con el contenido solicitado y comunica su ruta. | Compara el estado antes y después. |
| Resultado | La orden comunica datos por stdout y diagnósticos por stderr. | Captura también el código de terminación. |
| Fuente de verdad | El repositorio y la configuración efectiva determinan el resultado. | Usa tipo, tamaño, hash, referencia o etapa impresos por una segunda consulta. |

## Requisitos y laboratorio

Crea un commit base, conserva sus hashes con `git rev-parse` y consulta cada objeto por tipo y contenido.

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

La salida expone datos internos para inspección o scripts. Los formatos explícitos y los separadores NUL evitan ambigüedad cuando los nombres contienen espacios o saltos de línea.

Fija el formato de salida que consumirá el siguiente proceso. Usa separadores NUL cuando una ruta pueda contener caracteres que también actúan como separadores de texto.

Para comprobar el resultado: la salida estructurada puede compararse o pasar a otro proceso sin alterar el repositorio. La verificación debe observar un estado distinto del canal que produjo el cambio.

## Ejemplo mínimo

```bash
blob=$(git rev-parse HEAD:README.md)
temporal=$(git unpack-file "$blob")
printf '%s\n' "$temporal"
```

Ejecuta el bloque en orden. Conserva los nombres del laboratorio hasta confirmar el resultado. Sustituye rutas, revisiones o URL solo después de identificar su tipo y alcance.

### Resultado esperado

- La entrada queda limitada a: objetos, referencias, árboles o entradas del índice que debe leer la consulta.
- La operación observable es: crear un archivo temporal con el contenido de un blob.
- La comprobación se realiza mediante: la salida estructurada puede compararse o pasar a otro proceso sin alterar el repositorio.
- stdout contiene datos o confirmaciones; stderr contiene diagnósticos. Captura ambos canales cuando automatices.

## Sintaxis

```text
git unpack-file <blob>
```

### Uso verificado con `git version 2.51.1`

```text
git unpack-file <blob>
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git unpack-file -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Casos de uso

| Caso | Objetivo | Criterio de verificación |
| --- | --- | --- |
| Caso base | crear un archivo temporal con el contenido de un blob | Ejecuta el ejemplo mínimo y registra el estado antes y después. |
| Alcance explícito | Aplicar git unpack-file a una referencia, rango o ruta identificada. | Resuelve cada argumento antes de ejecutar y usa `--` para rutas. |
| Validación | Comprobar el resultado de git unpack-file con una orden de lectura independiente. | No uses la misma salida como única prueba del cambio. |



## Selección de entradas

Distingue identificadores de objeto, referencias y rutas. Resuelve revisiones con `git rev-parse --verify`; inspecciona tipo y tamaño con `git cat-file`; usa actualización condicional al escribir referencias.

Comprueba cada entrada con una orden de lectura antes de una escritura. Para listas de rutas generadas por otro proceso, prefiere una interfaz terminada en NUL cuando esté disponible.

## Salida y códigos de terminación

Un código 0 indica que la operación terminó bajo el contrato solicitado. Trata cualquier código distinto de cero según la función; no deduzcas el estado solo a partir de que stdout esté vacío.

No analices mensajes destinados a personas si existe un formato de máquina. Declara los campos, desactiva color y conserva stderr para diagnóstico.

## Errores y diagnóstico

| Señal | Causa que debes comprobar | Acción |
| --- | --- | --- |
| El objeto no existe | El identificador no resuelve o no está disponible en un clon parcial | Valida el hash y la política de descarga. |
| La salida se separa mal | Un nombre contiene espacios o saltos de línea | Usa terminación NUL cuando la función la admita. |
| El recorrido incluye más commits | El rango expresa alcanzabilidad y no una lista literal | Comprueba extremos positivos y negativos del rango. |

Si una operación deja archivos de estado dentro de `.git`, usa `git status` y la acción de continuar, omitir o abortar definida por esa operación. No borres esos archivos para simular una cancelación.

## Automatización

1. Declara la versión mínima de Git que necesita el script.
2. Resuelve la raíz del repositorio y evita depender del directorio actual.
3. Separa opciones y rutas con `--`.
4. Captura stdout, stderr y el código de terminación.
5. Usa formatos de máquina o terminación NUL para nombres de archivo.
6. Ejecuta primero sobre el laboratorio y añade un caso sin coincidencias.

## Seguridad y recuperación

Persistencia: Crea un archivo temporal con el contenido solicitado y comunica su ruta. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

## Práctica guiada

Prueba con nombres que contengan espacios. Si el comando ofrece `-z`, procesa la salida por bytes y conserva los separadores NUL.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git var`](../plumbing-read/var.md)
- [`git show-ref`](../plumbing-read/show-ref.md)
- [`git verify-pack`](../plumbing-read/verify-pack.md)

## Fuente

- [git-unpack-file - Creates a temporary file with a blob’s contents](https://git-scm.com/docs/git-unpack-file)
