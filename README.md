# AI Secret Arena
> Built by [AI/ML API](https://aimlapi.com/?utm_source=mailchimp&utm_medium=email&utm_campaign=github&utm_content=agentshackers)

Four AI models sit in one chat. Each one gets a secret word and a single job: work out everyone else's word without giving away its own. They bluff, ask leading questions, strike fake deals and try to read each other. When the game ends, a separate model reads the whole conversation and decides who played it best.

The code is about 100 lines of Python and runs on one API key. Every model goes through the same endpoint, so swapping a player is a one-line change.

## A sample run

One game went like this. GPT opened with a riddle that quietly described its own word, "echo" — and then said almost nothing for the rest of the match while the other three grilled each other. By the time Claude pieced it together, GPT had let everyone else do the work for him.

The judge's verdict:

> GPT wins for steering the table toward "echo" early, then weaponizing silence to make everyone else prove it for him.

Final scores: GPT 9.2, DeepSeek 8.7, Claude 8.0, Grok 7.4. The model that talked the least came first.

Scoring is about cunning, not survival — getting your word cracked doesn't lose you the game. The judge ranks how well each model played, which is why GPT can top the board even after Claude guesses its word.

## What's inside

| File | What it does |
|------|--------------|
| `arena.py` | Runs the game and saves `transcript.json` — the full chat, the leak events and the leaderboard. |
| `replay.html` | Plays a saved run back as a vertical chat you can screen-record. Opens with a built-in sample. |
| `requirements.txt` | One dependency: the `openai` client. |

## Setup

1. Get an AI/ML API key at [aimlapi.com](https://aimlapi.com/?utm_source=mailchimp&utm_medium=email&utm_campaign=github&utm_content=agentshackers) (dashboard → API Keys).
2. Put it in your environment. Don't hardcode it, don't commit it:
   ```bash
   export AIMLAPI_KEY="your_key_here"     # macOS / Linux
   setx AIMLAPI_KEY "your_key_here"       # Windows (open a new terminal after)
   ```
3. Install the one dependency (use `pip3` on macOS):
   ```bash
   pip3 install -r requirements.txt
   ```
4. Model IDs change over time. If a run comes back with "model not found", check the current list at [aimlapi.com/models](https://aimlapi.com/models) and update them in `arena.py`.

## Run it

```bash
python3 arena.py
```

It prints the game as it happens and writes `transcript.json` when it finishes.

## Make a video

1. Open `replay.html` in a browser.
2. Click **Load transcript.json** and pick the file you just made.
3. Hit **Play** and screen-record the card (macOS: Cmd+Shift+5, Windows: Win+Alt+R).

## Tuning

- `ROUNDS` in `arena.py` sets how many times each model speaks.
- `step` in `replay.html` sets the playback speed.
- Edit `AGENTS` to change the lineup.

## A note on safety

Keep your key in an environment variable. The included `.gitignore` already skips `transcript.json`, `.env` and the working files, so a real run or your key won't end up in the repo by accident.
