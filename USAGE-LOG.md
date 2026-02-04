# Background usage log

Optional, off-by-default. No UI; the main tool does not show any tracking.

## Enable logging

1. In `index.html`, set `USAGE_LOG_URL` to your collector endpoint, e.g.:
   ```js
   const USAGE_LOG_URL = 'http://localhost:8765/log';
   ```
2. Run the collector (see below), or use your own endpoint that accepts POST with JSON body.

## Collector (included)

- **Start server:** `node usage-log-server.js`  
  Listens on port 8765, appends each POST to `usage-log.jsonl`.
- **Summarize:** `node usage-log-summary.js`  
  Reads `usage-log.jsonl` and prints total runs, unique users, weapon combos, class breakdown, etc.

## Payload (per run)

Each run sends one POST with a JSON object, e.g.:

- `event`: `"sim_run"`
- `v`: app version
- `uid`: anonymous persistent id (localStorage)
- `ts`: timestamp
- `w1`: `{ preset, damage, delay, is2H }`
- `w2`: same or `null`
- `classId`, `durationSec`, `runs`, `totalDamage`
- `specialAttacks`, `fistweaving` (booleans)

`usage-log.jsonl` is in `.gitignore`.
