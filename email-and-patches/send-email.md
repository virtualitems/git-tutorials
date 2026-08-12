---
title: "git send-email"
source: "https://git-scm.com/docs/git-send-email"
section: "email-and-patches"
status: "source-audited"
version: "2.55.0"
---

# `git send-email`

Este caso usa `git send-email` para enviar parches por correo electrónico.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Cada parche puede transportar autoría, mensaje y diferencias. El receptor valida, aplica y registra la serie en su propio historial.

Conserva el orden de la serie y separa autor de quien aplica el parche. Los conflictos se resuelven antes de continuar con el siguiente mensaje.

## Ejemplo mínimo

```bash
git send-email --to=user@example.com parches/*.patch
```

La invocación `git send-email --to=user@example.com parches/*.patch` ejecuta esta operación: enviar parches por correo electrónico. Después, el receptor obtiene parches o commits con el orden, autoría y mensaje esperados.

## Sintaxis y formas de invocación

```text
git send-email [<options>] (<file>|<directory>)…
git send-email [<options>] <format-patch-options>
git send-email --dump-aliases
git send-email --translate-aliases
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git send-email -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `--dump-aliases`

Activa dump aliases durante enviar parches por correo electrónico. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `* Dump configured aliases and exit.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git send-email --dump-aliases --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

### `--translate-aliases`

Lee translate aliases como parte de la entrada de `git send-email`. En Git 2.51.1, la ayuda corta expresa el contrato como `* Translate aliases read from standard input according to the configured email`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia cómo `git send-email` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git send-email --translate-aliases --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

### `--from`

Activa from durante enviar parches por correo electrónico. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `<str> * Email From:`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git send-email --from --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

### `--to`

Activa to durante enviar parches por correo electrónico. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `<str> * Email To:`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git send-email --to --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

### `--cc`

Activa cc durante enviar parches por correo electrónico. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `<str> * Email Cc:`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git send-email --cc --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

### `--bcc`

Activa bcc durante enviar parches por correo electrónico. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `<str> * Email Bcc:`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git send-email --bcc --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

### `--subject`

Activa subject durante enviar parches por correo electrónico. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `<str> * Email "Subject:"`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git send-email --subject --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

### `--reply-to`

Activa reply to durante enviar parches por correo electrónico. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `<str> * Email "Reply-To:"`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git send-email --reply-to --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

### `--in-reply-to`

Activa in reply to durante enviar parches por correo electrónico. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `<str> * Email "In-Reply-To:"`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git send-email --in-reply-to --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

### `--outlook-id-fix`

Obtiene outlook id fix desde el origen indicado para esta invocación. En Git 2.51.1, la ayuda corta expresa el contrato como `* The SMTP host is an Outlook server that munges the Message-ID. Retrieve it from the server.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git send-email --outlook-id-fix --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

### `--xmailer`

Incluye xmailer en la entrada, el resultado o el registro que construye `git send-email`. En Git 2.51.1, la ayuda corta expresa el contrato como `* Add "X-Mailer:" header (default).`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git send-email --xmailer --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

### `--annotate`

Activa annotate durante enviar parches por correo electrónico. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `* Review each patch that will be sent in an editor.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git send-email --annotate --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

### `--compose`

Activa compose durante enviar parches por correo electrónico. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `* Open an editor for introduction.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git send-email --compose --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

### `--compose-encoding`

Activa compose encoding durante enviar parches por correo electrónico. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `<str> * Encoding to assume for introduction.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git send-email --compose-encoding --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

### `--8bit-encoding`

Activa 8bit encoding durante enviar parches por correo electrónico. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `<str> * Encoding to assume 8bit mails if undeclared`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git send-email --8bit-encoding --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

### `--transfer-encoding`

Define transfer encoding para esta ejecución de `git send-email`. En Git 2.51.1, la ayuda corta expresa el contrato como `<str> * Transfer encoding to use (quoted-printable, 8bit, base64)`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git send-email --transfer-encoding --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

### `--mailmap`

Define mailmap para esta ejecución de `git send-email`. En Git 2.51.1, la ayuda corta expresa el contrato como `* Use mailmap file to map all email addresses to canonical real names and email addresses.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git send-email --mailmap --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

### `--envelope-sender`

Activa envelope sender durante enviar parches por correo electrónico. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `<str> * Email envelope sender.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git send-email --envelope-sender --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

### `--sendmail-cmd`

Ejecuta sendmail cmd durante enviar parches por correo electrónico. En Git 2.51.1, la ayuda corta expresa el contrato como `<str> * Command to run to send email.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git send-email --sendmail-cmd --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

### `--smtp-server`

Define smtp server para esta ejecución de `git send-email`. En Git 2.51.1, la ayuda corta expresa el contrato como `<str:int> * Outgoing SMTP server to use. The port is optional. Default 'localhost'.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git send-email --smtp-server --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

### `--smtp-server-option`

Define smtp server option para esta ejecución de `git send-email`. En Git 2.51.1, la ayuda corta expresa el contrato como `<str> * Outgoing SMTP server option to use.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git send-email --smtp-server-option --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

### `--smtp-server-port`

Activa smtp server port durante enviar parches por correo electrónico. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `<int> * Outgoing SMTP server port.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git send-email --smtp-server-port --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

### `--smtp-user`

Activa smtp user durante enviar parches por correo electrónico. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `<str> * Username for SMTP-AUTH.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git send-email --smtp-user --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

### `--smtp-pass`

Activa smtp pass durante enviar parches por correo electrónico. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `<str> * Password for SMTP-AUTH; not necessary.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git send-email --smtp-pass --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

### `--smtp-encryption`

Activa smtp encryption durante enviar parches por correo electrónico. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `<str> * tls or ssl; anything else disables.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git send-email --smtp-encryption --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

### `--smtp-ssl`

Define smtp ssl para esta ejecución de `git send-email`. En Git 2.51.1, la ayuda corta expresa el contrato como `* Deprecated. Use '--smtp-encryption ssl'.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git send-email --smtp-ssl --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

### `--smtp-ssl-cert-path`

Define smtp ssl cert ruta con el valor que recibe la opción. En Git 2.51.1, la ayuda corta expresa el contrato como `<str> * Path to ca-certificates (either directory or file). Pass an empty string to disable certificate`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia cómo `git send-email` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git send-email --smtp-ssl-cert-path --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

### `--smtp-domain`

Activa smtp domain durante enviar parches por correo electrónico. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `<str> * The domain name sent to HELO/EHLO handshake`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git send-email --smtp-domain --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

### `--smtp-auth`

Impide smtp auth durante esta invocación de `git send-email`. En Git 2.51.1, la ayuda corta expresa el contrato como `<str> * Space-separated list of allowed AUTH mechanisms, or "none" to disable authentication.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git send-email --smtp-auth --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

### `--smtp-debug`

Impide smtp debug durante esta invocación de `git send-email`. En Git 2.51.1, la ayuda corta expresa el contrato como `<0|1> * Disable, enable Net::SMTP debug.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git send-email --smtp-debug --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

### `--batch-size`

Activa batch size durante enviar parches por correo electrónico. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `<int> * send max <int> message per connection.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia cómo `git send-email` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git send-email --batch-size --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

### `--relogin-delay`

Limita enviar parches por correo electrónico al alcance identificado por relogin delay. En Git 2.51.1, la ayuda corta expresa el contrato como `<int> * delay <int> seconds between two successive login. This option can only be used with --batch-size`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia cómo `git send-email` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git send-email --relogin-delay --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

### `--identity`

Define identity para esta ejecución de `git send-email`. En Git 2.51.1, la ayuda corta expresa el contrato como `<str> * Use the sendemail.<id> options.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git send-email --identity --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

### `--to-cmd`

Activa to cmd durante enviar parches por correo electrónico. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `<str> * Email To: via `<str> $patch_path`.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git send-email --to-cmd --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

### `--cc-cmd`

Activa cc cmd durante enviar parches por correo electrónico. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `<str> * Email Cc: via `<str> $patch_path`.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git send-email --cc-cmd --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

### `--header-cmd`

Incluye header cmd en la entrada, el resultado o el registro que construye `git send-email`. En Git 2.51.1, la ayuda corta expresa el contrato como `<str> * Add headers via `<str> $patch_path`.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git send-email --header-cmd --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

### `--suppress-cc`

Suprime suppress cc en la salida de esta invocación de `git send-email`. En Git 2.51.1, la ayuda corta expresa el contrato como `<str> * author, self, sob, cc, cccmd, body, bodycc, misc-by, all.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git send-email --suppress-cc --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

### `--cc-cover`

Activa cc cover durante enviar parches por correo electrónico. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `* Email Cc: addresses in the cover letter.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git send-email --cc-cover --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

### `--to-cover`

Activa to cover durante enviar parches por correo electrónico. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `* Email To: addresses in the cover letter.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git send-email --to-cover --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

### `--signed-off-by-cc`

Activa firmado off by cc durante enviar parches por correo electrónico. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `* Send to Signed-off-by: addresses. Default on.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git send-email --signed-off-by-cc --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

### `--suppress-from`

Suprime suppress from en la salida de esta invocación de `git send-email`. En Git 2.51.1, la ayuda corta expresa el contrato como `* Send to self. Default off.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git send-email --suppress-from --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

### `--chain-reply-to`

Activa chain reply to durante enviar parches por correo electrónico. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `* Chain In-Reply-To: fields. Default off.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git send-email --chain-reply-to --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

### `--thread`

Define thread para esta ejecución de `git send-email`. En Git 2.51.1, la ayuda corta expresa el contrato como `* Use In-Reply-To: field. Default on.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git send-email --thread --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

### `--confirm`

Activa confirm durante enviar parches por correo electrónico. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `<str> * Confirm recipients before sending; auto, cc, compose, always, or never.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git send-email --confirm --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

### `--quiet`

Reduce mensajes que no representan errores.

```bash
git send-email --quiet --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

### `--dry-run`

Calcula el alcance y muestra lo que ocurriría sin aplicar el cambio.

```bash
git send-email --dry-run --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

### `--validate`

Valida el dato o estado antes de producir el resultado.

```bash
git send-email --validate --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

### `--format-patch`

Activa formato parche durante enviar parches por correo electrónico. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `* understand any non optional arguments as `git format-patch` ones.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git send-email --format-patch --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

### `--force`

Omite una protección concreta; úsala solo después de verificar el estado objetivo.

```bash
git send-email --force --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

### `--no-to`

Desactiva para esta invocación el comportamiento que habilita `--to`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git send-email --no-to --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

### `--no-cc`

Desactiva para esta invocación el comportamiento que habilita `--cc`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git send-email --no-cc --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

### `--no-outlook-id-fix`

Desactiva para esta invocación el comportamiento que habilita `--outlook-id-fix`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git send-email --no-outlook-id-fix --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

### `--no-mailmap`

Desactiva para esta invocación el comportamiento que habilita `--mailmap`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git send-email --no-mailmap --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

### `--no-cc-cover`

Desactiva para esta invocación el comportamiento que habilita `--cc-cover`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git send-email --no-cc-cover --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

### `--no-to-cover`

Desactiva para esta invocación el comportamiento que habilita `--to-cover`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git send-email --no-to-cover --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

### `--no-signed-off-by-cc`

Desactiva para esta invocación el comportamiento que habilita `--signed-off-by-cc`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git send-email --no-signed-off-by-cc --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

### `--no-suppress-from`

Desactiva para esta invocación el comportamiento que habilita `--suppress-from`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git send-email --no-suppress-from --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

### `--no-chain-reply-to`

Desactiva para esta invocación el comportamiento que habilita `--chain-reply-to`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git send-email --no-chain-reply-to --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

### `--no-thread`

Desactiva para esta invocación el comportamiento que habilita `--thread`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git send-email --no-thread --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

### `--no-format-patch`

Desactiva para esta invocación el comportamiento que habilita `--format-patch`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git send-email --no-format-patch --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

## Páginas relacionadas

- [`git imap-send`](../email-and-patches/imap-send.md)
- [`git format-patch`](../email-and-patches/format-patch.md)

## Fuente

- [git-send-email - Send a collection of patches as emails](https://git-scm.com/docs/git-send-email)
