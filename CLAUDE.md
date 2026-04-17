# Agente de Time Blocking Diario

## Descripción

Agente remoto (Remote Trigger) de Claude Code que se ejecuta diariamente a las
07:00 AM (America/Cancun). Lee tareas pendientes de Notion, las organiza por
prioridad, estima su duración, crea bloques de tiempo en Google Calendar, y
envía un email resumen a Gmail. Todo en español.

## Estructura del proyecto

```
agent/
  daily-planner-agent.md   # Prompt principal del agente (Remote Trigger)
CLAUDE.md                  # Este archivo
README.md                  # Resumen del proyecto
```

## Configuración del Remote Trigger

### 1. Conectores MCP necesarios

- **Notion** — lectura de base de datos y páginas
- **Google Calendar** — lectura y escritura de eventos
- **Gmail** — creación de borradores de email

### 2. Base de datos de Notion

Crear una base de datos con estos campos exactos:

| Campo              | Tipo   | Valores                           |
|--------------------|--------|-----------------------------------|
| Nombre de la tarea | Title  | Texto libre                       |
| Estado             | Status | Pendiente, En progreso, Completada|
| Prioridad          | Select | Alta, Media, Baja                 |
| Dificultad         | Select | Fácil, Moderado, Difícil          |

### 3. Cron

```
0 7 * * *    America/Cancun
```

### 4. Prompt del trigger

Usa el contenido de `agent/daily-planner-agent.md` como prompt del Remote Trigger.

## Flujo de ejecución

1. Lee tareas no completadas de Notion
2. Lee eventos de Google Calendar (hoy + 4 días)
3. Estima duración de cada tarea
4. Planifica distribución en huecos libres
5. Crea/actualiza eventos `[Agente]` en Google Calendar
6. Envía email resumen vía Gmail (como borrador)

## Limitaciones conocidas

- **Gmail**: solo puede crear borradores (`gmail_create_draft`), no enviar
  directamente. Cuando `gmail_send_draft` esté disponible, el agente lo usará.
- **Transparencia de eventos**: la API de Google Calendar MCP no expone el
  parámetro `transparency`. Los eventos no se marcan como "disponible".
- **Notion**: el agente nunca escribe en Notion (solo lectura).

## Convenciones

- Todos los eventos creados llevan el prefijo `[Agente]` en el título
- Ventana de trabajo: 09:00 - 21:00 America/Cancun
- Bloques máximos de 180 minutos (3 horas)
- Colores: Alta=Tomato(11), Media=Tangerine(6), Baja=Banana(5)
