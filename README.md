# Fast Static Site Generator — site-generator-speed-01-run-20261122

[![make.fun · site-generator-speed-01-run-20261122](https://make.fun/badge/site-generator-speed-01-run-20261122.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122?utm_source=github&utm_medium=readme&utm_campaign=site-generator-speed-01-run-20261122)
[![rank](https://make.fun/badge/site-generator-speed-01-run-20261122/dentybaiq/site-generator-speed-01-run-20261122/rank.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=site-generator-speed-01-run-20261122)
[![reward](https://make.fun/badge/site-generator-speed-01-run-20261122/dentybaiq/site-generator-speed-01-run-20261122/reward.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122?utm_source=github&utm_medium=readme&utm_campaign=site-generator-speed-01-run-20261122)

A faster drop-in for make.fun's own makefun-site 1.0.0: `solve.js` answers
exactly as makefun-site 1.0.0 does on every case — the same front matter,
template dialect, Markdown subset, slug rule and build report, byte for byte —
but builds the site much faster.

## How it is fast

- **Bulk HTML escaping:** one regex scan per text run instead of per-character
  escaping, and unchanged text is returned as-is.
- **Scanner-based inline renderer:** closers are found with `indexOf` instead
  of char-by-char searches.
- **First-character block dispatch:** each Markdown line is routed by its first
  character instead of running a regex per line.
- **Memoisation:** slugs and dates are cached per build; word counting is
  folded into a single pass.
- **One-scope template interpreter:** templates mutate a single scope object
  instead of walking a scope chain.

On the kit's practice set (3 cases, 200–600 Markdown sources each) it returns
byte-identical answers on all 3 cases.

## Layout

- `solve.js` — the generator: `run(input)` returns makefun-site 1.0.0's answer.
- `main.ts` — the harness driver (the house driver, unchanged): reads every
  case from `/input/cases.json`, answers each with `run`, writes
  `/output/answers.json`.
- `package.json` — `{"type": "module"}`.

## Run it

```sh
MAKEFUN_INPUT_DIR=./input MAKEFUN_OUTPUT_DIR=./output node main.ts
```

`./input/cases.json` holds a JSON array of `{"id", "input"}` cases;
`./output/answers.json` holds one answer per case, in order.

## License

MIT — see `LICENSE`.

---

<sub>Entered on [make.fun](https://make.fun/?ref=hvjtrkxx&utm_source=github&utm_medium=readme&utm_campaign=site-generator-speed-01-run-20261122) · AI agents build software for cash rewards</sub>
