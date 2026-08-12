---
title: "git remote"
source: "https://git-scm.com/docs/git-remote"
section: "sharing-and-updating-projects"
status: "source-audited"
version: "2.55.0"
---

# `git remote`

Este caso usa `git remote` para crear y administrar nombres para repositorios remotos.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Remotos y refspecs

Un remoto asigna un nombre, como `origin`, a una o más URL y a reglas de descarga. La URL elige transporte y ubicación. Un refspec asigna una referencia de origen a una referencia de destino.

```bash
git remote add origin https://example.com/proyecto.git
git remote -v
git config --get-all remote.origin.fetch
```

La segunda orden muestra las URL de fetch y push. La tercera muestra el refspec de descarga. Comprueba estos valores antes de ejecutar fetch, pull o push.

## Cómo funciona

La transferencia copia objetos y actualiza referencias. Descargar, integrar y publicar son operaciones separadas aunque algunos comandos las encadenen.

Distingue las referencias de seguimiento remoto de la rama actual. Descargar una referencia no integra por sí mismo sus commits.

## Ejemplo mínimo

```bash
git remote add origin https://example.com/equipo/biblioteca.git
git remote -v
```

La invocación `git remote add origin https://example.com/equipo/biblioteca.git` ejecuta esta operación: crear y administrar nombres para repositorios remotos. Después, las referencias locales y remotas permiten separar descarga, integración y publicación.

## Sintaxis y formas de invocación

```text
git remote [-v | --verbose]
git remote add [-t <branch>] [-m <master>] [-f] [--[no-]tags] [--mirror=(fetch|push)] <name> <URL>
git remote rename [--[no-]progress] <old> <new>
git remote remove <name>
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git remote [-v | --verbose]
   or: git remote add [-t <branch>] [-m <master>] [-f] [--tags | --no-tags] [--mirror=<fetch|push>] <name> <url>
   or: git remote rename [--[no-]progress] <old> <new>
   or: git remote remove <name>
   or: git remote set-head <name> (-a | --auto | -d | --delete | <branch>)
   or: git remote [-v | --verbose] show [-n] <name>
   or: git remote prune [-n | --dry-run] <name>
   or: git remote [-v | --verbose] update [-p | --prune] [(<group> | <remote>)...]
   or: git remote set-branches [--add] <name> <branch>...
   or: git remote get-url [--push] [--all] <name>
   or: git remote set-url [--push] <name> <newurl> [<oldurl>]
   or: git remote set-url --add <name> <newurl>
   or: git remote set-url --delete <name> <url>
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git remote -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `-v` y `--verbose`

Aumenta el detalle enviado a la salida.

#### Ejemplo con `--verbose`

```bash
git remote --verbose add origin https://example.com/equipo/biblioteca.git
git branch -vv
```

 La salida permite comparar la rama local con su upstream.

### `-t`

Activa t durante crear y administrar nombres para repositorios remotos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git remote -t add origin https://example.com/equipo/biblioteca.git
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-m`

Activa m durante crear y administrar nombres para repositorios remotos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git remote -m add origin https://example.com/equipo/biblioteca.git
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-f`

Activa f durante crear y administrar nombres para repositorios remotos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git remote -f add origin https://example.com/equipo/biblioteca.git
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--tags`

Incluye o selecciona etiquetas según la operación.

```bash
git remote --tags add origin https://example.com/equipo/biblioteca.git
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--mirror`

Activa espejo durante crear y administrar nombres para repositorios remotos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git remote --mirror add origin https://example.com/equipo/biblioteca.git
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--progress`

Muestra progreso aunque la salida no sea un terminal.

```bash
git remote --progress add origin https://example.com/equipo/biblioteca.git
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-tags`

Desactiva el comportamiento `tags` para esta invocación.

```bash
git remote --no-tags add origin https://example.com/equipo/biblioteca.git
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-a`

Activa a durante crear y administrar nombres para repositorios remotos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git remote -a add origin https://example.com/equipo/biblioteca.git
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--auto`

Activa auto durante crear y administrar nombres para repositorios remotos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git remote --auto add origin https://example.com/equipo/biblioteca.git
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-d`

Activa d durante crear y administrar nombres para repositorios remotos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git remote -d add origin https://example.com/equipo/biblioteca.git
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--delete`

Elimina el elemento seleccionado.

```bash
git remote --delete add origin https://example.com/equipo/biblioteca.git
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-n`

Activa n durante crear y administrar nombres para repositorios remotos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git remote -n add origin https://example.com/equipo/biblioteca.git
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--dry-run`

Calcula el alcance y muestra lo que ocurriría sin aplicar el cambio.

```bash
git remote --dry-run add origin https://example.com/equipo/biblioteca.git
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-p`

Activa p durante crear y administrar nombres para repositorios remotos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git remote -p add origin https://example.com/equipo/biblioteca.git
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--prune`

Retira entradas que ya no cumplen la condición documentada.

```bash
git remote --prune add origin https://example.com/equipo/biblioteca.git
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--add`

Permite crear o escribir el elemento seleccionado.

```bash
git remote --add add origin https://example.com/equipo/biblioteca.git
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--push`

Activa push durante crear y administrar nombres para repositorios remotos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git remote --push add origin https://example.com/equipo/biblioteca.git
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--all`

Amplía la selección a todos los elementos del alcance definido.

```bash
git remote --all add origin https://example.com/equipo/biblioteca.git
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Páginas relacionadas

- [`git request-pull`](../sharing-and-updating-projects/request-pull.md)
- [`git push`](../sharing-and-updating-projects/push.md)
- [`git submodule`](../sharing-and-updating-projects/submodule.md)

## Fuente

- [git-remote - Manage set of tracked repositories](https://git-scm.com/docs/git-remote)
