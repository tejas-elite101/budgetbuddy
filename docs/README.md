# BudgetBuddy product guide

A small spending and allowance tracker for keeping track of a saved account
and its transactions in the terminal.

## Team

- Tejas Elluri (solo founder, building BudgetBuddy)

## Run and test

Use Python 3 from the repository root. No dependency installation is required.

```bash
python3 main.py
python3 -m unittest
```

The starter data is in `data/budgetbuddy.json`. Adding a transaction saves
that file; use a backup if you want to preserve the sample data.

## Terminal menu

| Option | Action |
|---|---|
| 1 | Show the current balance |
| 2 | List transactions |
| 3 | Add a transaction |
| 4 | Filter transactions by category |
| 5 | Show the last transaction |
| 6 | Count transactions in each category |
| 7 | Show total spending and the average signed transaction amount |
| 8 | Show an account summary |
| 0 | Quit |

Expenses have negative amounts; income has positive amounts. Category
matching is exact and case-sensitive. The last-transaction menu action
expects at least one transaction.

## Big-expense warnings

`features.core.big_expenses(transactions, threshold)` returns expenses whose
positive spending amount meets the threshold, excluding income. The
threshold must be positive; zero or negative values raise `ValueError`.
No qualifying expenses, including an empty list, produce `[]`.

Task: [ticket-01](../tickets/ticket-01-big-expenses.md).

## Category dollar totals

`features.reports.category_report(data)` returns `{category: signed_total}`.
Every transaction contributes once. Refunds and income retain their signs;
an empty account returns `{}`. This differs from menu option 6, which counts
transactions rather than summing amounts.

Task: [ticket-02](../tickets/ticket-02-category-report.md).

## Average balance history

`features.reports.average_balance(data)` averages the numbers in
`data["history"]` and rounds to one decimal place. An empty history returns
`0.0`. This is the provided Lesson 12 report helper, now covered by tests.
The saved history is not automatically extended when adding a transaction.

## Try the helpers

From the repository root:

```bash
python3 -c 'import storage; from features import core; print(core.big_expenses(storage.load_data()["transactions"], 10))'
python3 -c 'import storage; from features import reports; print(reports.category_report(storage.load_data()))'
python3 -c 'import storage; from features import reports; print(reports.average_balance(storage.load_data()))'
```

With the sample data, the warning helper finds the $12 movie ticket,
category totals are transport -2.5, income 35.0, food -10.0, and fun -12.0,
and average history is 51.7. These helpers are not new menu options.

## Solo demo plan

Tejas Elluri records the screen and narrates one take of about a minute:

1. First 10 seconds: introduce BudgetBuddy and its spending-tracking purpose.
2. Next 20 seconds: run the app and show balance and spending summary.
3. Next 15 seconds: run the big-expense helper to find the $12 movie ticket.
4. Next 10 seconds: explain the signed-amount/threshold edge case and show
   that the unit tests pass.
5. Final 5 seconds: name a next step, such as connecting the new report
   helpers to menu options, and one lesson from testing empty inputs.

This is a recording plan; no recording or upload is included in the repo.
