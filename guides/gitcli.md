---
title: "Convenciones de la interfaz de Git"
source: "https://git-scm.com/docs/gitcli"
section: "guides"
status: "reviewed"
version: "2.55.0"
---

# Convenciones de la interfaz de Git

Git analiza una invocación en este orden: opciones globales, comando, opciones del comando y argumentos. Estas reglas se aplican a las demás guías y evitan repetir la misma explicación en cada opción.

```text
git [opciones globales] <comando> [opciones del comando] [argumentos]
```

## Laboratorio

Ejecuta los ejemplos que necesitan archivos dentro del [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base). Los ejemplos que solo consultan la versión o la ayuda funcionan fuera de un repositorio.

## Orden de opciones y argumentos

Escribe las opciones antes de los argumentos. Algunos comandos aceptan otro orden, pero un script no debe depender de esa tolerancia porque una opción nueva puede volver ambigua una invocación anterior.

```bash
git log --oneline --max-count=2 HEAD
```

`--oneline` y `--max-count=2` son opciones de `log`; `HEAD` es la revisión consultada.

Las opciones globales se escriben antes del comando. `-C` cambia de directorio y `-c` añade una configuración para esa invocación.

```bash
git -C ../proyecto -c color.ui=false status --short
```

Esta orden ejecuta `status` dentro de `../proyecto` sin guardar `color.ui=false` en ningún archivo de configuración.

## Revisiones, rangos y rutas

Cuando un comando acepta revisiones y rutas, escribe primero las revisiones y después las rutas. El separador `--` termina las opciones y separa ambos grupos.

```bash
git diff HEAD~1 HEAD -- docs/guia.md
```

El ejemplo compara dos commits y limita el resultado a `docs/guia.md`. La guía de [revisiones y rangos](gitrevisions.md#revisiones-y-rangos) explica expresiones como `HEAD~1`, `A..B` y `A...B`.

Usa `--` aunque solo haya una ruta cuando su nombre pueda confundirse con una revisión u opción.

```bash
printf 'dato\n' > ./-entrada.txt
git add -- ./-entrada.txt
git status --short
```

La salida de `status` contiene `A  -entrada.txt`. Sin el separador, Git intentaría interpretar `-entrada.txt` como una opción.

`--end-of-options` ofrece una protección equivalente para comandos que lo admiten cuando el argumento posterior debe interpretarse como una revisión.

```bash
git rev-parse --verify --end-of-options refs/heads/main
```

## Pathspecs y expansión del shell

Un pathspec selecciona rutas para el comando. Las comillas determinan si el shell expande un patrón antes de invocar Git.

```bash
git ls-files '*.md'
git ls-files -- ':(top)guides/*.md'
```

En la primera orden, Git recibe `*.md` y aplica el patrón de forma recursiva. En la segunda, la firma mágica `top` fija la raíz del patrón en el nivel superior del repositorio. Sin comillas, el shell podría sustituir el patrón por los nombres que coincidan en el directorio actual.

Para inspeccionar qué rutas selecciona un pathspec sin ejecutar una operación de escritura, usa `git ls-files -- <pathspec>`.

## Valores obligatorios y opcionales

Una opción con valor obligatorio acepta normalmente el valor separado o unido con `=`. Las opciones cortas pueden aceptar el valor pegado o separado.

```bash
git log --max-count=2
git log --max-count 2
git log -n2
git log -n 2
```

Una opción con valor opcional necesita `=` en su forma larga cuando proporcionas el valor. De otro modo, el siguiente argumento conserva su propia función.

```bash
git describe --abbrev HEAD
git describe --abbrev=10 HEAD
```

La primera orden activa `--abbrev` con su valor predeterminado y describe `HEAD`. La segunda fija la abreviatura en diez caracteres. `git describe --abbrev 10 HEAD` intentaría describir las revisiones `10` y `HEAD`.

## Alias cortos y opciones agrupadas

Las formas corta y larga que aparecen juntas en la sintaxis son alias. Un solo ejemplo basta para el comportamiento compartido; la guía de cada comando enumera ambas formas.

```bash
git status --short
git status -s
```

Ambas órdenes solicitan el formato corto. Los comandos que usan el analizador ampliado también permiten agrupar opciones cortas sin valor.

```bash
git clean -n -d
git clean -nd
```

Ambas órdenes simulan la limpieza e incluyen directorios. No agrupes una opción corta con valor sin comprobar cómo el comando separa ese valor.

## Negación de opciones

El analizador ampliado permite anteponer `--no-` a muchas opciones largas. La negación restaura o desactiva el comportamiento de la forma positiva; no constituye una función independiente.

```bash
git branch --track tema origin/main
git branch --no-track local main
```

La primera orden configura el upstream de `tema`. La segunda crea `local` sin configuración de seguimiento. Usa una forma `--no-...` solo cuando la sintaxis o el manual del comando defina el efecto que se desactiva.

## Abreviaturas de opciones largas

Algunos comandos aceptan un prefijo inequívoco de una opción larga. La abreviatura puede dejar de ser inequívoca cuando una versión posterior añade otra opción, por lo que los scripts deben usar el nombre completo.

```bash
git commit --amend
```

`--amend` permanece estable aunque aparezca otra opción que comience por `--amen`.

## Opciones que reciben archivos

Las opciones de archivo admiten el prefijo mágico `:(optional)` en los comandos que siguen la convención de `gitcli`. Si el archivo no existe, Git trata la opción como ausente.

```bash
git commit -F ':(optional)COMMIT_EDITMSG'
```

Consulta el manual del comando antes de usar esta forma: el archivo y la ausencia de la opción deben producir un resultado válido para ese flujo.

## Ayuda y opciones ocultas

`-h` muestra la sintaxis breve. `--help` abre el manual completo y `--help-all` incluye opciones de plomería u obsoletas que la ayuda normal puede ocultar.

```bash
git add -h
git add --help
git add --help-all
```

La salida depende de la versión instalada. Estas guías toman Git 2.55.0 como referencia; comprueba `git --version` antes de usar una opción en automatización.

## Salida y códigos de terminación

Una salida vacía no implica por sí sola un error. Un script debe conservar stdout, stderr y el código de terminación inmediatamente después del comando.

```bash
git rev-parse --verify --quiet refs/heads/no-existe
status=$?
printf 'exit=%s\n' "$status"
```

En un shell POSIX, el ejemplo imprime un estado distinto de cero y `--quiet` evita el diagnóstico normal. PowerShell expone el código del último programa nativo en `$LASTEXITCODE`.

## Ejemplos destructivos e interactivos

Ejecuta una opción que escriba estado en un repositorio desechable. Registra antes `git status --short`, `git diff`, `git diff --cached` y, si cambiarán referencias, `git show-ref`. Las opciones `--dry-run` o `-n` solo simulan una operación cuando el manual del comando lo afirma.

Una opción interactiva necesita entrada del usuario y no sirve como ejemplo desatendido. La guía correspondiente indica qué seleccionar y qué salida o cambio permite comprobar el resultado.

## Fuente

- [gitcli 2.55.0 — convenciones de la línea de comandos](https://git-scm.com/docs/gitcli/2.55.0)
