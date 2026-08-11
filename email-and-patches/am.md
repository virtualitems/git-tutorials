---
title: "git am"
source: "https://git-scm.com/docs/git-am"
section: "email-and-patches"
status: "expanded"
---

# `git am`

Este caso usa `git am` para convertir una serie de parches de correo en commits. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Alcance y responsabilidad

git am genera, transporta o aplica series de parches conservando autoría y orden. Recibe como entrada una serie de commits, parches o mensajes de correo. La operación consiste en convertir una serie de parches de correo en commits.

La página distingue lectura, escritura y resultado:

| Elemento | Relación con la función | Comprobación |
| --- | --- | --- |
| Entrada | una serie de commits, parches o mensajes de correo. | Registra los argumentos y resuelve revisiones antes de ejecutar. |
| Efecto principal | convertir una serie de parches de correo en commits. | Comprueba el resultado con una orden de lectura. |
| Persistencia | Puede persistir el estado implicado por esta operación: convertir una serie de parches de correo en commits. Las opciones pueden limitar o ampliar ese efecto. | Compara el estado antes y después. |
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
git am 0001-corrige-indice.patch
# Si aparece un conflicto:
git am --continue
```

Ejecuta el bloque en orden. Conserva los nombres del laboratorio hasta confirmar el resultado. Sustituye rutas, revisiones o URL solo después de identificar su tipo y alcance.

### Resultado esperado

- La entrada queda limitada a: una serie de commits, parches o mensajes de correo.
- La operación observable es: convertir una serie de parches de correo en commits.
- La comprobación se realiza mediante: el receptor obtiene parches o commits con el orden, autoría y mensaje esperados.
- stdout contiene datos o confirmaciones; stderr contiene diagnósticos. Captura ambos canales cuando automatices.

## Sintaxis

```text
git am [--signoff] [--keep] [--[no-]keep-cr] [--[no-]utf8] [--[no-]verify]
	 [--[no-]3way] [--interactive] [--committer-date-is-author-date]
	 [--ignore-date] [--ignore-space-change | --ignore-whitespace]
	 [--whitespace=<action>] [-C<n>] [-p<n>] [--directory=<dir>]
```

### Uso verificado con `git version 2.51.1`

```text
git am [<options>] [(<mbox> | <Maildir>)...]
   or: git am [<options>] (--continue | --skip | --abort)
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git am -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Casos de uso

| Caso | Objetivo | Criterio de verificación |
| --- | --- | --- |
| Caso base | convertir una serie de parches de correo en commits | Ejecuta el ejemplo mínimo y registra el estado antes y después. |
| Alcance explícito | Aplicar git am a una referencia, rango o ruta identificada. | Resuelve cada argumento antes de ejecutar y usa `--` para rutas. |
| Sesión interrumpida | Continuar o cancelar una secuencia después de revisar el estado. | Consulta `git status` antes de elegir la acción. |
| Validación | Comprobar el resultado de git am con una orden de lectura independiente. | No uses la misma salida como única prueba del cambio. |


## Opciones y variaciones

La tabla agrupa las opciones visibles en la sintaxis y en la ayuda corta. Una opción puede tener un significado propio cuando la página lo define; ejecuta la ayuda de tu versión antes de usarla en automatización.

| Opción | Efecto que debes controlar |
| --- | --- |
| `--signoff` | Activa el modo `--signoff`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--keep` | Activa el modo `--keep`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--keep-cr` | Activa el modo `--keep-cr`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--utf8` | Activa el modo `--utf8`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--verify` | Exige que el nombre o estructura cumpla el contrato antes de continuar. |
| `--3way` | Activa el modo `--3way`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--interactive` | Abre una selección interactiva antes de aplicar la operación. |
| `--committer-date-is-author-date` | Aplica una fecha, duración o política de vencimiento. |
| `--ignore-date` | Aplica una fecha, duración o política de vencimiento. |
| `--ignore-space-change` | Excluye elementos que cumplan la condición indicada. |
| `--ignore-whitespace` | Excluye elementos que cumplan la condición indicada. |
| `--whitespace` | Activa el modo `--whitespace`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-C` | Ejecuta Git como si se hubiera iniciado en el directorio indicado. |
| `-p` | Activa la forma corta del modo patch o de una opción propia de la orden. |
| `--directory` | Activa el modo `--directory`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--continue` | Reanuda una secuencia pausada después de resolver su estado. |
| `--skip` | Omite el elemento actual y continúa la secuencia. |
| `--abort` | Cancela la secuencia y restaura el punto que la orden registró al comenzar. |
| `-i` | Activa la forma corta del modo interactivo o una opción propia de la orden. |
| `-n` | Activa la forma corta documentada por la sintaxis; en muchas órdenes corresponde a simulación o límite numérico. |
| `--no-verify` | Desactiva el comportamiento `verify` para esta invocación. |
| `-3` | Activa el modo `-3`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-q` | Activa la forma corta del modo sin mensajes. |
| `--quiet` | Reduce mensajes que no representan errores. |
| `-s` | Activa el modo `-s`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-u` | Activa el modo `-u`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-k` | Activa el modo `-k`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--keep-non-patch` | Activa el modo `--keep-non-patch`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-b` | Activa el modo `-b`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-m` | Activa el modo `-m`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--message-id` | Activa el modo `--message-id`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-c` | Aplica una clave de configuración solo a esta invocación. |
| `--scissors` | Activa el modo `--scissors`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--quoted-cr` | Activa el modo `--quoted-cr`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--exclude` | Excluye elementos que cumplan la condición indicada. |
| `--include` | Incluye elementos adicionales dentro del alcance indicado. |
| `--patch-format` | Controla campos, orden o representación del resultado. |
| `--reject` | Activa el modo `--reject`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--resolvemsg` | Activa el modo `--resolvemsg`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-r` | Activa el modo `-r`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--resolved` | Activa el modo `--resolved`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--quit` | Sale de la secuencia y conserva el estado que la documentación define. |
| `--show-current-patch` | Incluye información adicional en la salida. |
| `--retry` | Activa el modo `--retry`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--allow-empty` | Activa el modo `--allow-empty`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--rerere-autoupdate` | Activa el modo `--rerere-autoupdate`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-S` | Activa el modo `-S`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--gpg-sign` | Activa el modo `--gpg-sign`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--empty` | Activa el modo `--empty`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |

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

Persistencia: Puede persistir el estado implicado por esta operación: convertir una serie de parches de correo en commits. Las opciones pueden limitar o ampliar ese efecto. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

## Práctica guiada

Genera una serie de dos commits en una rama de prueba. Inspecciona los archivos de parche y aplícalos en otro clon.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git format-patch`](../email-and-patches/format-patch.md)
- [`git imap-send`](../email-and-patches/imap-send.md)

## Fuente

- [git-am - Apply a series of patches from a mailbox](https://git-scm.com/docs/git-am)
