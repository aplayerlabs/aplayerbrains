# Getting Started

This guide assumes you've never used a terminal before. That's fine. You'll be up and running in 10 minutes.

## Step 1: Get Claude Code

A Player Brains runs inside Claude Code, an AI tool made by Anthropic.

### Option A: Desktop app (easiest)

1. Go to [claude.ai/code](https://claude.ai/code)
2. Download the desktop app for your computer (Mac or Windows)
3. Install it like any other app
4. Open it. You'll see a text input where you can type.

### Option B: Terminal

1. Open Terminal (Mac: search "Terminal" in Spotlight) or Command Prompt (Windows: search "cmd")
2. Paste this and press Enter:
   ```
   npm install -g @anthropic-ai/claude-code
   ```
3. If that doesn't work, you may need to install Node.js first: go to [nodejs.org](https://nodejs.org), download and install it, then try again.

## Step 2: Subscribe to Claude

Claude Code requires a subscription. You'll need one of:

- **Claude Max** ($100/month) — recommended. Includes generous usage.
- **Claude API** — pay-per-use. More technical to set up.

Sign up at [claude.ai](https://claude.ai) if you haven't already.

## Step 3: Install A Player Brains

Open Claude Code (the desktop app or terminal) and type:

```
! git clone https://github.com/aplayerlabs/aplayerbrains.git ~/.claude/skills/aplayerbrains && cd ~/.claude/skills/aplayerbrains && ./setup
```

The `!` at the start tells Claude Code to run this as a system command. It downloads A Player Brains and sets everything up.

You should see a confirmation that the brains are installed.

## Step 4: Start your first project

Type:

```
/aplayerbrains
```

That's it. The brain will ask you about your problem or idea and guide you from there.

## What you'll need along the way

The pipeline will ask you to set up a few things at the right time:

- **GitHub account** (free) — where your code lives. /setup will walk you through this.
- **Render account** (free tier available) — where your app runs. /setup will walk you through this.
- **A domain name** (optional) — if you want a custom URL. /setup will cover this too.

You don't need any of these right now. /setup handles it when the time comes.

## Key commands

| Command | What it does |
|---------|-------------|
| `/aplayerbrains` | Start here. Routes you to the right brain. |
| `/wrap` | Pause your session. Pick up later exactly where you left off. |
| `/status` | See where you are in the pipeline and what's next. |
| `/upgrade` | Get the latest brains and improvements. |

## The pipeline

Your project will move through these brains in order:

1. **/discover** — Find the real problem
2. **/plan** — Stress-test the direction
3. **/setup** — Set up GitHub and hosting
4. **/define** — Write the product requirements
5. **/design** — See what the app will look like
6. **/build** — Build it (multiple sessions)
7. **/test** — Break it on purpose
8. **/launch** — Go live

You don't need to memorize these. `/aplayerbrains` always knows where you are and what's next.

## Tips

- **You can stop anytime.** Type `/wrap` and your progress is saved. Come back tomorrow, next week, whenever.
- **Plain English.** Check STATUS.md in your project folder to see where things stand. It's written for you, not for programmers.
- **Ask questions.** Every brain is conversational. If something doesn't make sense, say so. The brain will explain.
- **Trust the order.** The pipeline exists so you don't skip steps. Each brain builds on what the previous one produced.

## Need help?

- [YouTube series](#) — watch the whole pipeline in action
- [GitHub Issues](https://github.com/aplayerlabs/aplayerbrains/issues) — report bugs or ask questions
- [A Player Labs](https://aplayerlabs.com) — the team behind A Player Brains
