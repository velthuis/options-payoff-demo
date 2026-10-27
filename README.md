# Option payoffs (a version an agent wrote earlier)

[![Open in GitHub Codespaces](https://github.com/codespaces/badge.svg)](https://codespaces.new/velthuis/options-payoff-demo)

MSF 8615 Derivatives, Fall 2026 · the backup app for the options class.

An agent built this payoff app from the class prompt. Its tests pass. **Is it right?**
Check it against your class table and the checklist in the worksheet before you trust it.

## Try it
1. Click **Open in GitHub Codespaces** above (or **Code → Codespaces → Create codespace on main**).
   The first build takes a few minutes and uses your free Codespace hours.
2. In the terminal:
   ```
   pip install -r requirements.txt
   pytest                  # the agent's tests
   streamlit run app.py    # the app
   ```
3. Run the **critic** agent on `payoff.py` in a new session, then compare its findings with your own.
4. On campus, Codespaces don't open (the network blocks their tunnels): use VS Code on your laptop.
   `docs/local-setup.md` has the steps.

Building it in Google Colab instead? `payoff_starter.ipynb` is the starting point:
[open it in Colab](https://colab.research.google.com/github/velthuis/options-payoff-demo/blob/main/payoff_starter.ipynb).

Your team's project does **not** start here: create it from the course template
(github.com/velthuis/derivatives-app-template → **Use this template**).

## Inputs and outputs
- Inputs: call or put, long or short, the strike `K`, the option price per share, and the number of
  contracts (100 shares each).
- Outputs: the payoff and profit per share across stock prices at expiration, as a chart, plus the
  break-even price and the maximum gain and loss for the position size you entered.

European option, at expiration only. Profit = payoff − premium for a long position; the short side
is the mirror image.

## Method
Per share, at expiration: a call pays `max(S − K, 0)`, a put pays `max(K − S, 0)`. Profit subtracts
the premium paid (long) or adds the premium received (short). Break-even is `K + premium` for a
call and `K − premium` for a put. One contract is 100 shares. Hull, Chapter 10.

## Data
No market data: every input is a scenario the user enters. The class example uses `K = 405` with a
call at \$17.65 and a put at \$20.

## Tests
Run `pytest`. The numbers come from the class table, not from the code:
- `tests/test_payoff.py`: the call and put examples from class (K = 405), the short side as the
  mirror image, and the break-even prices.
- `tests/test_pricing.py`: the template's Black-Scholes tests (Hull Chapter 15; put-call parity).

The agent skill in `.agents/skills/check-the-numbers/` tells coding agents how to add checks like these.

## Limitations
- Expiration only: no time value, no early exercise, no dividends, no interest on the premium.
- One option at a time; no spreads or combinations.
- The chart's price range is fixed at 350–460, around the class example's strike.

## Files in this repo
| File | Who uses it | What it is for |
|---|---|---|
| `README.md` | You | This page |
| `AI_LOG.md` | You | How you used AI, the critic's findings and your fixes, and examiner practice |
| `RUBRIC.md` | You read it | How the app is graded |
| `AGENTS.md` | The agent | Standing rules it reads every session |
| `PLAN.md` | The agent | Notes on the current task, so a new session can pick up where the last one stopped |
| `app.py`, `payoff.py`, `pricing.py`, `tests/` | Code | The page, the payoff formulas, the template's formulas, the checks |
| `payoff_starter.ipynb` | You | The Colab route, when Codespaces won't open |
| `docs/` | You, when needed | Guides: laptop setup, setting up your agent, how Streamlit works, git as a team |

To read a `.md` file with its formatting: on github.com, click it. In a Codespace, right-click it
and choose **Open Preview** (Ctrl+Shift+V).

## Working with agents
Set up the agent you want with `docs/agent-setup.md`: GitHub Copilot (free for students), Antigravity
CLI, Codex or Claude Code. All of them read `AGENTS.md`. Two review helpers live in `.github/agents/`:
- `critic`: adversarial review in a new session; cannot edit files; findings go in `AI_LOG.md`
- `examiner`: asks practice questions for the group demo and scores them against `RUBRIC.md`

## AI use
See `AI_LOG.md`. This whole app was written by an agent from the class prompt; the point of the
exercise is to check it.
