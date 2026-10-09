# Esquema de datos

## Base de datos

- **Nombre:** Centro de Comando — Contenido Clínica
- **Tipo:** Base de datos de Notion
- **Database ID:** `3d5b55b2-56b6-40e0-a765-379b8d915c96`
- **Data Source ID:** `d2e9bc58-4321-46de-b701-161dd2c0987f`
- **Link de solo lectura:** (completar con el link que compartas desde Notion con permiso "Can view")

## Campos (propiedades)

| Campo | Tipo | Valores posibles | Quién lo escribe |
|---|---|---|---|
| Idea Semilla | Título | Texto libre | Carga manual (semilla del contenido) |
| Estado | Selección | Generando, En revisión, Aprobado, Rechazado, Publicado | Make (módulos 14 y 15) |
| Aprobado | Casilla | Sí / No | Persona (punto HITL) |
| Borrador Generado | Texto | Texto generado por la IA | Make, módulo 14, con el resultado de Claude |
| Fecha de última ejecución | Fecha | Fecha y hora | Make, módulos 14 y 15 |

## Ciclo de vida de una fila

1. Se crea la fila con **Idea Semilla** y **Estado = Generando**.
2. El trigger (módulo 16) detecta la fila nueva y dispara el escenario.
3. OpenAI clasifica el tema y Claude redacta el posteo.
4. Módulo 14 guarda el borrador en **Borrador Generado** y cambia **Estado = En revisión**.
5. Una persona revisa el texto y tilda **Aprobado**.
6. Módulo 15 cambia **Estado = Publicado** después de que Slack envía el mensaje.

## Estado actual de la base (dato real, consultado el 9/10/2026)

| Estado | Cantidad de filas |
|---|---|
| En revisión | 7 |
| Aprobado | 1 |
| Publicado | 5 |

Total: 13 filas.
