---
title: "Referencia de Git"
source: "https://git-scm.com/docs"
section: "overview"
status: "reviewed"
version: "2.55.0"
---

# Referencia de Git

El [README](../README.md#menú-de-secciones) es el índice único del proyecto. Organiza cada guía por la responsabilidad principal del comando o concepto y enlaza una sola ubicación canónica.

## Localizar un comando

`git help --all` enumera los comandos instalados. Usa `--no-external-commands` para excluir ejecutables `git-*` externos y `--no-aliases` para excluir alias de configuración.

```bash
git help --all
git help --all --no-external-commands --no-aliases
```

Busca después el nombre en el [README](../README.md). Si una función pertenece a varias categorías, el índice la coloca donde se explica su efecto principal y las demás páginas la enlazan.

## Abrir un manual

```bash
git help add
git help revisions
git help gitignore
```

`git help add` abre el manual de un comando. `revisions` y `gitignore` son guías conceptuales: se consultan mediante `git help`, pero no se ejecutan como `git revisions` o `git gitignore`.

La opción `--help-all` de un comando incluye opciones de plomería u obsoletas que pueden faltar en la ayuda normal.

```bash
git fetch --help-all
```

## Rutas de aprendizaje

- Para crear un repositorio y registrar cambios: [`git init`](../getting-and-creating-projects/init.md), [`git add`](../basic-snapshotting/add.md) y [`git commit`](../basic-snapshotting/commit.md).
- Para compartir historia: [`git remote`](../sharing-and-updating-projects/remote.md), [`git fetch`](../sharing-and-updating-projects/fetch.md), [`git pull`](../sharing-and-updating-projects/pull.md) y [`git push`](../sharing-and-updating-projects/push.md).
- Para interpretar argumentos comunes: [convenciones de la CLI](../guides/gitcli.md), [revisiones](../guides/gitrevisions.md) y [pathspecs](../guides/gitcli.md#pathspecs-y-expansión-del-shell).
- Para opciones reutilizadas por varios comandos: [opciones de diff](../plumbing-read/diff-pairs.md#opciones) y [recorrido de revisiones](../plumbing-read/rev-list.md#opciones).

## Versión documental

Las guías toman Git 2.55.0 como referencia. Comprueba la instalación antes de automatizar una opción:

```bash
git --version
git <comando> --help-all
```

Una versión anterior puede no reconocer una opción y una versión posterior puede añadir otras. Contrasta los cambios con la carpeta `Documentation` de la versión oficial que quieras adoptar.

## Fuente

- [Documentación oficial de Git](https://git-scm.com/docs)
