# Agente de Time Blocking Diario

## Descripcion

Agente remoto (Remote Trigger) que se ejecuta diariamente a las 07:00 AM (America/Cancun).
Lee tareas pendientes de Notion, las organiza por prioridad, estima su duracion,
crea bloques de tiempo en Google Calendar, y envia un email resumen via Gmail.

Todo el output es en espanol.

## Configuracion del Remote Trigger

- **Cron**: `0 7 * * *` (todos los dias a las 07:00 AM)
- **Zona horaria**: `America/Cancun`
- **Prompt**: Contenido de `agents/daily-time-blocker.md`

## Recursos externos

### Notion
- **Base de datos**: "Tareas Time Blocking"
- **Database ID**: `55b917844a824df5962973e6a7efc8d2`
- **Data Source ID**: `fb1dd6dc-f559-44c3-943a-3552051a07a5`
- **URL**: https://www.notion.so/55b917844a824df5962973e6a7efc8d2
- **Pagina contenedora**: "Productividad - Time Blocking" (`34483b69-8081-81f8-8d27-f90e0275fe4a`)

### Google Calendar
- **Calendario**: `ivan@invedx.com`
- **Zona horaria**: `America/Cancun`
- **Ventana de trabajo**: 09:00 - 21:00

### Gmail
- **Destinatario**: `ivan@invedx.com`

## Esquema de la base de datos Notion

| Campo | Tipo | Valores |
|---|---|---|
| Nombre de la tarea | Title | Texto libre |
| Estado | Status | Sin empezar, En progreso, Listo |
| Prioridad | Select | Alta, Media, Baja |
| Dificultad | Select | Facil, Moderado, Dificil |

El contenido de cada pagina (debajo del titulo) se usa como SOP/descripcion del evento.

## Conectores MCP requeridos

- **Notion**: Solo lectura (el agente NUNCA escribe en Notion)
- **Google Calendar**: Lectura + escritura (solo eventos con prefijo `[Agente]`)
- **Gmail**: Solo envio (crear draft)

## Estructura del proyecto

```
/agents/daily-time-blocker.md   # Prompt del agente (remote trigger)
/CLAUDE.md                      # Este archivo
/README.md                      # Documentacion del proyecto
```
