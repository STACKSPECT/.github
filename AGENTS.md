# Project agent memory

This file is the project's committed home for project-intrinsic agent knowledge: build, test, release, architecture, and sharp-edge notes that should travel with the code.

This repository is the STACKSPECT **organisation profile**. `profile/README.md` is what a
visitor sees at `github.com/STACKSPECT`; `img/` holds the pictures it uses. There is no build,
no test suite and no application code.

## Sharp edges

- **Every claim on the page must trace to the other repositories' code**, not to their READMEs
  — those are rewritten often and go stale. Read the source, the configs and each repo's own
  `AGENTS.md`, and run its tests.
- **`Simulation`'s work is on `dev`, not `main`.** `main` is an older, much smaller skeleton,
  so a link to that repo's default branch shows a visitor something other than what the page
  describes. Check before linking.
- **Reference images by this repository's own raw URL on `main`**
  (`https://raw.githubusercontent.com/STACKSPECT/.github/main/img/<file>`). Never hotlink
  another repository's files: a branch rename there silently breaks the front page. New images
  404 until the PR merges — that is expected, not a mistake.
- **Do not put a hard-coded `%%{init}%%` palette on Mermaid diagrams.** GitHub themes Mermaid
  to the reader's colour mode; a fixed dark palette renders near-invisible text in light mode.
  Leave the theme alone and the diagram works in both.
- **In a Mermaid `flowchart`, `direction LR` inside a subgraph is ignored** once an edge points
  at a node *inside* that subgraph from outside it. Aim such edges at the subgraph itself.

## Previewing the page

Render with GitHub's own markdown API and **`"mode": "markdown"`** — `"mode": "gfm"` applies
comment-style hard line breaks that README files do not have, which makes badge rows and
paragraphs render wrongly:

```bash
gh api -X POST /markdown --input <(jq -n --rawfile t profile/README.md '{text:$t,mode:"markdown"}')
```

Check both colour schemes, and phone width (~390 px) for horizontal overflow.

## Images

Resize to 1440 px wide with a **box** filter (Lanczos rings on flat-shaded renders and
compresses worse), drop alpha, quantise to a 256-colour palette with octree and **no** dither,
then oxipng at maximum effort. Look at every result before accepting it — dithering speckles
these renders' floors and gradients. Typical saving is 80–90 %.

## Maintaining this file

Keep this file for knowledge useful to almost every future agent session in this project.
Do not repeat what the codebase already shows; point to the authoritative file or command instead.
Prefer rewriting or pruning existing entries over appending new ones.
When updating this file, preserve this bar for all agents and keep entries concise.
