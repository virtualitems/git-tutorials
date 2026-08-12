---
title: "git cvsserver"
source: "https://git-scm.com/docs/git-cvsserver"
section: "external-systems"
status: "source-audited"
version: "2.55.0"
---

# `git cvsserver`

Este caso usa `git cvsserver` para permitir que clientes CVS accedan a un repositorio Git.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

La integración traduce identidades, ramas y cambios entre dos modelos de control de versiones. Una migración se valida comparando historial, contenido y referencias en el destino.

Define una regla para autores, ramas, etiquetas y finales de línea antes de importar. Valida cada regla con un conjunto que contenga ese caso.

## Ejemplo mínimo

```bash
git config cvsserver.enabled true
CVS_SERVER='git cvsserver' cvs -d :ext:servidor/repo co modulo
```

La invocación `git cvsserver` ejecuta esta operación: permitir que clientes CVS accedan a un repositorio Git. Después, el destino conserva el contenido, autores, ramas y etiquetas que admita la conversión.

## Sintaxis y formas de invocación

```text
export CVS_SERVER="git cvsserver"
cvs -d :ext:user@server/path/repo.git co <HEAD_name>
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git cvsserver -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `-d`

Activa d durante permitir que clientes CVS accedan a un repositorio Git. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git cvsserver -d
printf 'exit=%s\n' "$?"
```

## Páginas relacionadas

- [`git fast-export`](../external-systems/fast-export.md)
- [`git cvsimport`](../external-systems/cvsimport.md)
- [`git fast-import`](../external-systems/fast-import.md)

## Fuente

- [git-cvsserver - A CVS server emulator for Git](https://git-scm.com/docs/git-cvsserver)
