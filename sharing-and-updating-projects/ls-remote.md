---
title: "git ls-remote"
source: "https://git-scm.com/docs/git-ls-remote"
section: "sharing-and-updating-projects"
status: "source-audited"
version: "2.55.0"
---

# `git ls-remote`

Este caso usa `git ls-remote` para enumerar referencias anunciadas por un repositorio remoto.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

La transferencia copia objetos y actualiza referencias. Descargar, integrar y publicar son operaciones separadas aunque algunos comandos las encadenen.

Distingue las referencias de seguimiento remoto de la rama actual. Descargar una referencia no integra por sí mismo sus commits.

## Ejemplo mínimo

```bash
git ls-remote --heads origin
```

La invocación `git ls-remote --heads origin` ejecuta esta operación: enumerar referencias anunciadas por un repositorio remoto. Después, las referencias locales y remotas permiten separar descarga, integración y publicación.

## Sintaxis y formas de invocación

```text
git ls-remote [--branches] [--tags] [--refs] [--upload-pack=<exec>]
	      [-q | --quiet] [--exit-code] [--get-url] [--sort=<key>]
	      [--symref] [<repository> [<patterns>…]]
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git ls-remote [--branches] [--tags] [--refs] [--upload-pack=<exec>]
                     [-q | --quiet] [--exit-code] [--get-url] [--sort=<key>]
                     [--symref] [<repository> [<patterns>...]]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git ls-remote -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `--branches` y `-b`

Incluye o selecciona ramas según la operación.

#### Ejemplo con `--branches`

```bash
git ls-remote --branches --heads origin
git branch -vv
```

 La salida permite comparar la rama local con su upstream.

### `--tags` y `-t`

Incluye o selecciona etiquetas según la operación.

#### Ejemplo con `--tags`

```bash
git ls-remote --tags --heads origin
git branch -vv
```

 La salida permite comparar la rama local con su upstream.

### `--refs`

Selecciona o modifica referencias dentro del alcance de la orden.

```bash
git ls-remote --refs --heads origin
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--upload-pack`

Activa upload pack durante enumerar referencias anunciadas por un repositorio remoto. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `path of git-upload-pack on the remote host`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git ls-remote --upload-pack=valor --heads origin
git branch -vv
```

### `-q` y `--quiet`

Reduce mensajes que no representan errores.

#### Ejemplo con `--quiet`

```bash
git ls-remote --quiet --heads origin
git branch -vv
```

 La salida permite comparar la rama local con su upstream.

### `--exit-code`

Activa exit code durante enumerar referencias anunciadas por un repositorio remoto. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `exit with exit code 2 if no matching refs are found`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git ls-remote --exit-code --heads origin
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--get-url`

Activa get url durante enumerar referencias anunciadas por un repositorio remoto. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `take url.<base>.insteadOf into account`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git ls-remote --get-url --heads origin
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--sort`

Ordena registros por el campo indicado.

```bash
git ls-remote --sort=user.name --heads origin
git branch -vv
```

El ejemplo usa `user.name` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--symref`

Incluye symref en la salida o cambia cómo `git ls-remote` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `show underlying ref in addition to the object pointed by it`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git ls-remote --symref --heads origin
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-o` y `--server-option`

Activa server option durante enumerar referencias anunciadas por un repositorio remoto. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `option to transmit`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--server-option`

```bash
git ls-remote --server-option=valor --heads origin
git branch -vv
```

En esta forma, `valor` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. La salida permite comparar la rama local con su upstream.

## Páginas relacionadas

- [`git pull`](../sharing-and-updating-projects/pull.md)
- [`git fetch`](../sharing-and-updating-projects/fetch.md)
- [`git push`](../sharing-and-updating-projects/push.md)

## Fuente

- [git-ls-remote - List references in a remote repository](https://git-scm.com/docs/git-ls-remote)
