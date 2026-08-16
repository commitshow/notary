# Legit.Show — daily score fingerprint

Every night, Legit.Show hashes the benchmark scores of its whole catalogue into a single
fingerprint (a Merkle root) and commits it here.

**Why this repository exists.** The fingerprint was already computed and published on our
own servers. That is worth little on its own: if we could change a score after the fact, we
could change the fingerprint with it. Committing it somewhere we do not control fixes that.
Git records the date, GitHub holds the copy, and neither is ours to rewrite quietly.

**How to use it.** Save the line for any date. If a score from that date is later changed,
the fingerprint for that date no longer matches the catalogue — and the line you saved says
what it was.

    date        spec  algo    leaves  root
    2026-08-17  v2    sha256   7,665  aab37cfb…

`spec` is the encoding version, stored per day on purpose: when the overall score became
public the encoding changed to v2, and days recorded under v1 still verify under v1. A
change to how we compute the fingerprint must never quietly invalidate an older proof.

**What this does and does not prove.** It proves the scores for a given date have not been
altered since that date. It does not let a third party recompute the root from scratch: leaf
hashes are salted with a server-side secret, which keeps the published tree from becoming a
brute-forceable index of everything we have measured. So this is a commitment, not a
trustless proof, and we say so rather than implying otherwise.

Method: https://legit.show/methodology
