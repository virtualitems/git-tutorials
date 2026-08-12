---
title: "git instaweb"
source: "https://git-scm.com/docs/git-instaweb"
section: "graphical-tools"
status: "source-audited"
version: "2.55.0"
---

# `git instaweb`

Este caso usa `git instaweb` para iniciar una instancia temporal de gitweb.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

La interfaz presenta operaciones que también existen en el modelo de objetos, índice, referencias y commits. La vista cambia; el repositorio conserva el mismo estado.

Relaciona cada acción de la interfaz con índice, commit o referencia. Usa una consulta de Git para comprobar el cambio de estado.

## Ejemplo mínimo

```bash
git instaweb --start
git instaweb --stop
```

La invocación `git instaweb --start` ejecuta esta operación: iniciar una instancia temporal de gitweb. Después, los comandos de consulta confirman el mismo estado que presenta la interfaz.

## Sintaxis y formas de invocación

```text
git instaweb [--local] [--httpd=<httpd>] [--port=<port>]
               [--browser=<browser>]
git instaweb [--start] [--stop] [--restart]
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git instaweb [options] (--start | --stop | --restart)
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git instaweb -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `--local` y `-l`

Opera sobre la configuración del repositorio.

#### Ejemplo con `--local`

```bash
git instaweb --local --start
printf 'exit=%s\n' "$?"
```

### `--httpd` y `-d`

Activa httpd durante iniciar una instancia temporal de gitweb. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `the command to launch`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--httpd`

```bash
git instaweb --httpd --start
printf 'exit=%s\n' "$?"
```

### `--port` y `-p`

Activa port durante iniciar una instancia temporal de gitweb. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `the port to bind to`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--port`

```bash
git instaweb --port --start
printf 'exit=%s\n' "$?"
```

### `--browser` y `-b`

Activa browser durante iniciar una instancia temporal de gitweb. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `the browser to launch`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--browser`

```bash
git instaweb --browser --start
printf 'exit=%s\n' "$?"
```

### `--start`

Activa start durante iniciar una instancia temporal de gitweb. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `start the web server`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git instaweb --start
printf 'exit=%s\n' "$?"
```

### `--stop`

Activa stop durante iniciar una instancia temporal de gitweb. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `stop the web server`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git instaweb --stop --start
printf 'exit=%s\n' "$?"
```

### `--restart`

Activa restart durante iniciar una instancia temporal de gitweb. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `restart the web server`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git instaweb --restart --start
printf 'exit=%s\n' "$?"
```

### `-m` y `--module-path`

Limita iniciar una instancia temporal de gitweb al alcance identificado por module ruta. En Git 2.51.1, la ayuda corta expresa el contrato como `the module path (only needed for apache2)`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--module-path`

```bash
git instaweb --module-path --start
printf 'exit=%s\n' "$?"
```

## Páginas relacionadas

- [`gitk`](../graphical-tools/gitk.md)
- [`git gui`](../graphical-tools/gui.md)
- [`gitweb`](../graphical-tools/gitweb.md)

## Fuente

- [git-instaweb - Instantly browse your working repository in gitweb](https://git-scm.com/docs/git-instaweb)
