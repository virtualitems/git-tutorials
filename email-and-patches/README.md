# Parches por correo

Esta sección genera, transporta o aplica series de parches conservando autoría y orden. Lee commits, archivos mbox, cabeceras y configuración de transporte y puede escribir parches, mensajes o commits aplicados.

## Modelo de la sección

| Elemento | Relación con la función | Comprobación |
| --- | --- | --- |
| Entrada | commits, archivos mbox, cabeceras y configuración de transporte. | Registra los argumentos y resuelve revisiones antes de ejecutar. |
| Efecto principal | genera, transporta o aplica series de parches conservando autoría y orden. | Comprueba el resultado con una orden de lectura. |
| Persistencia | parches, mensajes o commits aplicados | Compara el estado antes y después. |
| Resultado | La orden comunica datos por stdout y diagnósticos por stderr. | Captura también el código de terminación. |
| Fuente de verdad | El repositorio y la configuración efectiva determinan el resultado. | Usa el orden de la serie, `git diff --check`, los encabezados y el log resultante. |

## Preparación

Genera una serie en un directorio de prueba. Revisa destinatarios y encabezados sin enviar mensajes.

## Ruta de trabajo

1. Abre la guía de la función que produce el estado de entrada.
2. Ejecuta el ejemplo en el laboratorio de esa guía.
3. Comprueba el resultado con una operación de lectura.
4. Prueba un caso sin coincidencias o con una entrada inválida.
5. Registra la versión con `git --version` cuando el resultado forme parte de una automatización.

## Inventario

| Página | Responsabilidad |
| --- | --- |
| [`git am`](am.md) | convertir una serie de parches de correo en commits |
| [`git format-patch`](format-patch.md) | representar commits como archivos de parche para correo |
| [`git imap-send`](imap-send.md) | enviar una colección de parches a una carpeta IMAP |
| [`git send-email`](send-email.md) | enviar parches por correo electrónico |

## Diagnóstico compartido

| Señal | Causa que debes comprobar | Acción |
| --- | --- | --- |
| La numeración no coincide | El rango o la revisión de la serie cambió | Regenera la serie completa con el mismo punto base. |
| La aplicación se detiene | El parche no coincide o falta información de autor | Corrige el parche o resuelve y continúa la sesión. |
| El transporte rechaza el mensaje | La configuración SMTP o IMAP no autoriza la operación | Prueba autenticación fuera del contenido del mensaje y evita secretos en argumentos. |

## Convenciones

- `HEAD` identifica el commit actual o la referencia simbólica que lo selecciona.
- Una revisión selecciona objetos; un pathspec selecciona rutas.
- `--` separa opciones y revisiones de rutas cuando la sintaxis lo admite.
- stdout transporta resultados; stderr transporta diagnósticos.
- Un código distinto de cero puede representar una respuesta negativa en comandos de consulta.
