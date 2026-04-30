# UI Design Skills

Quickstart (30-second setup)

Run the skills installer via npx:

```bash
npx skills@latest add otmanesabiri/ui-design-skills
```

Pick the skills you want, and which coding agents you want to install them on. Make sure you select `/setup-otmanesabiri-skills` in the repo you add, then run that setup script in your agent. It will:

- Ask which issue tracker you want to use (GitHub, Linear, or local files)
- Ask what labels you apply when triaging ticks (used by `/triage`)
- Ask where to save any docs we create

Bam — you're ready to go.

Notes:

- To use `npx skills@latest` as-is you must publish this package to npm under the name `skills`. Alternately, run directly from GitHub without publishing:

```bash
npx github:otmanesabiri/skills add otmanesabiri/skills
```

