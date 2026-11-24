---
name: founder-pricing
description: Analyze survey/panel price sensitivity, competitors and margins to propose price tests; do not change actual prices automatically.
argument-hint: "[current price]"
---

# Founder pricing

1. Use real survey answers first, otherwise existing `founder/panel/answers`. Reuse comparable prices and source dates from `founder/competitors.csv` and context from `founder/competitors.md` when present. Read `founder/numbers.json` and the approved pitch/price. Keep currency, quantity, tax and billing period comparable. established prices stay unchanged without the user’s decision.
2. At least five valid responses are needed. CSV input columns: `too_cheap,cheap,expensive,too_expensive`. If data are absent, state that no sensitivity range is known; a simulated panel is an optional test-design aid, not a required next step.
3. Run (replace CURRENT_PRICE with the actual comparable price):
```bash
python3 "~/.claude/skills/founder-pricing/van_westendorp.py" founder/panel/answers --price CURRENT_PRICE --out founder/pricing-curve.md
```
Use the CSV path instead when surveys are supplied. Read PMC/PME (acceptable range), OPP (least resistance) and IPP (bargain/expensive intersection); small/simulated samples are weak evidence.
4. Check 2–3 candidate prices against margins and break-even without editing actual inputs:
```bash
python3 "~/.claude/skills/founder-cfo/unit_economics.py" founder/numbers.json --price CANDIDATE_PRICE
```
Flag prices below variable cost and the cost/time of any loss. Never invent a prior price, discount or willingness-to-pay result.
5. Write `founder/pricing.md`: recommended test price/reason, supported price ladder/offer if relevant, two real-buyer tests, key objections and evidence gaps. Keep candidates as what-ifs until adopted. Only after explicit adoption update the corresponding input and rerun founder-cfo.

Done: curve, price tests and financial outputs agree on inputs/currency. Simulation proposes what to test; it does not prove demand. No public price or offer changes occur from producing this analysis.
