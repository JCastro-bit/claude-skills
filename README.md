# claude-skills

Colección personal de skills para Claude Code. Cada skill es un conjunto de instrucciones que Claude Code aplica automáticamente en contextos específicos.

## Instalación

### Opción A — Instalar directamente

```bash
claude install-skill /ruta/a/claude-skills/prompt-framework
```

### Opción B — Clonar y usar desde el repo

```bash
git clone https://github.com/JCastro-bit/claude-skills.git ~/.claude-skills
claude install-skill ~/.claude-skills/prompt-framework
```

### Opción C — Symlink desde dotfiles

```bash
ln -s /ruta/a/claude-skills ~/.claude/skills
```

## Skills disponibles

| Skill | Descripción |
|-------|-------------|
| [prompt-framework](./prompt-framework/) | Framework de prompts estructurados para planear y construir proyectos |

### prompt-framework

Framework que Claude Code aplica automáticamente al ayudarte a planear y construir proyectos. Incluye 7 triggers con comportamientos prescriptivos:

| Trigger | Qué hace |
|---------|----------|
| Proyecto sin contexto | Pregunta QUÉ, PARA QUIÉN, POR QUÉ antes de escribir código |
| Feature sin estructura | Reformula en patrón RCF (Resultado -> Criterio -> Formato) |
| Feedback vago | Bloquea rehacer y pide cambios enumerados |
| Bug sin contexto | Pide los 4 datos estructurados para diagnosticar |
| Crear CLAUDE.md | Guía sección por sección con template |
| Cerrar sesión | Genera resumen técnico para retomar después |
| Retomar sesión | Lee resumen, confirma estado, propone siguiente paso |

Además aplica desarrollo en 5 fases (Planificación -> Fundación -> Construcción -> Integración -> Pulido) con checkpoints de aprobación entre cada fase.

**Archivos:**
- `SKILL.md` — Instrucciones principales con triggers y comportamientos
- `references/claude-md-template.md` — Templates reutilizables (CLAUDE.md, restricciones, resumen de sesión)

## Créditos

El framework `prompt-framework` está basado en el trabajo de **Erik Taveras** ([@eriktaveras](https://eriktaveras.dev)) de Taveras Solutions.
