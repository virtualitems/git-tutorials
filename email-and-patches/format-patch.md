---
title: "git format-patch"
source: "https://git-scm.com/docs/git-format-patch"
section: "email-and-patches"
status: "expanded"
---

# `git format-patch`

Este caso usa `git format-patch` para representar commits como archivos de parche para correo. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Alcance y responsabilidad

git format-patch genera, transporta o aplica series de parches conservando autoría y orden. Recibe como entrada una serie de commits, parches o mensajes de correo. La operación consiste en representar commits como archivos de parche para correo.

La página distingue lectura, escritura y resultado:

| Elemento | Relación con la función | Comprobación |
| --- | --- | --- |
| Entrada | una serie de commits, parches o mensajes de correo. | Registra los argumentos y resuelve revisiones antes de ejecutar. |
| Efecto principal | representar commits como archivos de parche para correo. | Comprueba el resultado con una orden de lectura. |
| Persistencia | Genera un archivo o flujo de salida; no mueve referencias por sí mismo. | Compara el estado antes y después. |
| Resultado | La orden comunica datos por stdout y diagnósticos por stderr. | Captura también el código de terminación. |
| Fuente de verdad | El repositorio y la configuración efectiva determinan el resultado. | Usa el orden de la serie, `git diff --check`, los encabezados y el log resultante. |

## Requisitos y laboratorio

Genera una serie en un directorio de prueba. Revisa destinatarios y encabezados sin enviar mensajes.

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

Cada parche puede transportar autoría, mensaje y diferencias. El receptor valida, aplica y registra la serie en su propio historial.

Conserva el orden de la serie y separa autor de quien aplica el parche. Los conflictos se resuelven antes de continuar con el siguiente mensaje.

Para comprobar el resultado: el receptor obtiene parches o commits con el orden, autoría y mensaje esperados. La verificación debe observar un estado distinto del canal que produjo el cambio.

## Ejemplo mínimo

```bash
git format-patch origin/main..HEAD --output-directory parches/
```

Ejecuta el bloque en orden. Conserva los nombres del laboratorio hasta confirmar el resultado. Sustituye rutas, revisiones o URL solo después de identificar su tipo y alcance.

### Resultado esperado

- La entrada queda limitada a: una serie de commits, parches o mensajes de correo.
- La operación observable es: representar commits como archivos de parche para correo.
- La comprobación se realiza mediante: el receptor obtiene parches o commits con el orden, autoría y mensaje esperados.
- stdout contiene datos o confirmaciones; stderr contiene diagnósticos. Captura ambos canales cuando automatices.

## Sintaxis

```text
git format-patch [-k] [(-o|--output-directory) <dir> | --stdout]
		   [--no-thread | --thread[=<style>]]
		   [(--attach|--inline)[=<boundary>] | --no-attach]
		   [-s | --signoff]
```

### Uso verificado con `git version 2.51.1`

```text
git format-patch [<options>] [<since> | <revision-range>]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git format-patch -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Casos de uso

| Caso | Objetivo | Criterio de verificación |
| --- | --- | --- |
| Caso base | representar commits como archivos de parche para correo | Ejecuta el ejemplo mínimo y registra el estado antes y después. |
| Alcance explícito | Aplicar git format-patch a una referencia, rango o ruta identificada. | Resuelve cada argumento antes de ejecutar y usa `--` para rutas. |
| Validación | Comprobar el resultado de git format-patch con una orden de lectura independiente. | No uses la misma salida como única prueba del cambio. |


## Opciones y variaciones

La tabla agrupa las opciones visibles en la sintaxis y en la ayuda corta. Una opción puede tener un significado propio cuando la página lo define; ejecuta la ayuda de tu versión antes de usarla en automatización.

| Opción | Efecto que debes controlar |
| --- | --- |
| `-k` | Activa el modo `-k`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-o` | Activa la forma corta de salida o una opción propia de la orden. |
| `--output-directory` | Selecciona un archivo de entrada o salida según la posición indicada en la sintaxis. |
| `--stdout` | Activa el modo `--stdout`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--no-thread` | Desactiva el comportamiento `thread` para esta invocación. |
| `--thread` | Activa el modo `--thread`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--attach` | Activa el modo `--attach`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--inline` | Activa el modo `--inline`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--no-attach` | Desactiva el comportamiento `attach` para esta invocación. |
| `-s` | Activa el modo `-s`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--signoff` | Activa el modo `--signoff`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-n` | Activa la forma corta documentada por la sintaxis; en muchas órdenes corresponde a simulación o límite numérico. |
| `--numbered` | Activa el modo `--numbered`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-N` | Activa el modo `-N`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--no-numbered` | Desactiva el comportamiento `numbered` para esta invocación. |
| `--cover-letter` | Activa el modo `--cover-letter`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--numbered-files` | Activa el modo `--numbered-files`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--suffix` | Activa el modo `--suffix`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--start-number` | Activa el modo `--start-number`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-v` | Activa la forma corta de salida con detalle o muestra versión según la orden. |
| `--reroll-count` | Establece un límite numérico para la selección o el recorrido. |
| `--filename-max-length` | Establece un límite numérico para la selección o el recorrido. |
| `--rfc` | Activa el modo `--rfc`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--cover-from-description` | Activa el modo `--cover-from-description`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--description-file` | Selecciona un archivo de entrada o salida según la posición indicada en la sintaxis. |
| `--subject-prefix` | Activa el modo `--subject-prefix`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--keep-subject` | Activa el modo `--keep-subject`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--no-binary` | Desactiva el comportamiento `binary` para esta invocación. |
| `--binary` | Activa el modo `--binary`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--zero-commit` | Activa el modo `--zero-commit`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--ignore-if-in-upstream` | Excluye elementos que cumplan la condición indicada. |
| `-p` | Activa la forma corta del modo patch o de una opción propia de la orden. |
| `--no-stat` | Desactiva el comportamiento `stat` para esta invocación. |
| `--add-header` | Permite crear o escribir el elemento seleccionado. |
| `--to` | Activa el modo `--to`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--cc` | Activa el modo `--cc`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--from` | Activa el modo `--from`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--in-reply-to` | Activa el modo `--in-reply-to`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--signature` | Activa el modo `--signature`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--base` | Activa el modo `--base`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--signature-file` | Selecciona un archivo de entrada o salida según la posición indicada en la sintaxis. |
| `-q` | Activa la forma corta del modo sin mensajes. |
| `--quiet` | Reduce mensajes que no representan errores. |
| `--progress` | Muestra progreso aunque la salida no sea un terminal. |
| `--interdiff` | Activa el modo `--interdiff`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--range-diff` | Activa el modo `--range-diff`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--creation-factor` | Activa el modo `--creation-factor`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--force-in-body-from` | Omite una protección concreta de la orden; requiere verificar origen y destino. |

## Selección de entradas

Resuelve por separado origen, destino y política de actualización. Una URL identifica un transporte; un refspec asigna referencias; un filtro limita objetos. Registra cada valor sin incluir credenciales.

Comprueba cada entrada con una orden de lectura antes de una escritura. Para listas de rutas generadas por otro proceso, prefiere una interfaz terminada en NUL cuando esté disponible.

## Salida y códigos de terminación

Un código 0 indica que la operación terminó bajo el contrato solicitado. Trata cualquier código distinto de cero según la función; no deduzcas el estado solo a partir de que stdout esté vacío.

No analices mensajes destinados a personas si existe un formato de máquina. Declara los campos, desactiva color y conserva stderr para diagnóstico.

## Errores y diagnóstico

| Señal | Causa que debes comprobar | Acción |
| --- | --- | --- |
| La numeración no coincide | El rango o la revisión de la serie cambió | Regenera la serie completa con el mismo punto base. |
| La aplicación se detiene | El parche no coincide o falta información de autor | Corrige el parche o resuelve y continúa la sesión. |
| El transporte rechaza el mensaje | La configuración SMTP o IMAP no autoriza la operación | Prueba autenticación fuera del contenido del mensaje y evita secretos en argumentos. |

Si una operación deja archivos de estado dentro de `.git`, usa `git status` y la acción de continuar, omitir o abortar definida por esa operación. No borres esos archivos para simular una cancelación.

## Automatización

1. Declara la versión mínima de Git que necesita el script.
2. Resuelve la raíz del repositorio y evita depender del directorio actual.
3. Separa opciones y rutas con `--`.
4. Captura stdout, stderr y el código de terminación.
5. Usa formatos de máquina o terminación NUL para nombres de archivo.
6. Ejecuta primero sobre el laboratorio y añade un caso sin coincidencias.

## Seguridad y recuperación

Persistencia: Genera un archivo o flujo de salida; no mueve referencias por sí mismo. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

## Práctica guiada

Genera una serie de dos commits en una rama de prueba. Inspecciona los archivos de parche y aplícalos en otro clon.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git imap-send`](../email-and-patches/imap-send.md)
- [`git am`](../email-and-patches/am.md)
- [`git send-email`](../email-and-patches/send-email.md)

## Fuente

- [git-format-patch - Prepare patches for e-mail submission](https://git-scm.com/docs/git-format-patch)
