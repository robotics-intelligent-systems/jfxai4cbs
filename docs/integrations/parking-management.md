# Gestión de estacionamientos: catálogo e integración propuesta

Revisión: 13 de octubre de 2026. Estado: evaluación documental; ningún conector implementado ni dependencia instalada.

## Procedencia y alcance de la revisión

Se interpretó «robotics» como [robotics-intelligent-systems](https://github.com/robotics-intelligent-systems), organización propietaria de JFXAI4CBS. Se consultaron búsquedas de repositorios y forks públicos accesibles para esta organización y [DK2035](https://github.com/DK2035), incluyendo parking, park, garage y estacionamiento. El inventario paginado de forks de robotics devolvió 972 entradas; no se identificó un sistema de estacionamientos por los nombres y búsquedas revisados. En DK2035 la búsqueda de forks devolvió solamente [esp32-homekit-remote](https://github.com/DK2035/esp32-homekit-remote), un control de aire acondicionado, excluido por su función.

Estas consultas describen lo visible mediante la conexión y el índice de GitHub; no certifican ausencia en repositorios privados, no indexados o con nombres distintos.

La fuente pertinente encontrada fue [jfoxpms](https://github.com/robotics-intelligent-systems/jfoxpms/blob/main/README.md), SHA de README `b6aa2118e9dc45a67fc844198f30f8848b3901d8`. Es un compendio propio, no un fork ni un gestor ejecutable. Se localizaron los proyectos externos que coinciden con sus nombres y descripciones. No se atribuyen estos repositorios a forks de DK2035 o robotics.

## Candidatos categorizados

| Proyecto | Categoría | Evidencia de licencia | Decisión y límite |
|---|---|---|---|
| [Parker — oxedom/parker](https://github.com/oxedom/parker) | Visión / ocupación de plazas | [MIT](https://github.com/oxedom/parker/blob/main/LICENSE.txt) | Prioridad para experimento de ocupación. Procesamiento en navegador con TensorFlow.js y YOLOv7; no equivale a gestor de reservas, tarifas o barreras. Revisar pesos y dependencias. |
| [TheParker — ketanchoyal/theParker](https://github.com/ketanchoyal/theParker) | Reservas / aparcamiento compartido móvil | [MIT](https://github.com/ketanchoyal/theParker/blob/master/LICENSE) | Referencia funcional y candidato opcional. Android en Java; usa Firebase y Google Maps. Su pago es estático, sin pasarela implementada según README. Evaluar actualización o sustitución de servicios externos. La licencia Android no certifica las variantes iOS y Flutter. |
| [Ezy-Parking — prathimacode-hub/Ezy-Parking](https://github.com/prathimacode-hub/Ezy-Parking) | Gestión web / reservas / IoT propuesto | [GPL v3](https://github.com/prathimacode-hub/Ezy-Parking/blob/main/LICENSE) | Sugerencia de integración mediante servicio separado. El README describe un alcance amplio; validar en código y pruebas cada función antes de asumirla disponible. GitHub lo identifica como GPL-3.0; precisar only/or-later para la versión elegida. |
| [Parkingslot — visualbuffer/parkingslot](https://github.com/visualbuffer/parkingslot) | Investigación / detección de ocupación | No se encontró licencia explícita en la raíz; metadatos de GitHub sin licencia | Referencia pendiente; no aprobar como dependencia de código abierto hasta aclarar permisos. Usa modelos YOLO / Mask R-CNN y clasificación de ocupación. Revisar también pesos y datos. |

Las fechas del último push observadas son 2026-06-28 para Parker, 2020-05-22 para TheParker, 2023-04-04 para Ezy-Parking y 2020-08-11 para Parkingslot. Son señales de revisión, no certificación de mantenimiento ni fecha de una versión estable.

## Referencias sin identificación suficiente

El compendio también menciona «Parking Management System Project In Java», «Zernike Facilities / P7» y «Smart Park with YOLO-V3». Quedan conservadas como referencias pendientes: faltan enlaces canónicos inequívocos y licencias. No elegir un repositorio por coincidencia de nombre. «Kerberos Agent» pertenece a videovigilancia, no a gestión de estacionamientos; se evaluaría en esa categoría.

## Ruta de integración con JFXAI4CBS

Propuesta: fuente de visión o sensores → adaptador de estacionamiento → Mosquitto → Ditto e historial → panel e IA. Desarrollar el adaptador; ninguno de estos proyectos se ha verificado con integración nativa MQTT, Ditto u OIDC.

- Representar instalación, zona, plaza, cámara, sensor y barrera con identificadores estables. Ditto mantiene estado observado y su calidad; el servicio de reservas conserva transacciones.
- Separar ocupación física (`free`, `occupied`, `unknown`) y reserva comercial. Una reserva no prueba ocupación; una cámara desconectada produce estado desconocido, no plaza libre.
- Proponer eventos `parking.slot.observed`, `parking.reservation.created`, `parking.reservation.cancelled`, `parking.session.started` y `parking.session.ended`. No son interfaces nativas verificadas de los candidatos.
- Cada evento incluye `schema_version`, `event_id`, `source`, `asset_id`, `lot_id`, `slot_id`, `observed_at`, `received_at` y calidad; los eventos de visión añaden versión del modelo y confianza. Validar esquemas, deduplicar y controlar estados obsoletos.
- El adaptador de Parker necesita extraer observaciones y publicarlas de forma autenticada; no asumir que una pestaña cerrada mantiene el servicio. Para continuidad operacional, evaluar un proceso de borde persistente.
- Reservas requieren creación atómica, expiración y pruebas de concurrencia. Integrar TheParker o Ezy-Parking mediante una API que se deberá inspeccionar o desarrollar; no asumir REST u OIDC existentes.
- Mantener matrículas, identidad, pagos e imágenes fuera de los eventos generales. Publicar referencias protegidas cuando sean necesarias; el gemelo no necesita plantillas biométricas.
- Las barreras requieren un controlador local con interbloqueos y apertura manual. La detección visual por sí sola no autoriza movimiento.
- Evaluar Keycloak según capacidades reales del sistema elegido, y Wazuh para supervisión de hosts. Simular flujos y colas con modelos validados; Ditto conserva estado, no sustituye el simulador.

## Piloto y condiciones de promoción

1. Probar Parker en una cámara fija y plazas delimitadas: medir errores por plaza, oclusión, noche, lluvia y latencia.
2. Construir el adaptador y verificar observación → MQTT → gemelo correcto, duplicados, reconexión y estado desconocido tras pérdida de señal.
3. Elegir un gestor de reservas tras verificar despliegue, autenticación, consistencia y funciones reales. Ensayar dos reservas concurrentes de la misma plaza.
4. Revisar licencia del código, bibliotecas, pesos y datos; fijar commit, documentar configuración y revisar dependencias antiguas.
5. Promover solamente tras superar las pruebas. La integración de control de barreras y cobros constituye una etapa separada.

El registro legible por máquina está en [catalog/parking-integrations.json](../../catalog/parking-integrations.json). Las entradas son candidatos y referencias, no dependencias de ejecución aceptadas. El compendio de JFXAI4CBS sigue siendo una propuesta documental.
