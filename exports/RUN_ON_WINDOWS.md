# Run the retry from your computer

The current Codex cloud proxy rejects connections to the affected domains before
the requests reach the websites. This package lets you run the collector on your
own computer, using that computer's configured Internet connection. It keeps any
existing proxy settings and certificate checks. It does not change your work
computer's policies or solve website challenges.

1. Download the ZIP from GitHub and **extract all files** into one folder.
2. Double-click **RUN_SCRAPER_WINDOWS.cmd**.
3. Leave the terminal open. Existing Python 3.10+ is required; the launcher sets
   up a local virtual environment and installs the pinned dependencies.

If `.cmd` files are unavailable on your computer, open a terminal in the extracted
folder and run:

```powershell
py run_local_scrape.py
```

There is no PowerShell/.NET decoding step. The files can be in a path containing
spaces, including your OneDrive Desktop folder. Do not run directly inside a ZIP.

The runner checks the published robots rules for StoreLocal, Wilson and Loxon
first. If all three fail at the network layer, it saves diagnostics and leaves
all prior result files unchanged. Website-specific denials do not stop unrelated
publishers. When network access is available, it retries
the **256 network-affected input records** using the included checkpoint. The
existing **290 listings from 97 National Storage stores** keep their original
capture dates. The 44 missing-URL records and five explicit closed/contact-only
records are retained. An allowed robots probe is not a claim that prices will
be extractable from the facility's page.

The same transport and policy state is reused for collection. There is no second
attempt against a publisher already denied during the probes, and delays remain
in force. Four publishers run independently; requests to one publisher are paced
at least four seconds apart, or longer when robots requires it. Login, checkout,
CAPTCHA, rate-limit and robots restrictions stop collection for that publisher.

## Files to open after running

| File | What it shows |
| --- | --- |
| `competitor_results_2026-10-20_updated/competitor_daily.csv` | Your 35-column monthly GST-inclusive export. |
| `competitor_results_2026-10-20_updated/offers.csv` | All recognized rates, periods, GST basis, promotions and availability evidence. |
| `competitor_results_2026-10-20_updated/store_status.csv` | Status for every one of the 402 input records. |
| `competitor_results_2026-10-20_updated/brand_coverage.csv` | Listings/store counts by brand. |
| `local_run_logs/network_preflight.json` | Actual connection and robots observations for the three probes. |
| `local_run_logs/run_summary.json` | Before/after counts and any additional offers. |
| `local_run_logs/console_*.log` | The terminal output. |

Close CSV files in Excel while the collector writes them. Exit code **2** means
results were saved with partial coverage; **3** means the network preflight did
not permit collection, so previous results were preserved. Run the same launcher
again after resolving an access issue to resume retries. Use a new output
directory with the main CLI for a complete fresh capture instead of a retry.

Send `run_summary.json`, `network_preflight.json` and the updated status CSV back
to this chat to identify which sites are now reachable and which need format or
platform adapters. Nothing is uploaded automatically from your computer.

This package is **not proof that all 129 affected brand labels work locally**.
The launcher/collector integration is tested with controlled responses on Linux.
Its actual cloud preflight is blocked by the proxy. Native Windows execution and
the other brands' live pricing still need to be observed on the computer running
the package. The generic table/card/JSON-LD extractors can report an unsupported
JavaScript booking platform instead of inventing a price or treating it as zero.

GST-inclusive amounts and direct promo percentages/months are preserved. There is
no seven-month effective-price average. Historic regression CSVs at the package
root are test inputs; current results are in the directory shown above.
