---
title: "git send-email"
source: "https://git-scm.com/docs/git-send-email"
section: "email-and-patches"
status: "option-expanded"
---

# `git send-email`

Este caso usa `git send-email` para enviar parches por correo electrónico. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Responsabilidad y efecto

git send-email genera, transporta o aplica series de parches conservando autoría y orden. Recibe como entrada una serie de commits, parches o mensajes de correo. La operación consiste en enviar parches por correo electrónico.

Envía datos a un sistema externo; no crea commits por sí mismo.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). La posición de opciones, revisiones y rutas sigue las [convenciones de la interfaz de Git](../guides/gitcli.md#convenciones-de-la-cli). La selección de rutas se explica en [pathspecs y separación con `--`](../guides/gitcli.md#pathspecs). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

Cada parche puede transportar autoría, mensaje y diferencias. El receptor valida, aplica y registra la serie en su propio historial.

Conserva el orden de la serie y separa autor de quien aplica el parche. Los conflictos se resuelven antes de continuar con el siguiente mensaje.

## Ejemplo mínimo

```bash
git send-email --to=user@example.com parches/*.patch
```

La invocación `git send-email --to=user@example.com parches/*.patch` ejecuta esta operación: enviar parches por correo electrónico. Después, el receptor obtiene parches o commits con el orden, autoría y mensaje esperados. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
git send-email [<options>] (<file>|<directory>)…
git send-email [<options>] <format-patch-options>
git send-email --dump-aliases
git send-email --translate-aliases
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git send-email -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

enviar parches por correo electrónico. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### Alcance explícito

Aplicar git send-email a una referencia, rango o ruta identificada. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Resuelve cada argumento antes de ejecutar y usa `--` para rutas.

### Simulación

Calcular el efecto sin escribir el estado principal. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Compara la simulación con la selección prevista.

### Validación

Comprobar el resultado de git send-email con una orden de lectura independiente. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. No uses la misma salida como única prueba del cambio.

## Opciones

Cada apartado usa una opción en una invocación concreta. Las opciones equivalentes comparten la explicación, pero cada alias tiene su propio ejemplo. Ejecuta una opción por vez antes de combinarlas.

### `--dump-aliases`

Activa dump aliases durante enviar parches por correo electrónico. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `* Dump configured aliases and exit.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git send-email`, dump aliases modifica la forma en que se ejecuta enviar parches por correo electrónico. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git send-email --dump-aliases --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-email` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--translate-aliases`

Lee translate aliases como parte de la entrada de `git send-email`. En Git 2.51.1, la ayuda corta expresa el contrato como `* Translate aliases read from standard input according to the configured email`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia cómo `git send-email` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git send-email --translate-aliases --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-email` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--from`

Activa from durante enviar parches por correo electrónico. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `<str> * Email From:`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git send-email`, from modifica la forma en que se ejecuta enviar parches por correo electrónico. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git send-email --from --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-email` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--to`

Activa to durante enviar parches por correo electrónico. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `<str> * Email To:`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git send-email`, to modifica la forma en que se ejecuta enviar parches por correo electrónico. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git send-email --to --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-email` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--cc`

Activa cc durante enviar parches por correo electrónico. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `<str> * Email Cc:`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git send-email`, cc modifica la forma en que se ejecuta enviar parches por correo electrónico. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git send-email --cc --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-email` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--bcc`

Activa bcc durante enviar parches por correo electrónico. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `<str> * Email Bcc:`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git send-email`, bcc modifica la forma en que se ejecuta enviar parches por correo electrónico. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git send-email --bcc --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-email` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--subject`

Activa subject durante enviar parches por correo electrónico. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `<str> * Email "Subject:"`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git send-email`, subject modifica la forma en que se ejecuta enviar parches por correo electrónico. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git send-email --subject --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-email` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--reply-to`

Activa reply to durante enviar parches por correo electrónico. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `<str> * Email "Reply-To:"`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git send-email`, reply to modifica la forma en que se ejecuta enviar parches por correo electrónico. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git send-email --reply-to --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-email` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--in-reply-to`

Activa in reply to durante enviar parches por correo electrónico. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `<str> * Email "In-Reply-To:"`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git send-email`, in reply to modifica la forma en que se ejecuta enviar parches por correo electrónico. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git send-email --in-reply-to --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-email` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--outlook-id-fix`

Obtiene outlook id fix desde el origen indicado para esta invocación. En Git 2.51.1, la ayuda corta expresa el contrato como `* The SMTP host is an Outlook server that munges the Message-ID. Retrieve it from the server.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git send-email`, outlook id fix modifica la forma en que se ejecuta enviar parches por correo electrónico. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git send-email --outlook-id-fix --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-email` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--xmailer`

Incluye xmailer en la entrada, el resultado o el registro que construye `git send-email`. En Git 2.51.1, la ayuda corta expresa el contrato como `* Add "X-Mailer:" header (default).`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git send-email`, xmailer modifica la forma en que se ejecuta enviar parches por correo electrónico. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git send-email --xmailer --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-email` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--annotate`

Activa annotate durante enviar parches por correo electrónico. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `* Review each patch that will be sent in an editor.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git send-email`, annotate modifica la forma en que se ejecuta enviar parches por correo electrónico. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git send-email --annotate --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-email` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--compose`

Activa compose durante enviar parches por correo electrónico. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `* Open an editor for introduction.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git send-email`, compose modifica la forma en que se ejecuta enviar parches por correo electrónico. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git send-email --compose --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-email` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--compose-encoding`

Activa compose encoding durante enviar parches por correo electrónico. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `<str> * Encoding to assume for introduction.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git send-email`, compose encoding modifica la forma en que se ejecuta enviar parches por correo electrónico. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git send-email --compose-encoding --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-email` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--8bit-encoding`

Activa 8bit encoding durante enviar parches por correo electrónico. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `<str> * Encoding to assume 8bit mails if undeclared`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git send-email`, 8bit encoding modifica la forma en que se ejecuta enviar parches por correo electrónico. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git send-email --8bit-encoding --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-email` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--transfer-encoding`

Define transfer encoding para esta ejecución de `git send-email`. En Git 2.51.1, la ayuda corta expresa el contrato como `<str> * Transfer encoding to use (quoted-printable, 8bit, base64)`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git send-email --transfer-encoding --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-email` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--mailmap`

Define mailmap para esta ejecución de `git send-email`. En Git 2.51.1, la ayuda corta expresa el contrato como `* Use mailmap file to map all email addresses to canonical real names and email addresses.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción limita o amplía el conjunto sobre el que se ejecuta enviar parches por correo electrónico. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git send-email --mailmap --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-email` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--envelope-sender`

Activa envelope sender durante enviar parches por correo electrónico. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `<str> * Email envelope sender.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git send-email`, envelope sender modifica la forma en que se ejecuta enviar parches por correo electrónico. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git send-email --envelope-sender --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-email` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--sendmail-cmd`

Ejecuta sendmail cmd durante enviar parches por correo electrónico. En Git 2.51.1, la ayuda corta expresa el contrato como `<str> * Command to run to send email.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git send-email`, sendmail cmd modifica la forma en que se ejecuta enviar parches por correo electrónico. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git send-email --sendmail-cmd --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-email` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--smtp-server`

Define smtp server para esta ejecución de `git send-email`. En Git 2.51.1, la ayuda corta expresa el contrato como `<str:int> * Outgoing SMTP server to use. The port is optional. Default 'localhost'.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git send-email`, smtp server modifica la forma en que se ejecuta enviar parches por correo electrónico. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git send-email --smtp-server --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-email` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--smtp-server-option`

Define smtp server option para esta ejecución de `git send-email`. En Git 2.51.1, la ayuda corta expresa el contrato como `<str> * Outgoing SMTP server option to use.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git send-email`, smtp server option modifica la forma en que se ejecuta enviar parches por correo electrónico. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git send-email --smtp-server-option --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-email` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--smtp-server-port`

Activa smtp server port durante enviar parches por correo electrónico. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `<int> * Outgoing SMTP server port.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git send-email`, smtp server port modifica la forma en que se ejecuta enviar parches por correo electrónico. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git send-email --smtp-server-port --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-email` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--smtp-user`

Activa smtp user durante enviar parches por correo electrónico. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `<str> * Username for SMTP-AUTH.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git send-email`, smtp user modifica la forma en que se ejecuta enviar parches por correo electrónico. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git send-email --smtp-user --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-email` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--smtp-pass`

Activa smtp pass durante enviar parches por correo electrónico. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `<str> * Password for SMTP-AUTH; not necessary.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git send-email`, smtp pass modifica la forma en que se ejecuta enviar parches por correo electrónico. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git send-email --smtp-pass --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-email` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--smtp-encryption`

Activa smtp encryption durante enviar parches por correo electrónico. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `<str> * tls or ssl; anything else disables.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git send-email`, smtp encryption modifica la forma en que se ejecuta enviar parches por correo electrónico. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git send-email --smtp-encryption --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-email` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--smtp-ssl`

Define smtp ssl para esta ejecución de `git send-email`. En Git 2.51.1, la ayuda corta expresa el contrato como `* Deprecated. Use '--smtp-encryption ssl'.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git send-email`, smtp ssl modifica la forma en que se ejecuta enviar parches por correo electrónico. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git send-email --smtp-ssl --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-email` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--smtp-ssl-cert-path`

Define smtp ssl cert ruta con el valor que recibe la opción. En Git 2.51.1, la ayuda corta expresa el contrato como `<str> * Path to ca-certificates (either directory or file). Pass an empty string to disable certificate`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia cómo `git send-email` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git send-email --smtp-ssl-cert-path --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-email` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--smtp-domain`

Activa smtp domain durante enviar parches por correo electrónico. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `<str> * The domain name sent to HELO/EHLO handshake`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git send-email`, smtp domain modifica la forma en que se ejecuta enviar parches por correo electrónico. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git send-email --smtp-domain --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-email` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--smtp-auth`

Impide smtp auth durante esta invocación de `git send-email`. En Git 2.51.1, la ayuda corta expresa el contrato como `<str> * Space-separated list of allowed AUTH mechanisms, or "none" to disable authentication.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción limita o amplía el conjunto sobre el que se ejecuta enviar parches por correo electrónico. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git send-email --smtp-auth --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-email` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-smtp-auth`

Desactiva el comportamiento `smtp-auth` para esta invocación.

La opción limita o amplía el conjunto sobre el que se ejecuta enviar parches por correo electrónico. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git send-email --no-smtp-auth --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-email` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--smtp-debug`

Impide smtp debug durante esta invocación de `git send-email`. En Git 2.51.1, la ayuda corta expresa el contrato como `<0|1> * Disable, enable Net::SMTP debug.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git send-email`, smtp debug modifica la forma en que se ejecuta enviar parches por correo electrónico. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git send-email --smtp-debug --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-email` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--batch-size`

Activa batch size durante enviar parches por correo electrónico. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `<int> * send max <int> message per connection.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia cómo `git send-email` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git send-email --batch-size --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-email` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--relogin-delay`

Limita enviar parches por correo electrónico al alcance identificado por relogin delay. En Git 2.51.1, la ayuda corta expresa el contrato como `<int> * delay <int> seconds between two successive login. This option can only be used with --batch-size`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia cómo `git send-email` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git send-email --relogin-delay --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-email` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--identity`

Define identity para esta ejecución de `git send-email`. En Git 2.51.1, la ayuda corta expresa el contrato como `<str> * Use the sendemail.<id> options.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git send-email`, identity modifica la forma en que se ejecuta enviar parches por correo electrónico. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git send-email --identity --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-email` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--to-cmd`

Activa to cmd durante enviar parches por correo electrónico. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `<str> * Email To: via `<str> $patch_path`.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git send-email`, to cmd modifica la forma en que se ejecuta enviar parches por correo electrónico. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git send-email --to-cmd --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-email` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--cc-cmd`

Activa cc cmd durante enviar parches por correo electrónico. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `<str> * Email Cc: via `<str> $patch_path`.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git send-email`, cc cmd modifica la forma en que se ejecuta enviar parches por correo electrónico. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git send-email --cc-cmd --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-email` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--header-cmd`

Incluye header cmd en la entrada, el resultado o el registro que construye `git send-email`. En Git 2.51.1, la ayuda corta expresa el contrato como `<str> * Add headers via `<str> $patch_path`.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git send-email`, header cmd modifica la forma en que se ejecuta enviar parches por correo electrónico. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git send-email --header-cmd --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-email` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-header-cmd`

Desactiva el comportamiento `header-cmd` para esta invocación.

En `git send-email`, desactivar header cmd modifica la forma en que se ejecuta enviar parches por correo electrónico. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git send-email --no-header-cmd --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-email` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--suppress-cc`

Suprime suppress cc en la salida de esta invocación de `git send-email`. En Git 2.51.1, la ayuda corta expresa el contrato como `<str> * author, self, sob, cc, cccmd, body, bodycc, misc-by, all.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción limita o amplía el conjunto sobre el que se ejecuta enviar parches por correo electrónico. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git send-email --suppress-cc --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-email` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--cc-cover`

Activa cc cover durante enviar parches por correo electrónico. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `* Email Cc: addresses in the cover letter.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git send-email`, cc cover modifica la forma en que se ejecuta enviar parches por correo electrónico. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git send-email --cc-cover --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-email` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--to-cover`

Activa to cover durante enviar parches por correo electrónico. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `* Email To: addresses in the cover letter.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git send-email`, to cover modifica la forma en que se ejecuta enviar parches por correo electrónico. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git send-email --to-cover --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-email` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--signed-off-by-cc`

Activa firmado off by cc durante enviar parches por correo electrónico. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `* Send to Signed-off-by: addresses. Default on.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git send-email`, firmado off by cc modifica la forma en que se ejecuta enviar parches por correo electrónico. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git send-email --signed-off-by-cc --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-email` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--suppress-from`

Suprime suppress from en la salida de esta invocación de `git send-email`. En Git 2.51.1, la ayuda corta expresa el contrato como `* Send to self. Default off.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git send-email`, suppress from modifica la forma en que se ejecuta enviar parches por correo electrónico. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git send-email --suppress-from --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-email` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--chain-reply-to`

Activa chain reply to durante enviar parches por correo electrónico. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `* Chain In-Reply-To: fields. Default off.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git send-email`, chain reply to modifica la forma en que se ejecuta enviar parches por correo electrónico. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git send-email --chain-reply-to --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-email` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--thread`

Define thread para esta ejecución de `git send-email`. En Git 2.51.1, la ayuda corta expresa el contrato como `* Use In-Reply-To: field. Default on.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git send-email`, thread modifica la forma en que se ejecuta enviar parches por correo electrónico. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git send-email --thread --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-email` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--confirm`

Activa confirm durante enviar parches por correo electrónico. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `<str> * Confirm recipients before sending; auto, cc, compose, always, or never.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git send-email`, confirm modifica la forma en que se ejecuta enviar parches por correo electrónico. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git send-email --confirm --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-email` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--quiet`

Reduce mensajes que no representan errores.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git send-email --quiet --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-email` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--dry-run`

Calcula el alcance y muestra lo que ocurriría sin aplicar el cambio.

La opción limita o amplía el conjunto sobre el que se ejecuta enviar parches por correo electrónico. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git send-email --dry-run --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-email` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--validate`

Valida el dato o estado antes de producir el resultado.

La opción añade, retira o consulta una comprobación previa. Ejecuta primero la forma que no escribe cuando exista y conserva el código de terminación como parte del resultado.

```bash
git send-email --validate --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-email` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--format-patch`

Activa formato parche durante enviar parches por correo electrónico. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `* understand any non optional arguments as `git format-patch` ones.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git send-email --format-patch --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-email` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--force`

Omite una protección concreta; úsala solo después de verificar el estado objetivo.

La opción controla omitir la protección. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque enviar parches por correo electrónico puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git send-email --force --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-email` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-to`

Desactiva para esta invocación el comportamiento que habilita `--to`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git send-email`, desactivar to modifica la forma en que se ejecuta enviar parches por correo electrónico. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git send-email --no-to --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-email` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-cc`

Desactiva para esta invocación el comportamiento que habilita `--cc`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git send-email`, desactivar cc modifica la forma en que se ejecuta enviar parches por correo electrónico. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git send-email --no-cc --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-email` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-bcc`

Desactiva para esta invocación el comportamiento que habilita `--bcc`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git send-email`, desactivar bcc modifica la forma en que se ejecuta enviar parches por correo electrónico. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git send-email --no-bcc --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-email` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-outlook-id-fix`

Desactiva para esta invocación el comportamiento que habilita `--outlook-id-fix`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git send-email`, desactivar outlook id fix modifica la forma en que se ejecuta enviar parches por correo electrónico. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git send-email --no-outlook-id-fix --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-email` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-xmailer`

Desactiva para esta invocación el comportamiento que habilita `--xmailer`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git send-email`, desactivar xmailer modifica la forma en que se ejecuta enviar parches por correo electrónico. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git send-email --no-xmailer --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-email` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-annotate`

Desactiva para esta invocación el comportamiento que habilita `--annotate`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git send-email`, desactivar annotate modifica la forma en que se ejecuta enviar parches por correo electrónico. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git send-email --no-annotate --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-email` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-mailmap`

Desactiva para esta invocación el comportamiento que habilita `--mailmap`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta enviar parches por correo electrónico. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git send-email --no-mailmap --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-email` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-cc-cover`

Desactiva para esta invocación el comportamiento que habilita `--cc-cover`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git send-email`, desactivar cc cover modifica la forma en que se ejecuta enviar parches por correo electrónico. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git send-email --no-cc-cover --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-email` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-to-cover`

Desactiva para esta invocación el comportamiento que habilita `--to-cover`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git send-email`, desactivar to cover modifica la forma en que se ejecuta enviar parches por correo electrónico. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git send-email --no-to-cover --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-email` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-signed-off-by-cc`

Desactiva para esta invocación el comportamiento que habilita `--signed-off-by-cc`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git send-email`, desactivar firmado off by cc modifica la forma en que se ejecuta enviar parches por correo electrónico. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git send-email --no-signed-off-by-cc --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-email` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-suppress-from`

Desactiva para esta invocación el comportamiento que habilita `--suppress-from`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git send-email`, desactivar suppress from modifica la forma en que se ejecuta enviar parches por correo electrónico. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git send-email --no-suppress-from --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-email` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-chain-reply-to`

Desactiva para esta invocación el comportamiento que habilita `--chain-reply-to`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git send-email`, desactivar chain reply to modifica la forma en que se ejecuta enviar parches por correo electrónico. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git send-email --no-chain-reply-to --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-email` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-thread`

Desactiva para esta invocación el comportamiento que habilita `--thread`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git send-email`, desactivar thread modifica la forma en que se ejecuta enviar parches por correo electrónico. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git send-email --no-thread --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-email` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-validate`

Desactiva para esta invocación el comportamiento que habilita `--validate`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción añade, retira o consulta una comprobación previa. Ejecuta primero la forma que no escribe cuando exista y conserva el código de terminación como parte del resultado.

```bash
git send-email --no-validate --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-email` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-format-patch`

Desactiva para esta invocación el comportamiento que habilita `--format-patch`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git send-email --no-format-patch --to=user@example.com parches/*.patch
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-email` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Errores y diagnóstico

### La numeración no coincide

Comprueba esta causa: El rango o la revisión de la serie cambió. Regenera la serie completa con el mismo punto base.

### La aplicación se detiene

Comprueba esta causa: El parche no coincide o falta información de autor. Corrige el parche o resuelve y continúa la sesión.

### El transporte rechaza el mensaje

Comprueba esta causa: La configuración SMTP o IMAP no autoriza la operación. Prueba autenticación fuera del contenido del mensaje y evita secretos en argumentos.

## Automatización y recuperación

Persistencia: Envía datos a un sistema externo; no crea commits por sí mismo. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

Genera una serie de dos commits en una rama de prueba. Inspecciona los archivos de parche y aplícalos en otro clon.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git imap-send`](../email-and-patches/imap-send.md)
- [`git format-patch`](../email-and-patches/format-patch.md)

## Fuente

- [git-send-email - Send a collection of patches as emails](https://git-scm.com/docs/git-send-email)
