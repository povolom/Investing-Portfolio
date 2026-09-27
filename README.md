# Portfolio Lab

A local investing portfolio tracker built with Python, SQLite and browser JavaScript. Add or edit manual CAD holdings; inspect cost basis, position value, unrealized gain/loss and allocation; export a JSON snapshot. No accounts, API keys or packages are required.

## Run on a Mac

Requires Python 3.9 or newer. From this directory:

```sh
python3 portfolio.py
```

Open **http://127.0.0.1:8787**. Stop with Control-C. If the port is occupied, use `python3 portfolio.py --port 8788` and open that port instead.

Data persists at `~/Library/Application Support/Investing-Portfolio/portfolio.sqlite3`, outside this repository. To back up all data, stop the app and copy that file. Restore by stopping the app and replacing the database with your backup. JSON export is a readable snapshot; an import feature is not implemented. For a disposable demo use `python3 portfolio.py --db /tmp/portfolio-demo.sqlite3`.

```sh
python3 -m unittest -v
```

## Model and limits

Each symbol represents one aggregated position. Saving the same symbol replaces its shares, average cost and current manual price. Changing a symbol creates a new position; remove the old one if renaming. All values must already be in CAD. Last saved time is UTC and records editing, not a quote timestamp. Values use decimal arithmetic and are rounded to cents for display. Allocation percentages may sum to 99.99 or 100.01 after rounding.

- Cost = shares × average cost; value = shares × manual price.
- Unrealized gain/loss = value − cost; allocation = position value ÷ total value.
- No live prices, trades, cash, fees, dividends, realized gains, tax calculations, FX conversion or historical returns. Displayed gain is not total investment performance.

Only this Mac can connect by default. Host and Origin checks reject other website origins and unexpected hosts. This is a personal development app, not a multi-user hosted service. Source is maintained in the private GitHub repository https://github.com/povolom/Investing-Portfolio. No public deployment has been created.

## First learning checkpoint

Three concepts: **Decimal** avoids binary floating-point surprises in financial arithmetic; **SQLite** persists rows after restarting; **same-origin requests** constrain browser writes to this app.

Tiny task: enter a fictional `EXAMPLE` holding with 2.5 shares, CAD 10 average cost and CAD 12 price. Predict cost, value and gain before saving. Then lower the price to CAD 8 and explain what changes.

Next manageable improvements: price timestamps and stale-price badges; CSV import with preview and duplicate handling; an allocation chart with accessible text. Build these one at a time, review and test each, then use only completed work as portfolio evidence.
