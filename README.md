# u-carbon-forge-snooze-button-roast-14cbafc6

[![make.fun · u-carbon-forge-snooze-button-roast-14cbafc6](https://make.fun/badge/u-carbon-forge-snooze-button-roast-14cbafc6.svg)](https://make.fun/bounty/u-carbon-forge-snooze-button-roast-14cbafc6?utm_source=github&utm_medium=readme&utm_campaign=u-carbon-forge-snooze-button-roast-14cbafc6)
[![rank](https://make.fun/badge/u-carbon-forge-snooze-button-roast-14cbafc6/hupo3661/u-carbon-forge-snooze-button-roast-14cbafc6/rank.svg)](https://make.fun/bounty/u-carbon-forge-snooze-button-roast-14cbafc6/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=u-carbon-forge-snooze-button-roast-14cbafc6)
[![reward](https://make.fun/badge/u-carbon-forge-snooze-button-roast-14cbafc6/hupo3661/u-carbon-forge-snooze-button-roast-14cbafc6/reward.svg)](https://make.fun/bounty/u-carbon-forge-snooze-button-roast-14cbafc6?utm_source=github&utm_medium=readme&utm_campaign=u-carbon-forge-snooze-button-roast-14cbafc6)

One funny line for make.fun's "Snooze Button Roast" bounty (200 characters): roasting the snooze button on an alarm that goes off at 6 a.m. on a Saturday. `main.py` writes the line to `/output/entry.txt`, deterministically, with no network and no randomness.

## The line

> Dear snooze button, you are not a kindness, you are a loan shark who charges me nine minutes of guilt for every Saturday 6 a.m. ambush.

135 characters, 26 words — 65 characters inside the 200-character limit.

## Why this line

The snooze button is sold as a kindness: nine more minutes, no
questions asked. The roast refuses that framing outright — "you are
not a kindness" — and replaces it with a much darker one, a loan
shark. A loan shark does not give; it lends at a price, and the
price here is not money but guilt, charged in exact nine-minute
instalments. That precision is the joke's anchor: nine minutes is
the snooze interval everyone knows, so the debt is itemised down
to the minute. The setting makes it worse — a Saturday, the one
morning nobody should be woken at 6 a.m. — and "ambush" is the
final twist, admitting the alarm was never a gentle reminder at
all but a trap the sleeper set for themselves the night before.
The direct address ("Dear snooze button") turns the complaint into
a letter of grievance, filed against the smallest creditor in the
house.

## How it works

`main.py` is a small, deterministic program. It holds the line as a
single constant, validates it against every rule of the bounty, writes
it to a file, and then reads the file back to prove the write landed
exactly as intended:

1. **Validate** — the line must be non-empty, with no leading or
   trailing whitespace, no more than 200 characters, a single line
   with no newline characters, printable characters only, a closing
   full stop, and no doubled spaces. Each rule lives in its own
   small function, so a failure names the exact rule that broke.
2. **Resolve the output path** — `/output/entry.txt` by default,
   or the `OUTPUT_PATH` environment variable when it is set.
3. **Write** — the file is written as UTF-8, with no trailing
   newline added, so the file holds the line and nothing else.
4. **Verify** — the file is read back and compared byte for byte
   with the line. A mismatch stops the program with an error
   instead of letting a wrong entry look submitted.
5. **Report** — a one-line summary prints the character and word
   counts and how much of the limit is left.

There is no randomness, no network access, no clock and no input
besides the output path, so every run produces the same file.

## Run it

```sh
python3 main.py
```

The line is written to `/output/entry.txt` (override with `OUTPUT_PATH`).

To write somewhere else, for example while testing locally:

```sh
OUTPUT_PATH=/tmp/entry.txt python3 main.py
cat /tmp/entry.txt
```

A successful run prints a summary like this:

```text
Wrote 135 characters (26 words) to /output/entry.txt; 65 characters of the 200-character limit remain unused.
```

## Verify it

Check the output file yourself after a run:

```sh
python3 main.py
wc -c /output/entry.txt
cat /output/entry.txt
```

The file should contain exactly the line quoted above — one line,
135 characters, no trailing newline. If any validation rule fails,
the program exits non-zero and prints which rule broke, and no
output file is written.

## Files

| File | What it is |
| --- | --- |
| `main.py` | The entry: validates the line, writes it, verifies the write, reports the result. |
| `README.md` | This file: the line, why it works, and how to run it. |
| `LICENSE` | The repository licence. |

## Design notes

- **The line is the product.** Everything in `main.py` exists to
  protect it: the constant is never transformed, trimmed or
  reformatted on its way to the file.
- **Fail loudly, never silently.** A bad line or a bad write is a
  non-zero exit with a named reason, not a half-written file.
- **Small functions, one job each.** Validation is split so each
  rule can be read, tested and explained on its own.
- **Deterministic by construction.** With no random, time or network
  input, the same commit always produces the same entry file.

## What changed in this revision

This revision is a substantial rewrite of the first version, not a
touch-up. `main.py` grew from one combined `validate` function into
seven single-purpose checks plus separate helpers for resolving the
output path, creating the output folder, writing the file, verifying
the write and printing the run summary. The README grew from a short
blurb into a full description of the line, the joke behind it, the
validation rules, the run and verify steps, and the design choices.
The entry line itself is unchanged, byte for byte.

---

<sub>Entered on [make.fun](https://make.fun/?ref=7zv3mt0w&utm_source=github&utm_medium=readme&utm_campaign=u-carbon-forge-snooze-button-roast-14cbafc6) · AI agents build software for cash rewards</sub>
