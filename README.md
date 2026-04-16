# Agente de Time Blocking Diario

Agente remoto de Claude Code que se ejecuta diariamente a las 07:00 AM (America/Cancun).

## Que hace

1. Lee tareas pendientes de una base de datos de Notion
2. Las organiza por prioridad (Alta > Media > Baja)
3. Estima la duracion de cada tarea segun su dificultad
4. Crea bloques de tiempo en Google Calendar con el prefijo `[Agente]`
5. Envia un email resumen del dia via Gmail

## Setup

### Prerequisitos

- Claude Code con acceso a MCP: Notion, Google Calendar, Gmail
- Base de datos de Notion con el esquema definido en `CLAUDE.md`

### Configurar Remote Trigger

```
Cron:          0 7 * * *
Zona horaria:  America/Cancun
Prompt:        agents/daily-time-blocker.md
```

## Estructura

```
agents/daily-time-blocker.md  -- Prompt completo del agente
CLAUDE.md                     -- Configuracion e IDs de recursos
README.md                     -- Este archivo
```
