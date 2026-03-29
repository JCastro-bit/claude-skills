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
| [prompt-framework](./prompt-framework/) | Framework de prompts estructurados: 5 reglas, patrón RCF, fases de desarrollo, debugging, gestión de sesiones y generación de CLAUDE.md |

## Créditos

El framework `prompt-framework` está basado en el trabajo de **Erik Taveras** ([@eriktaveras](https://eriktaveras.dev)) de Taveras Solutions.
