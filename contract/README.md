# The contract

Machine-written. Nothing here is edited by hand.

`vocabulary.ts` is generated from `tessera/api/vocabulary.py`: the nine core signals,
story states, card labels, round kinds, ladders, functions and the 203-topic taxonomy.
`queues.json` is every queue a Procrastinate task registers on.

Both are published to the public `tessera-releases` repo by `.github/workflows/contract.yml`
after CI passes. `tessera-desktop` and `tessera-mobile` each commit a copy of
`vocabulary.ts` and fail their own build when it differs from the published one;
`tessera-deploy` checks its compose file against `queues.json` before a deploy.

To change any of it: edit the Python, run `./scripts/gen-vocabulary.py`, commit both.
The clients pick it up with their own `./scripts/sync-vocabulary.sh`.

The reason this exists rather than each repo typing the words itself: one vocabulary
drifting into two has broken this product three times, and every time it failed in front
of a user rather than at build time. A `Tags` component taking `items` on one side and
`tags` on the other. An interview card carrying `claim_text` in the client and `claim`
in the server. `DebriefWrite.state` defaulting to `pending` while both clients tested
for `proposed`, which left the consent gate unreachable while showing a veto nobody had
made.
