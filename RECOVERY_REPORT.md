# Conflict Recovery Report

## What was broken
- `main` carried raw conflict markers in `checkout.js` from commits `e02e673` and `981e441`.
- Commit `3c0947a` duplicated the rounding fix already present on `bugfix/rounding` (`4a6171c`).
- `feature/tax-v2` (`cba4ecb`) drifted and was never synced with `main`.

## Recovery actions
- Reverted `e02e673` (bad commit on shared main) instead of resetting, to keep history traceable.
- Merged `feature/tax-v2` and resolved `checkout.js` by combining rounding + tax.
- Cherry-picked the discount change from `feature/discounts` and resolved it onto the combined logic.

## Result
`checkout.js` now applies discount -> tax -> rounding and `test.js` validates $10.00 -> $9.45.
