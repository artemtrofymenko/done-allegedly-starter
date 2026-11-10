# INCIDENTS

What goes in: anything that went wrong because someone (agent or human) believed something
false. Write the false belief exactly; it is the useful part. A stop and audit (rule 5 in
AGENTS.md) ends with an entry here.
Append-only: add new entries at the bottom.
What never goes in: secrets (passwords, keys, tokens, card numbers, private links), raw chat
transcripts, blame. Name the false belief, not the person.

Format:

    ## [date] | [what broke, in a few words]
    - What happened:
    - The false belief:
    - What it cost:
    - Rule changed:

---

EXAMPLE - delete me

## 2026-03-05 | Sale prices missing on the marketplace
- What happened: the agent lowered 20 prices in `feed/products.csv` for a weekend sale and
  reported "prices updated". The marketplace kept showing the old prices all weekend.
- The false belief: "the file I edited is the file the marketplace reads". The marketplace reads
  the copy the owner uploads; nobody had uploaded the new one.
- What it cost: the sale ran on the shop's own site only; two customers emailed to ask why the
  marketplace price was higher.
- Rule changed: none new; AGENTS.md rule 1 (written is not in effect) already covers it.
  From now on, a feed change goes into the human queue as "upload the feed" until the owner
  confirms the upload.

END OF EXAMPLE
