# Design Engineer Skill

A Claude Code agent skill for building interfaces that feel crafted, intentional, and alive.

This is a skill graph — a traversable knowledge base covering philosophy, visual craft, motion, and component patterns. Claude follows the wikilinks to load only what's relevant for the task at hand.

## What's inside

- **philosophy** — why things should feel a certain way; the intentionality behind motion and craft
- **visual-craft** — CSS techniques for visual polish: color, alignment, depth, borders, performance
- **motion** — animation and interaction: gestures, transitions, layout animations, enter/exit choreography
- **patterns** — full component implementations that combine multiple techniques into real UI
- **reference** — supporting material the graph links into

The entry point is [`SKILL.md`](./SKILL.md).

## Install

```bash
npx skills add outlawcollin/design-engineer-skill -y -g
```

Or clone manually into your Claude skills directory:

```bash
git clone https://github.com/outlawcollin/design-engineer-skill ~/.claude/skills/design-engineer-skill
```

Or symlink from a repo you keep elsewhere:

```bash
git clone https://github.com/outlawcollin/design-engineer-skill ~/code/design-engineer-skill
ln -s ~/code/design-engineer-skill ~/.claude/skills/design-engineer-skill
```

## Use

Inside Claude Code, the skill triggers automatically when you're working on UI polish, animation, component design, or visual craft. You can also invoke it explicitly by mentioning design engineering in your prompt.

## Updating

```bash
cd ~/.claude/skills/design-engineer-skill && git pull
```
