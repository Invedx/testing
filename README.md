# Agente de Time Blocking Diario

Agente remoto de Claude Code que automatiza la planificación diaria:

1. Lee tareas pendientes de **Notion**
2. Calcula huecos libres en **Google Calendar**
3. Estima duraciones y distribuye bloques de tiempo
4. Crea eventos `[Agente]` en Google Calendar (con colores por prioridad)
5. Envía email resumen en español vía **Gmail**

## Inicio rápido

1. Configura los conectores MCP: Notion, Google Calendar, Gmail
2. Crea la base de datos de Notion (ver `CLAUDE.md` para el esquema)
3. Configura un Remote Trigger con cron `0 7 * * *` (America/Cancun)
4. Usa `agent/daily-planner-agent.md` como prompt del trigger

## Documentación

- [`CLAUDE.md`](CLAUDE.md) — Documentación completa del proyecto
- [`agent/daily-planner-agent.md`](agent/daily-planner-agent.md) — Prompt del agente
