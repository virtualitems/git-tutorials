---
title: "git imap-send"
source: "https://git-scm.com/docs/git-imap-send"
section: "email-and-patches"
status: "expanded"
---

# `git imap-send`

Este caso usa `git imap-send` para enviar una colección de parches a una carpeta IMAP. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Alcance y responsabilidad

git imap-send genera, transporta o aplica series de parches conservando autoría y orden. Recibe como entrada una serie de commits, parches o mensajes de correo. La operación consiste en enviar una colección de parches a una carpeta IMAP.

La página distingue lectura, escritura y resultado:

| Elemento | Relación con la función | Comprobación |
| --- | --- | --- |
| Entrada | una serie de commits, parches o mensajes de correo. | Registra los argumentos y resuelve revisiones antes de ejecutar. |
| Efecto principal | enviar una colección de parches a una carpeta IMAP. | Comprueba el resultado con una orden de lectura. |
| Persistencia | Envía datos a un sistema externo; no crea commits por sí mismo. | Compara el estado antes y después. |
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
git format-patch --stdout origin/main..HEAD | git imap-send
```

Ejecuta el bloque en orden. Conserva los nombres del laboratorio hasta confirmar el resultado. Sustituye rutas, revisiones o URL solo después de identificar su tipo y alcance.

### Resultado esperado

- La entrada queda limitada a: una serie de commits, parches o mensajes de correo.
- La operación observable es: enviar una colección de parches a una carpeta IMAP.
- La comprobación se realiza mediante: el receptor obtiene parches o commits con el orden, autoría y mensaje esperados.
- stdout contiene datos o confirmaciones; stderr contiene diagnósticos. Captura ambos canales cuando automatices.

## Sintaxis

```text
git imap-send [-v] [-q] [--[no-]curl] [(--folder|-f) <folder>]
git imap-send --list
```

### Uso verificado con `git version 2.51.1`

```text
git imap-send [-v] [-q] [--[no-]curl] [(--folder|-f) <folder>] < <mbox>
   or: git imap-send --list
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git imap-send -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Casos de uso

| Caso | Objetivo | Criterio de verificación |
| --- | --- | --- |
| Caso base | enviar una colección de parches a una carpeta IMAP | Ejecuta el ejemplo mínimo y registra el estado antes y después. |
| Alcance explícito | Aplicar git imap-send a una referencia, rango o ruta identificada. | Resuelve cada argumento antes de ejecutar y usa `--` para rutas. |
| Validación | Comprobar el resultado de git imap-send con una orden de lectura independiente. | No uses la misma salida como única prueba del cambio. |


## Opciones y variaciones

La tabla agrupa las opciones visibles en la sintaxis y en la ayuda corta. Una opción puede tener un significado propio cuando la página lo define; ejecuta la ayuda de tu versión antes de usarla en automatización.

| Opción | Efecto que debes controlar |
| --- | --- |
| `-v` | Activa la forma corta de salida con detalle o muestra versión según la orden. |
| `-q` | Activa la forma corta del modo sin mensajes. |
| `--curl` | Activa el modo `--curl`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--folder` | Activa el modo `--folder`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-f` | Activa la forma corta de la operación forzada. |
| `--list` | Incluye información adicional en la salida. |
| `--verbose` | Aumenta el detalle enviado a la salida. |
| `--quiet` | Reduce mensajes que no representan errores. |

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

Persistencia: Envía datos a un sistema externo; no crea commits por sí mismo. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

## Práctica guiada

Genera una serie de dos commits en una rama de prueba. Inspecciona los archivos de parche y aplícalos en otro clon.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git send-email`](../email-and-patches/send-email.md)
- [`git format-patch`](../email-and-patches/format-patch.md)
- [`git am`](../email-and-patches/am.md)

## Fuente

- [git-imap-send - Send a collection of patches from stdin to an IMAP folder](https://git-scm.com/docs/git-imap-send)
