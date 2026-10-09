# Seguridad y resiliencia

## Manejo de errores (probado en vivo)

Se probó a propósito un **camino infeliz**: correr el módulo Notion 14 con el campo obligatorio "Database Item ID" vacío.

Resultado: Make detectó el dato faltante y bloqueó la ejecución con un error controlado (`BundleValidationError — Missing value of required parameter 'page'`), sin romper el resto del escenario ni escribir datos corruptos en Notion. Captura de este error incluida en `/screenshots`.

## Punto de control humano (HITL)

Ninguna publicación en Slack llega sin que una persona revise el borrador y tilde la casilla **Aprobado** en Notion. Esto evita que la IA publique contenido sin supervisión.

## Prevención de bucle infinito

- El trigger de Notion (módulo 16) solo escucha filas **nuevas** (`select: create`), no cambios repetidos sobre la misma fila. Una fila ya procesada no vuelve a disparar el escenario.
- El Router tiene dos rutas con condiciones distintas (generar borrador / publicar tras aprobación), por lo que una misma fila no puede recorrer las dos rutas en la misma ejecución.
- No hay ningún módulo que escriba de vuelta en el campo que el propio trigger está mirando, así que no hay riesgo de retroalimentación infinita.

## Tipos de datos controlados

- **Estado** es un campo de selección con una lista fija de opciones (Generando, En revisión, Aprobado, Rechazado, Publicado). No se puede guardar un valor fuera de esa lista.
- **Aprobado** es una casilla (verdadero/falso), no texto libre, así que no admite valores ambiguos.

## Prompts dinámicos (no hardcodeados)

El prompt que arma el posteo usa variables reales, no texto fijo:
- `[16. Properties Value: Idea Semilla]` → el tema de la fila.
- `[19. Result]` → la categoría que devolvió OpenAI.

Esto significa que el mismo módulo sirve para cualquier idea nueva, sin tener que tocar el escenario.

## Credenciales

- Las conexiones a Notion, OpenAI, Anthropic y Slack están guardadas dentro de Make como conexiones autenticadas (OAuth / API key gestionada por Make). Ninguna clave aparece en los prompts, en los nombres de los módulos ni en las capturas.
- En el video demo, el panel de conexiones no se muestra expandido, para no exponer ningún dato de cuenta.

## Problemas conocidos (documentados con honestidad)

| Problema | Causa | Cómo se resolvió |
|---|---|---|
| El trigger "Watch Data Source Items" de Notion no entregaba datos reales en ejecuciones completas del escenario ("Run once") | Limitación conocida de esa combinación Make + Notion en este tipo de conexión | Se generó evidencia real igual, ejecutando cada módulo por separado ("Run this module") con datos reales de Notion, y verificando cada resultado contra la base de datos real con consultas directas |
| La cuenta de OpenAI se quedó sin crédito durante las pruebas | Error externo de facturación de la cuenta, no del escenario | Se dejó el módulo de OpenAI armado y configurado en el escenario (evidencia de arquitectura real de dos proveedores) y se usaron precios oficiales publicados para la comparación de costos, en vez de pagar más crédito |

## Autochequeo de seguridad antes de la entrega

- [x] No hay API keys ni contraseñas visibles en el escenario, capturas o video.
- [x] El filtro de "Estado" usa una lista cerrada de opciones (no texto libre).
- [x] El trigger no puede generar un bucle infinito (solo escucha filas nuevas).
- [x] Los prompts usan variables dinámicas, no texto fijo.
- [x] Se probó al menos un camino de error a propósito y quedó documentado.
