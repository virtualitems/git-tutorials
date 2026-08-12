---
title: "scalar"
source: "https://git-scm.com/docs/scalar"
section: "administration"
status: "option-expanded"
---

# `scalar`

Este caso usa `scalar` para administrar repositorios con funciones orientadas a conjuntos de archivos extensos. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Responsabilidad y efecto

scalar comprueba integridad, administra reflogs y reorganiza o elimina datos del almacén. Recibe como entrada los objetos, referencias o archivos de almacenamiento que se van a inspeccionar. La operación consiste en administrar repositorios con funciones orientadas a conjuntos de archivos extensos.

Puede persistir el estado implicado por esta operación: administrar repositorios con funciones orientadas a conjuntos de archivos extensos. Las opciones pueden limitar o ampliar ese efecto.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). La posición de opciones, revisiones y rutas sigue las [convenciones de la interfaz de Git](../guides/gitcli.md#convenciones-de-la-cli). Los nombres como `HEAD`, `main`, `HEAD~2` y `A..B` se explican en [revisiones y rangos](../guides/gitrevisions.md#revisiones-y-rangos). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

Git almacena objetos sueltos, packs, referencias y reflogs. Las tareas de administración reorganizan o eliminan datos según su alcanzabilidad y antigüedad.

Relaciona cada archivo con su alcanzabilidad y retención. La compactación cambia la representación; la poda puede cambiar qué datos se pueden recuperar.

## Ejemplo mínimo

```bash
scalar clone https://example.com/equipo/biblioteca.git biblioteca
scalar list
```

La invocación `scalar clone https://example.com/equipo/biblioteca.git biblioteca` ejecuta esta operación: administrar repositorios con funciones orientadas a conjuntos de archivos extensos. Después, los modos de simulación y las consultas de tamaño muestran el efecto antes y después. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
scalar clone [--single-branch] [--branch <main-branch>] [--full-clone]
	[--[no-]src] [--[no-]tags] [--[no-]maintenance] <url> [<enlistment>]
scalar list
scalar register [--[no-]maintenance] [<enlistment>]
```

### Uso verificado con `git version 2.51.1`

```text
scalar [-C <directory>] [-c <key>=<value>] <command> [<options>]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `scalar -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

administrar repositorios con funciones orientadas a conjuntos de archivos extensos. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### Alcance explícito

Aplicar scalar a una referencia, rango o ruta identificada. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Resuelve cada argumento antes de ejecutar y usa `--` para rutas.

### Validación

Comprobar el resultado de scalar con una orden de lectura independiente. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. No uses la misma salida como única prueba del cambio.

## Opciones

Cada apartado usa una opción en una invocación concreta. Las opciones equivalentes comparten la explicación, pero cada alias tiene su propio ejemplo. Ejecuta una opción por vez antes de combinarlas.

### `--single-branch`

Selecciona o modifica referencias dentro del alcance de la orden.

La opción limita o amplía el conjunto sobre el que se ejecuta administrar repositorios con funciones orientadas a conjuntos de archivos extensos. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
scalar --single-branch clone https://example.com/equipo/biblioteca.git biblioteca
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `scalar` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--branch`

Selecciona o modifica referencias dentro del alcance de la orden.

La opción limita o amplía el conjunto sobre el que se ejecuta administrar repositorios con funciones orientadas a conjuntos de archivos extensos. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
scalar --branch clone https://example.com/equipo/biblioteca.git biblioteca
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `scalar` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--full-clone`

Activa full clone durante administrar repositorios con funciones orientadas a conjuntos de archivos extensos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `scalar`, full clone modifica la forma en que se ejecuta administrar repositorios con funciones orientadas a conjuntos de archivos extensos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
scalar --full-clone clone https://example.com/equipo/biblioteca.git biblioteca
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `scalar` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--src`

Activa src durante administrar repositorios con funciones orientadas a conjuntos de archivos extensos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `scalar`, src modifica la forma en que se ejecuta administrar repositorios con funciones orientadas a conjuntos de archivos extensos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
scalar --src clone https://example.com/equipo/biblioteca.git biblioteca
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `scalar` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--tags`

Incluye o selecciona etiquetas según la operación.

La opción limita o amplía el conjunto sobre el que se ejecuta administrar repositorios con funciones orientadas a conjuntos de archivos extensos. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
scalar --tags clone https://example.com/equipo/biblioteca.git biblioteca
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `scalar` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--maintenance`

Activa maintenance durante administrar repositorios con funciones orientadas a conjuntos de archivos extensos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `scalar`, maintenance modifica la forma en que se ejecuta administrar repositorios con funciones orientadas a conjuntos de archivos extensos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
scalar --maintenance clone https://example.com/equipo/biblioteca.git biblioteca
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `scalar` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-C`

Ejecuta Git como si se hubiera iniciado en el directorio indicado.

En `scalar`, C modifica la forma en que se ejecuta administrar repositorios con funciones orientadas a conjuntos de archivos extensos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
scalar -C clone https://example.com/equipo/biblioteca.git biblioteca
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `scalar` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-c`

Aplica una clave de configuración solo a esta invocación.

En `scalar`, c modifica la forma en que se ejecuta administrar repositorios con funciones orientadas a conjuntos de archivos extensos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
scalar -c clone https://example.com/equipo/biblioteca.git biblioteca
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `scalar` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Errores y diagnóstico

### Un objeto aparece como inalcanzable

Comprueba esta causa: Ninguna referencia o reflog lo conserva. Determina si debe recuperarse antes de podar.

### El tamaño no disminuye

Comprueba esta causa: Los objetos siguen alcanzables o aún están protegidos por reflogs. Inspecciona alcanzabilidad y vencimientos.

### La operación se interrumpe

Comprueba esta causa: Otro proceso mantiene un lock. Comprueba procesos activos antes de retirar un lock obsoleto.

## Automatización y recuperación

Persistencia: Puede persistir el estado implicado por esta operación: administrar repositorios con funciones orientadas a conjuntos de archivos extensos. Las opciones pueden limitar o ampliar ese efecto. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

Haz la prueba en una copia. Ejecuta primero el modo de inspección o simulación disponible y registra referencias, reflogs y tamaño antes de modificar datos.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git replace`](../administration/replace.md)
- [`git repack`](../administration/repack.md)

## Fuente

- [scalar - A tool for managing large Git repositories](https://git-scm.com/docs/scalar)
