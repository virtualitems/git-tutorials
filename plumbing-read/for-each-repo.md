---
title: "git for-each-repo"
source: "https://git-scm.com/docs/git-for-each-repo"
section: "plumbing-read"
---

# `git for-each-repo`

## Ejemplo de partida

```bash
git config --global --add repos.proyectos ~/codigo/biblioteca
git for-each-repo --config=repos.proyectos status --short
```

Este caso usa `git for-each-repo` para ejecutar un comando Git en repositorios enumerados por configuración. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: objetos, referencias, árboles o entradas del índice que debe leer la consulta.
- Operación: ejecutar un comando Git en repositorios enumerados por configuración.
- Comprobación: la salida estructurada puede compararse o pasar a otro proceso sin alterar el repositorio.

## Modelo mental

La salida expone datos internos para inspección o scripts. Los formatos explícitos y los separadores NUL evitan ambigüedad cuando los nombres contienen espacios o saltos de línea.

Fija el formato de salida que consumirá el siguiente proceso. Usa separadores NUL cuando una ruta pueda contener caracteres que también actúan como separadores de texto.

## Forma de referencia

```text
git for-each-repo --config=<config> [--] <arguments>
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. El separador `--` termina las opciones y permite tratar lo que sigue como rutas.

## Práctica

Prueba con nombres que contengan espacios. Si el comando ofrece `-z`, procesa la salida por bytes y conserva los separadores NUL.

## Páginas relacionadas

- [`git format-rev`](../plumbing-read/format-rev.md)
- [`git for-each-ref`](../plumbing-read/for-each-ref.md)
- [`git get-tar-commit-id`](../plumbing-read/get-tar-commit-id.md)

## Fuente

- [git-for-each-repo - Run a Git command on a list of repositories](https://git-scm.com/docs/git-for-each-repo)
