# Financial Tracking System

AI-first financial tracking for your operations.

## Quick Start

Ask Claude:
- "What's our profit this month?"
- "Log invoice: [Client] $X for [description]"
- "Update dashboard"
- "How much do we owe contractors?"
- "What's outstanding?"

## Files

| File | Purpose |
|------|---------|
| [revenue.md](revenue.md) | All invoices and payments |
| [expenses.md](expenses.md) | All costs and expenses |
| [contractors.md](contractors.md) | Contractor rates and hours |
| [subscriptions.md](subscriptions.md) | Recurring software/service costs |
| [reports/](reports/) | Monthly and annual reports |

## AI Instructions

### Logging Revenue

When a new invoice is created or payment received:
1. Add row to `revenue.md` in appropriate year section
2. Update status (PAID/OUTSTANDING/PENDING)
3. Link to invoice PDF in `invoices/` folder if available
4. Update `README.md` dashboard

### Logging Expenses

When a cost is incurred:
1. Add row to `expenses.md` with correct category
2. For contractor payments, reference hours from `contractors.md`
3. Update dashboard as needed

### Calculating Profit

```
Profit = Sum(revenue.md WHERE status=PAID AND date in range)
       - Sum(expenses.md WHERE date in range)
```

### Generating Reports

Monthly reports should include:
- Revenue breakdown by client
- Expense breakdown by category
- Profit/loss
- Outstanding receivables
- Key metrics changes

Save to `reports/YYYY-MM.md`

## Data Format Rules

- Dates: YYYY-MM-DD format
- Amounts: $X,XXX format with dollar sign
- Status: PAID | OUTSTANDING | PENDING (all caps)
- Client names: Must match `projects/clients/` folder names

## Audit Trail

All changes to financial files should be committed with descriptive messages:
- "Log invoice: Client $10K Phase 1"
- "Mark paid: Client Invoice #4"
- "Add expense: Software subscription $20"
