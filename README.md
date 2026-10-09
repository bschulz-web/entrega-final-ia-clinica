# Entrega Final — Ecosistema de Automatización IA Autónomo

Automatización para una clínica médica: genera, revisa y publica contenido para redes sociales, sin intervención manual salvo la aprobación final.

## Categorías tecnológicas usadas

| Categoría | Herramienta |
|---|---|
| Orquestador | Make.com |
| Base de datos | Notion |
| IA | OpenAI (gpt-4o-mini) + Anthropic Claude (Haiku 4.5) |
| Salida | Slack |

## Contenido de este repositorio

| Archivo | Qué es |
|---|---|
| `01_arquitectura.pdf` | Diagrama de arquitectura del escenario |
| `02_esquema_de_datos.md` | Campos de la base de Notion y su ciclo de vida |
| `03_matriz_de_costos.md` | Comparación de costos OpenAI vs Claude, con datos reales |
| `04_seguridad_y_resiliencia.md` | Manejo de errores, punto de control humano, autochequeo |
| `05_dashboard.html` | Dashboard de control (abrir en el navegador) |
| `ENTREGA_FINAL.blueprint.json` | Exportación del escenario de Make |
| `/screenshots` | Capturas de las 5 pruebas en vivo |

## Link de solo lectura a la base de Notion

(completar con el link que compartas desde Notion con permiso "Can view")

## Punto de control humano (HITL)

Ninguna publicación sale a Slack sin que una persona apruebe el borrador tildando la casilla "Aprobado" en Notion.

## Pruebas en vivo

5 pruebas reales ejecutadas y verificadas contra la base de datos real (ver `/screenshots` y `04_seguridad_y_resiliencia.md`), incluyendo un camino infeliz con un error forzado a propósito.
