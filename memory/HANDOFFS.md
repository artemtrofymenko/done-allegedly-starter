# HANDOFFS

What goes in: one entry per working session, written by the agent before it stops.
Append-only: add new entries at the bottom, never edit an old one. The last entry is the newest.
What never goes in: secrets (passwords, keys, tokens, card numbers, private links), raw chat
transcripts. Summarize instead.
"Verified" means the agent saw the result where it lands, and says how. A success message from
the tool that did the work goes under "Not verified".

Format:

    ## [date] | [agent] | [task in a few words]
    - Done:
    - Verified (how):
    - Not verified:
    - Files changed:
    - Rollback:
    - Next for human:

---

EXAMPLE - delete me

## 2026-03-12 | Claude Code | product feed: missing weights
- Done: copied weights for 12 items from `data/product-sheet.csv` into `feed/products.csv`.
  2 items (MUG-07, MUG-09) have no weight in the sheet and were left empty.
- Verified (how): opened `feed/products.csv` from disk after saving and counted rows with an
  empty weight: 2, both mugs. Checked 3 filled rows against the product sheet by hand: they match.
- Not verified: whether the marketplace accepts the file. It has not been uploaded, and I have
  no access to the marketplace.
- Files changed: `feed/products.csv`. Backup of the old file: `feed/products.before-weights.csv`.
- Rollback: replace `feed/products.csv` with `feed/products.before-weights.csv`.
- Next for human: upload `feed/products.csv` to the marketplace; weigh MUG-07 and MUG-09.

END OF EXAMPLE
