# PROJECT-STATE

What goes in: where the project stands right now, in a few lines. This file is a snapshot.
Overwrite the whole file at the end of every session that changed a file.
What never goes in: secrets (passwords, keys, tokens, card numbers, private links), raw chat
transcripts, history. History goes in HANDOFFS.md.
Before you overwrite: read this file right before writing, and keep what another agent wrote
that is still true.

Format:

    Updated: [date] by [agent]
    ## Current task
    ## Status
    ## Verified
    ## Human queue      (only what the human must do; one line each: what, and why it needs them)

---

EXAMPLE - delete me

Updated: 2026-03-12 by Claude Code

## Current task
Fix the product feed so the marketplace stops rejecting items for a missing weight.

## Status
`feed/products.csv` now has a weight for 12 of the 14 rejected items. The other 2 (MUG-07,
MUG-09) have no weight in `data/product-sheet.csv`, so their weight is still empty.

## Verified
- 12 of 14 rows filled: counted in `feed/products.csv` after the change.
- Not verified: whether the marketplace accepts the new file. It has not been uploaded yet.

## Human queue
- Upload `feed/products.csv` to the marketplace. Only you have the login.
- Weigh MUG-07 and MUG-09 and add the weights to the product sheet. Only you have the mugs.

END OF EXAMPLE
