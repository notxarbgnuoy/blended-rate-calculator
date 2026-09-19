# Blended debt-rate calculator

Self-contained static calculator for comparing current consumer debt with two consolidation scenarios:

- Cash-out refinance
- HELOC

The tool lives in [`index.html`](./index.html) and has no build step or runtime dependencies, so it can be hosted directly on GitHub Pages, a CMS media bucket, or embedded in another website.

## Features

- Add, edit, and remove multiple consumer debts
- Enter balance, APR, monthly payment, and optional monthly interest override per debt
- Estimate:
  - total balance
  - total monthly payment
  - monthly interest expense
  - monthly principal reduction
  - current weighted blended APR
  - approximate payoff timing under current payments
- Compare current debts with:
  - a cash-out refinance
  - a HELOC using amortizing or interest-only payments
- “Keep paying the same total amount as before” mode for refinance and HELOC scenarios
- Optional existing mortgage inputs to show total secured blended rates after consolidation
- Built-in deterministic in-browser self-checks for the core math helpers
- Print / Save PDF support

## How the calculator works

### Current blended rate

The current blended APR is weighted by balance:

`Σ(balance × APR) ÷ Σ(balance)`

### Monthly interest

- Current debts use the optional monthly interest override when provided.
- Otherwise monthly interest is estimated as:

`balance × APR ÷ 12`

### Payoff timing

Payoff estimates are calculated month-by-month with safeguards for:

- zero-rate balances
- payments that do not cover monthly interest
- maximum iteration limits

Current portfolio payoff timing assumes each debt keeps its own payment schedule; freed-up payments are **not** snowballed into the remaining debts.

### Extra-payment comparison

For the refinance and HELOC comparison, “keep paying the same total amount as before” means:

- take the **current total monthly consumer-debt payment**
- use that amount as the payment on the new consolidated balance
- do **not** add it on top of the scenario’s scheduled payment

## Hosting / embedding

Because the calculator is a single static file, you can:

1. Upload `index.html` to any static web host
2. Serve it from the root of this repository with GitHub Pages
3. Copy the markup into an existing website template or iframe it from another page

## Usage

1. Open `index.html` in a browser
2. Replace the example debts with your real balances, rates, and payments
3. Optionally enter current monthly interest charges if they differ from a simple APR estimate
4. Adjust the refinance and HELOC assumptions
5. Review the side-by-side cards and comparison table

## Important disclaimer

This calculator is for educational estimation only. Actual rates, fees, taxes, escrows, payoff timing, promotional terms, closing costs, and HELOC variable-rate behavior can change. Verify all terms with a qualified lender or financial professional.
