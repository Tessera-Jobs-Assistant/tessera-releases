# Tessera releases

Public, and holds only what has to be readable without a credential.

## Downloads

Installers for the desktop app are attached to each [release](../../releases). The
project page at [omiiyamu.com/projects/tessera](https://omiiyamu.com/projects/tessera)
reads the latest one at render time, so it never needs editing when a version ships.

`latest.json` beside them is the update manifest. Every installed copy polls it hourly
and checks the signature against a public key compiled into the binary.

## `contract/`

`vocabulary.ts` is generated from `tessera/api/vocabulary.py` in `tessera-server`: the
signal names, story states, card labels, round kinds and the 203-topic taxonomy. Both
clients commit a copy so they build without network access, and both fail CI when their
copy differs from this one.

It is here, in public, because the alternative is a read token in two more repositories,
and because the file is already inside every shipped binary. 203 topic labels and nine
signal names leak nothing that a download does not.

`queues.json` is the queues every Procrastinate task registers on. `tessera-deploy`
checks its compose file against it before a deploy. A task on a queue nothing consumes
is enqueued and then sits there: no error, no log, the feature simply never happens.
That shipped once, for research, which is why it is checked now.

Everything here is written by CI. Nothing is edited by hand.
