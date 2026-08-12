---
title: "git fsck"
source: "https://git-scm.com/docs/git-fsck"
section: "administration"
status: "option-expanded"
---

# `git fsck`

Este caso usa `git fsck` para comprobar conectividad y validez de los objetos. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Responsabilidad y efecto

git fsck comprueba integridad, administra reflogs y reorganiza o elimina datos del almacén. Recibe como entrada los objetos, referencias o archivos de almacenamiento que se van a inspeccionar. La operación consiste en comprobar conectividad y validez de los objetos.

No modifica el repositorio en su forma de consulta. Puede iniciar un visor o escribir un archivo si se solicita de forma explícita.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). La posición de opciones, revisiones y rutas sigue las [convenciones de la interfaz de Git](../guides/gitcli.md#convenciones-de-la-cli). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

Git almacena objetos sueltos, packs, referencias y reflogs. Las tareas de administración reorganizan o eliminan datos según su alcanzabilidad y antigüedad.

Relaciona cada archivo con su alcanzabilidad y retención. La compactación cambia la representación; la poda puede cambiar qué datos se pueden recuperar.

## Ejemplo mínimo

```bash
git fsck --full
```

La invocación `git fsck --full` ejecuta esta operación: comprobar conectividad y validez de los objetos. Después, los modos de simulación y las consultas de tamaño muestran el efecto antes y después. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
git fsck [--tags] [--root] [--unreachable] [--cache] [--no-reflogs]
	 [--[no-]full] [--strict] [--verbose] [--lost-found]
	 [--[no-]dangling] [--[no-]progress] [--connectivity-only]
	 [--[no-]name-objects] [--[no-]references] [<object>…]
```

### Uso verificado con `git version 2.51.1`

```text
git fsck [--tags] [--root] [--unreachable] [--cache] [--no-reflogs]
                [--[no-]full] [--strict] [--verbose] [--lost-found]
                [--[no-]dangling] [--[no-]progress] [--connectivity-only]
                [--[no-]name-objects] [--[no-]references] [<object>...]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git fsck -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

comprobar conectividad y validez de los objetos. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### Alcance explícito

Aplicar git fsck a una referencia, rango o ruta identificada. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Resuelve cada argumento antes de ejecutar y usa `--` para rutas.

### Validación

Comprobar el resultado de git fsck con una orden de lectura independiente. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. No uses la misma salida como única prueba del cambio.

## Opciones

Cada apartado usa una opción en una invocación concreta. Las opciones equivalentes comparten la explicación, pero cada alias tiene su propio ejemplo. Ejecuta una opción por vez antes de combinarlas.

### `--tags`

Incluye o selecciona etiquetas según la operación.

La opción limita o amplía el conjunto sobre el que se ejecuta comprobar conectividad y validez de los objetos. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git fsck --tags --full
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fsck` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--root`

Activa root durante comprobar conectividad y validez de los objetos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `report root nodes`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git fsck`, root modifica la forma en que se ejecuta comprobar conectividad y validez de los objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git fsck --root --full
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fsck` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--unreachable`

Incluye unreachable en la salida o cambia cómo `git fsck` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `show unreachable objects`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git fsck --unreachable --full
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fsck` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--cache`

Activa cache durante comprobar conectividad y validez de los objetos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `make index objects head nodes`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git fsck`, cache modifica la forma en que se ejecuta comprobar conectividad y validez de los objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git fsck --cache --full
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fsck` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-reflogs`

Desactiva el comportamiento `reflogs` para esta invocación.

En `git fsck`, desactivar reflogs modifica la forma en que se ejecuta comprobar conectividad y validez de los objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git fsck --no-reflogs --full
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fsck` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--full`

Activa full durante comprobar conectividad y validez de los objetos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `also consider packs and alternate objects`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git fsck`, full modifica la forma en que se ejecuta comprobar conectividad y validez de los objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git fsck --full
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fsck` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--strict`

Activa strict durante comprobar conectividad y validez de los objetos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `enable more strict checking`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción añade, retira o consulta una comprobación previa. Ejecuta primero la forma que no escribe cuando exista y conserva el código de terminación como parte del resultado.

```bash
git fsck --strict --full
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fsck` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--verbose` y `-v`

Aumenta el detalle enviado a la salida.  La misma línea de ayuda también acepta `-v`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

#### Ejemplo con `--verbose`

```bash
git fsck --verbose --full
git count-objects -vH
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git fsck` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado.

#### Ejemplo con `-v`

```bash
git fsck -v --full
git count-objects -vH
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git fsck` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--lost-found`

Escribe o registra lost found como parte de comprobar conectividad y validez de los objetos. En Git 2.51.1, la ayuda corta expresa el contrato como `write dangling objects in .git/lost-found`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git fsck`, lost found modifica la forma en que se ejecuta comprobar conectividad y validez de los objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git fsck --lost-found --full
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fsck` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--dangling`

Incluye dangling en la salida o cambia cómo `git fsck` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `show dangling objects`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git fsck --dangling --full
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fsck` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--progress`

Muestra progreso aunque la salida no sea un terminal.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git fsck --progress --full
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fsck` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--connectivity-only`

Limita comprobar conectividad y validez de los objetos al alcance identificado por connectivity only. En Git 2.51.1, la ayuda corta expresa el contrato como `check only connectivity`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción añade, retira o consulta una comprobación previa. Ejecuta primero la forma que no escribe cuando exista y conserva el código de terminación como parte del resultado.

```bash
git fsck --connectivity-only --full
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fsck` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--name-objects`

Selecciona la representación o tratamiento de identificadores de objeto.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git fsck --name-objects --full
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fsck` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--references`

Comprueba references antes de aceptar el resultado de `git fsck`. En Git 2.51.1, la ayuda corta expresa el contrato como `check reference database consistency`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción añade, retira o consulta una comprobación previa. Ejecuta primero la forma que no escribe cuando exista y conserva el código de terminación como parte del resultado.

```bash
git fsck --references --full
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fsck` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--reflogs`

Activa reflogs durante comprobar conectividad y validez de los objetos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `make reflogs head nodes (default)`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git fsck`, reflogs modifica la forma en que se ejecuta comprobar conectividad y validez de los objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git fsck --reflogs --full
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fsck` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-tags`

Desactiva para esta invocación el comportamiento que habilita `--tags`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta comprobar conectividad y validez de los objetos. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git fsck --no-tags --full
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fsck` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-root`

Desactiva para esta invocación el comportamiento que habilita `--root`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git fsck`, desactivar root modifica la forma en que se ejecuta comprobar conectividad y validez de los objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git fsck --no-root --full
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fsck` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-unreachable`

Desactiva para esta invocación el comportamiento que habilita `--unreachable`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git fsck --no-unreachable --full
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fsck` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-cache`

Desactiva para esta invocación el comportamiento que habilita `--cache`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git fsck`, desactivar cache modifica la forma en que se ejecuta comprobar conectividad y validez de los objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git fsck --no-cache --full
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fsck` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-full`

Desactiva para esta invocación el comportamiento que habilita `--full`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git fsck`, desactivar full modifica la forma en que se ejecuta comprobar conectividad y validez de los objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git fsck --no-full
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fsck` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-strict`

Desactiva para esta invocación el comportamiento que habilita `--strict`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción añade, retira o consulta una comprobación previa. Ejecuta primero la forma que no escribe cuando exista y conserva el código de terminación como parte del resultado.

```bash
git fsck --no-strict --full
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fsck` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-verbose`

Desactiva para esta invocación el comportamiento que habilita `--verbose`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git fsck --no-verbose --full
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fsck` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-lost-found`

Desactiva para esta invocación el comportamiento que habilita `--lost-found`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git fsck`, desactivar lost found modifica la forma en que se ejecuta comprobar conectividad y validez de los objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git fsck --no-lost-found --full
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fsck` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-dangling`

Desactiva para esta invocación el comportamiento que habilita `--dangling`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git fsck --no-dangling --full
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fsck` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-progress`

Desactiva para esta invocación el comportamiento que habilita `--progress`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git fsck --no-progress --full
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fsck` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-connectivity-only`

Desactiva para esta invocación el comportamiento que habilita `--connectivity-only`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción añade, retira o consulta una comprobación previa. Ejecuta primero la forma que no escribe cuando exista y conserva el código de terminación como parte del resultado.

```bash
git fsck --no-connectivity-only --full
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fsck` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-name-objects`

Desactiva para esta invocación el comportamiento que habilita `--name-objects`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git fsck --no-name-objects --full
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fsck` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-references`

Desactiva para esta invocación el comportamiento que habilita `--references`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción añade, retira o consulta una comprobación previa. Ejecuta primero la forma que no escribe cuando exista y conserva el código de terminación como parte del resultado.

```bash
git fsck --no-references --full
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fsck` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Errores y diagnóstico

### Un objeto aparece como inalcanzable

Comprueba esta causa: Ninguna referencia o reflog lo conserva. Determina si debe recuperarse antes de podar.

### El tamaño no disminuye

Comprueba esta causa: Los objetos siguen alcanzables o aún están protegidos por reflogs. Inspecciona alcanzabilidad y vencimientos.

### La operación se interrumpe

Comprueba esta causa: Otro proceso mantiene un lock. Comprueba procesos activos antes de retirar un lock obsoleto.

## Automatización y recuperación

Persistencia: No modifica el repositorio en su forma de consulta. Puede iniciar un visor o escribir un archivo si se solicita de forma explícita. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

Haz la prueba en una copia. Ejecuta primero el modo de inspección o simulación disponible y registra referencias, reflogs y tamaño antes de modificar datos.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git gc`](../administration/gc.md)
- [`git filter-branch`](../administration/filter-branch.md)
- [`git maintenance`](../administration/maintenance.md)

## Fuente

- [git-fsck - Verifies the connectivity and validity of the objects in the database](https://git-scm.com/docs/git-fsck)
