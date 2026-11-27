# Skills & agents catalog sync — 2026-11-27

This repo's catalogs were synced with the live Clawd fleet sources:

| Source (as given) | Resolves to | What was taken |
| --- | --- | --- |
| clawdcompute.us/skills | live skills hub (674 unique skills) | Catalog entries: slug, name, description, category |
| clawdcompute.us/agents | live agents catalog (139 agents) | Agent records not already present here |
| github.com/Solizardking/skills | **moved → github.com/themusebook/skills** | Full skill folders for slugs not already in `skills/` |
| github.com/Solizardking/agents | **moved → github.com/themusebook/clawd-agents** | The paired repo of the clawdcompute.us/agents catalog |

## Results

- `skills/catalog.json`: **105 → 675 entries** (+570). Existing entries are
  untouched and keep their position; new entries carry
  `"source": "clawdcompute.us/skills"` (and `"source_repo": "themusebook/skills"`
  when a local folder was also imported).
- `skills/<slug>/`: **+115 folders, 6,520 files (~58 MB)** imported from
  themusebook/skills. Folders already present here were **not** overwritten —
  this repo's copies win; the hub/repo copies remain upstream.
- `agents/agents-catalog.json`: **130 → 179 agents** (+49 from
  clawdcompute.us/agents, each tagged `"source": "clawdcompute.us/agents"`;
  a `catalogSync` block records the sync). Existing agents untouched.

## Exclusions (deliberate)

- Files over 1 MB were not imported (5 files): two 4k mascot PNGs and a
  workflow diagram (in `solana-clawd-agents`, `nvidia`), and two generated
  scanner data files (`skills-store/scanner`). They remain in
  themusebook/skills.
- Secret scan over all imported folders: the only pattern hits were
  documented placeholders (`your-helius-api-key`, `sk-test…`, `<redacted>`)
  in reference docs — no real credentials imported.
- The ~570 hub-only catalog entries (e.g. `anthropic-skills/*`,
  `agent-orchestration/*`) have no folder in themusebook/skills; their
  SKILL.md is served by the hub at
  `clawdcompute.us/api/skills/<slug>/SKILL.md`, which is what their catalog
  entries point back to via the `source` field.

## Re-running the sync

The catalogs are snapshots. Re-run by re-fetching
`clawdcompute.us/agents/catalog.json` and the skills hub index, diffing by
`slug` / `identifier`, and appending only new entries — never overwriting
existing ones.
