---
title: "git send-email"
source: "https://git-scm.com/docs/git-send-email"
section: "email-and-patches"
status: "expanded"
---

# `git send-email`

Este caso usa `git send-email` para enviar parches por correo electrónico. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Alcance y responsabilidad

git send-email genera, transporta o aplica series de parches conservando autoría y orden. Recibe como entrada una serie de commits, parches o mensajes de correo. La operación consiste en enviar parches por correo electrónico.

La página distingue lectura, escritura y resultado:

| Elemento | Relación con la función | Comprobación |
| --- | --- | --- |
| Entrada | una serie de commits, parches o mensajes de correo. | Registra los argumentos y resuelve revisiones antes de ejecutar. |
| Efecto principal | enviar parches por correo electrónico. | Comprueba el resultado con una orden de lectura. |
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
git send-email --to=lista@example.test parches/*.patch
```

Ejecuta el bloque en orden. Conserva los nombres del laboratorio hasta confirmar el resultado. Sustituye rutas, revisiones o URL solo después de identificar su tipo y alcance.

### Resultado esperado

- La entrada queda limitada a: una serie de commits, parches o mensajes de correo.
- La operación observable es: enviar parches por correo electrónico.
- La comprobación se realiza mediante: el receptor obtiene parches o commits con el orden, autoría y mensaje esperados.
- stdout contiene datos o confirmaciones; stderr contiene diagnósticos. Captura ambos canales cuando automatices.

## Sintaxis

```text
git send-email [<options>] (<file>|<directory>)…
git send-email [<options>] <format-patch-options>
git send-email --dump-aliases
git send-email --translate-aliases
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git send-email -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Casos de uso

| Caso | Objetivo | Criterio de verificación |
| --- | --- | --- |
| Caso base | enviar parches por correo electrónico | Ejecuta el ejemplo mínimo y registra el estado antes y después. |
| Alcance explícito | Aplicar git send-email a una referencia, rango o ruta identificada. | Resuelve cada argumento antes de ejecutar y usa `--` para rutas. |
| Simulación | Calcular el efecto sin escribir el estado principal. | Compara la simulación con la selección prevista. |
| Validación | Comprobar el resultado de git send-email con una orden de lectura independiente. | No uses la misma salida como única prueba del cambio. |


## Opciones y variaciones

La tabla agrupa las opciones visibles en la sintaxis y en la ayuda corta. Una opción puede tener un significado propio cuando la página lo define; ejecuta la ayuda de tu versión antes de usarla en automatización.

| Opción | Efecto que debes controlar |
| --- | --- |
| `--dump-aliases` | Activa el modo `--dump-aliases`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--translate-aliases` | Activa el modo `--translate-aliases`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--from` | Activa el modo `--from`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--to` | Activa el modo `--to`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--cc` | Activa el modo `--cc`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--bcc` | Activa el modo `--bcc`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--subject` | Activa el modo `--subject`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--reply-to` | Activa el modo `--reply-to`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--in-reply-to` | Activa el modo `--in-reply-to`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--outlook-id-fix` | Activa el modo `--outlook-id-fix`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--xmailer` | Activa el modo `--xmailer`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--annotate` | Activa el modo `--annotate`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--compose` | Activa el modo `--compose`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--compose-encoding` | Activa el modo `--compose-encoding`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--8bit-encoding` | Activa el modo `--8bit-encoding`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--transfer-encoding` | Activa el modo `--transfer-encoding`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--mailmap` | Activa el modo `--mailmap`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--envelope-sender` | Activa el modo `--envelope-sender`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--sendmail-cmd` | Activa el modo `--sendmail-cmd`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--smtp-server` | Activa el modo `--smtp-server`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--smtp-server-option` | Activa el modo `--smtp-server-option`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--smtp-server-port` | Activa el modo `--smtp-server-port`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--smtp-user` | Activa el modo `--smtp-user`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--smtp-pass` | Activa el modo `--smtp-pass`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--smtp-encryption` | Activa el modo `--smtp-encryption`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--smtp-ssl` | Activa el modo `--smtp-ssl`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--smtp-ssl-cert-path` | Activa el modo `--smtp-ssl-cert-path`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--smtp-domain` | Activa el modo `--smtp-domain`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--smtp-auth` | Activa el modo `--smtp-auth`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--no-smtp-auth` | Desactiva el comportamiento `smtp-auth` para esta invocación. |
| `--smtp-debug` | Activa el modo `--smtp-debug`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--batch-size` | Activa el modo `--batch-size`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--relogin-delay` | Activa el modo `--relogin-delay`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--identity` | Activa el modo `--identity`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--to-cmd` | Activa el modo `--to-cmd`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--cc-cmd` | Activa el modo `--cc-cmd`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--header-cmd` | Activa el modo `--header-cmd`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--no-header-cmd` | Desactiva el comportamiento `header-cmd` para esta invocación. |
| `--suppress-cc` | Activa el modo `--suppress-cc`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--cc-cover` | Activa el modo `--cc-cover`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--to-cover` | Activa el modo `--to-cover`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--signed-off-by-cc` | Activa el modo `--signed-off-by-cc`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--suppress-from` | Activa el modo `--suppress-from`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--chain-reply-to` | Activa el modo `--chain-reply-to`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--thread` | Activa el modo `--thread`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--confirm` | Activa el modo `--confirm`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--quiet` | Reduce mensajes que no representan errores. |
| `--dry-run` | Calcula el alcance y muestra lo que ocurriría sin aplicar el cambio. |
| `--validate` | Valida el dato o estado antes de producir el resultado. |
| `--format-patch` | Controla campos, orden o representación del resultado. |
| `--force` | Omite una protección concreta; úsala solo después de verificar el estado objetivo. |

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

- [`git imap-send`](../email-and-patches/imap-send.md)
- [`git format-patch`](../email-and-patches/format-patch.md)

## Fuente

- [git-send-email - Send a collection of patches as emails](https://git-scm.com/docs/git-send-email)
