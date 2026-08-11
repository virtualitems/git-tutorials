# Servidor y transporte

Esta sección expone repositorios o participa en negociación y transferencia de objetos. Lee solicitudes, capacidades, referencias y objetos alcanzables y puede escribir objetos y referencias solo cuando el servicio admite recepción.

## Modelo de la sección

| Elemento | Relación con la función | Comprobación |
| --- | --- | --- |
| Entrada | solicitudes, capacidades, referencias y objetos alcanzables. | Registra los argumentos y resuelve revisiones antes de ejecutar. |
| Efecto principal | expone repositorios o participa en negociación y transferencia de objetos. | Comprueba el resultado con una orden de lectura. |
| Persistencia | objetos y referencias solo cuando el servicio admite recepción | Compara el estado antes y después. |
| Resultado | La orden comunica datos por stdout y diagnósticos por stderr. | Captura también el código de terminación. |
| Fuente de verdad | El repositorio y la configuración efectiva determinan el resultado. | Usa referencias anunciadas, logs del servicio, permisos y una transferencia desde un cliente de prueba. |

## Preparación

Vincula el servicio a localhost y usa un repositorio bare sin datos de producción.

## Ruta de trabajo

1. Abre la guía de la función que produce el estado de entrada.
2. Ejecuta el ejemplo en el laboratorio de esa guía.
3. Comprueba el resultado con una operación de lectura.
4. Prueba un caso sin coincidencias o con una entrada inválida.
5. Registra la versión con `git --version` cuando el resultado forme parte de una automatización.

## Inventario

| Página | Responsabilidad |
| --- | --- |
| [`git daemon`](daemon.md) | servir repositorios mediante el protocolo git |
| [`git fetch-pack`](fetch-pack.md) | solicitar a otro repositorio los objetos que faltan |
| [`git http-backend`](http-backend.md) | atender operaciones Git del lado servidor sobre HTTP |
| [`git http-fetch`](http-fetch.md) | descargar objetos mediante el transporte HTTP heredado |
| [`git http-push`](http-push.md) | enviar objetos mediante HTTP con WebDAV |
| [`git receive-pack`](receive-pack.md) | recibir objetos y solicitudes de actualización de referencias |
| [`git send-pack`](send-pack.md) | enviar objetos y actualizaciones de referencias al receptor |
| [`git shell`](shell.md) | restringir una cuenta SSH a operaciones de Git |
| [`git update-server-info`](update-server-info.md) | generar archivos auxiliares para clientes HTTP sin negociación |
| [`git upload-archive`](upload-archive.md) | responder a una solicitud remota de git archive |
| [`git upload-pack`](upload-pack.md) | negociar y enviar objetos a un cliente de fetch |

## Diagnóstico compartido

| Señal | Causa que debes comprobar | Acción |
| --- | --- | --- |
| El repositorio no se anuncia | La ruta, exportación o política no lo permite | Comprueba la raíz del servicio y los marcadores de exportación. |
| La negociación se corta | Cliente y servidor no acuerdan capacidad o protocolo | Registra trazas sin incluir credenciales y compara versiones. |
| La recepción se rechaza | Los permisos o hooks bloquean la referencia | Revisa la política del repositorio y el mensaje del hook. |

## Convenciones

- `HEAD` identifica el commit actual o la referencia simbólica que lo selecciona.
- Una revisión selecciona objetos; un pathspec selecciona rutas.
- `--` separa opciones y revisiones de rutas cuando la sintaxis lo admite.
- stdout transporta resultados; stderr transporta diagnósticos.
- Un código distinto de cero puede representar una respuesta negativa en comandos de consulta.
