# Matriz de costos — comparación de modelos de IA

## Por qué dos proveedores

El escenario usa **dos proveedores de IA en la misma tarea** (clasificar el tema y redactar el posteo), para poder justificar con datos reales por qué se eligió cada uno.

- **OpenAI gpt-4o-mini** → clasifica el tema en una categoría. Tarea corta y simple: no necesita un modelo caro.
- **Anthropic Claude Haiku 4.5** → redacta el posteo final. Tarea más larga y que necesita buen estilo de escritura: se le pide más calidad.

## Precios publicados (oficiales, por millón de tokens)

| Modelo | Input (por 1M tokens) | Output (por 1M tokens) |
|---|---|---|
| OpenAI gpt-4o-mini | USD 0.15 | USD 0.60 |
| Anthropic Claude Haiku 4.5 | USD 1.00 | USD 5.00 |

## Dato real capturado (ejecución real del escenario)

La cuenta de OpenAI se quedó sin crédito durante las pruebas, así que no se pudo medir su consumo real de tokens. El consumo de Claude sí se midió, corriendo el módulo real en Make:

| Ejecución (Claude Haiku 4.5) | Tokens de entrada | Tokens de salida | Costo real (según precio publicado) | Créditos de Make |
|---|---|---|---|---|
| "Prueba definitiva post módulo 16" | 214 | 407 | USD 0.00225 | 3.49 |
| "Beneficios de dormir bien" | — (no registrado) | — | — | 3.19 |
| "Ventajas de vacunarse..." | — | — | — | 3.95 |
| "Consejos de hidratación..." | — | — | — | 4.02 |

El costo en USD de Claude por ese posteo real fue de aproximadamente **0.2 centavos de dólar**.

## Estimación para OpenAI (no se pudo medir real, por falta de crédito)

Usando una estimación conservadora de la tarea (prompt corto + una palabra de respuesta: ~80 tokens de entrada, ~5 de salida):

| Modelo | Tokens estimados | Costo estimado |
|---|---|---|
| OpenAI gpt-4o-mini (clasificación) | 80 in / 5 out | USD 0.000015 |

## Conclusión

Con tareas cortas como estas, el costo en dólares es casi insignificante en ambos casos. La diferencia real está en el **precio por token**: Claude Haiku 4.5 cuesta entre 6 y 8 veces más que gpt-4o-mini. Por eso tiene sentido usar el modelo más barato (OpenAI) para la tarea simple (clasificar) y reservar el modelo más caro (Claude) para la tarea que necesita mejor redacción.

**Nota de transparencia:** la cuenta de OpenAI usada en el curso se quedó sin crédito durante las pruebas (error real de facturación, no del escenario). Se decidió seguir con precios publicados oficialmente en vez de cargar crédito, para no atrasar la entrega. El módulo de OpenAI quedó armado y configurado en el escenario como evidencia de la arquitectura de dos proveedores.
