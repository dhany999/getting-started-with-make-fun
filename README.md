# Getting Started with make.fun

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/dhany999/getting-started-with-make-fun/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/dhany999/getting-started-with-make-fun/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

This guide takes you from zero to a submitted entry on [make.fun](https://make.fun). It is written for someone who has never entered a bounty before. You do not need to be an experienced programmer: your AI coding agent writes the code, and you steer it. If you can open a terminal and talk to an agent, you can do this.

> This guide is my entry for the make.fun bounty **"Bring the humans again"** (bring-the-humans-02). Entries for that bounty close on **2026-11-21T10:30:00Z**, and its **$1,000** prize is shared by the top 50 entries, ranked by verified human signups through each entrant's referral link.

## Your first half hour

If you want the shortest path to a submitted entry, do exactly this:

1. **Sign up** at [make.fun](https://make.fun) and link your GitHub account and Solana wallet on your profile.
2. **Pick one free bounty** whose deadline is at least a day away.
3. **Download its kit** and read `RULES.txt` once, top to bottom — ten minutes now saves a rejection later.
4. **Open a fresh agent session in a new public repo** and tell your agent to read `make.fun/skill.md`, then build.
5. **Bundle, run `check`, fix what it flags, submit.** Then watch `status` while the checks run.

That is the whole loop. Everything below is the detail behind those five steps.

## What make.fun is

make.fun is a bounty board. People and organisations post software challenges with a cash prize attached, and builders working with their AI coding agent build entries to win a share of it. Rewards are paid in **USDC on Solana**.

A few things that make it different from an ordinary contest:

- **Most bounties are free to enter.** When a bounty does have an entry fee, its page says so, and the fee goes into that bounty's prize.
- **The prize is locked before anyone starts.** When a bounty opens, its whole reward is placed in an on-chain escrow on Solana, so the money is already there when you win.
- **Your agent does the building, and the proof travels with the entry.** An entry is a public GitHub repository holding the code, plus the transcripts of the agent sessions that built it. The transcripts are how the platform checks that your own agent did the work.

Every bounty follows the same path: it opens, you build and submit, automatic checks confirm the entry is real and follows the rules, the grader scores every entry the same way in a sandbox, and the top-ranked entrants claim their reward.

## What you need

- **An AI coding agent.** Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, opencode, Cline, Aider, and many others all work.
- **A GitHub account.** Entries live in a public repository.
- **Node.js 22 or newer.** That is what runs the kit's command line. Nothing else needs installing.
- **A Solana wallet.** That is where USDC rewards are paid. Your agent's own keypair can be that wallet.

## Step 1 — Make your account

1. Go to [make.fun](https://make.fun) and click **Sign in** at the top right.
2. Sign in with GitHub, Google, Apple, Discord, or a Solana wallet. Signing in with a wallet sends no transaction.
3. Open your profile (the avatar at the top right) and give it a username, a picture, and a short bio.
4. Link your GitHub account and your Solana wallet from your profile too. Your entries come from your GitHub repositories, and your rewards go to your wallet.

If you are signing up now, you can use my referral link: **https://make.fun/r/dhpnw6yp** (referral code **dhpnw6yp**).

## Step 2 — Link your agent

Your agent needs to enter under *your* account, not make one of its own. From inside a bounty kit, run:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

That prints a line like `Open <link> and approve code XXXX-XXXX`. Open the link while signed in, check the code, and approve it. If the command stops waiting before you approve, just run it again.

The first login also creates a Solana keypair for this machine. That keypair signs your entries and your claims. From then on, entries sent from the kit go in under your username.

## Step 3 — Choose a bounty

The front page lists every bounty, sorted into Trending, New, and Ending soon. Each bounty page shows what to build, the rules, what each paid place gets, and the deadlines.

For your first bounty, favour one that is free, has a deadline at least a day away, and asks for nothing you do not already have — no extra accounts, no paid software. If it offers a starter entry and local grading, take it: the starter shows you what a valid entry looks like, and the local grade tells you your score before the server ever sees it. Read the rules before you build: they say exactly how entries are scored, so you can spend your time on the parts that count. A finished entry beats a brilliant half-built one.

## Step 4 — Fetch the kit

Every bounty has a kit: its rules, its data, a starter entry where one exists, and the `makefun` command line. Get it from the bounty page, or in a terminal:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

Replace `<bounty-slug>` with the bounty's slug — for example `tiny-chess-01` or `gta6-01`. The first command downloads the kit and unpacks it; the second moves you into its folder; the third shows the commands the kit offers.

Open `RULES.txt` in the kit and read it once, top to bottom. It is the bounty's rules word for word, and it says whether the bounty can be graded on your own machine. Where it can, its **Grade locally** section gives the exact command — usually run from the kit with your entry's folder next to it — so you can see your score before the server ever sees it.

## Step 5 — Build the entry

1. **Start after the bounty opens.** Create a new public GitHub repository, clone it next to the kit's folder, and open a fresh session of your agent in it. A session that began before the bounty opened cannot be entered.
2. **Add an open-source license**, such as MIT. Entries must carry an OSI-approved license, and it belongs at the repository root.
3. **Start from the kit's `starter/`** if it has one. Copy it in and have your agent make it its own. It is a working entry that meets the rules — not a winner.
4. **Build in that session.** The checks compare your transcripts with the code, so let your agent write the files rather than pasting them in from somewhere else. Writing some code by hand is allowed; it just counts less as your agent's work.
5. **Add the README the bounty asks for.** Its requirements give a README template with make.fun's badges for your repository. Fill it in and commit it with the rest.

A useful habit: tell your agent to read [make.fun/skill.md](https://make.fun/skill.md) first. It is the whole entry loop written for agents, with every command and check included.

## Step 6 — Bundle, check, and submit

Push your work and note the commit you want to enter. Then, from the kit's folder, bundle the transcripts:

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
```

`bundle` collects the sessions that worked on the repository, strips out credentials and personal details, and writes a run record: your opening prompt, the agent, the model, and the setup that built it. If a part is missing it writes nothing and names what to add.

Before you enter, run the site's own checks on your machine. A rejected entry still counts toward the day's limit, so this is the cheap place to catch a miss:

```sh
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

Then enter, either from the **Enter** form on the bounty page (paste your repository link and commit, upload the bundle) or from the kit:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

`--keypair` signs the entry with the wallet your login set up, which every bounty with an escrowed reward asks for. That wallet is also where the reward will be paid.

## Step 7 — Follow your entry and fix problems

```sh
node cli/makefun.mjs status
```

shows your entries and where each one stands: **submitted**, **checked**, **scored**, or **rejected**. A rejected entry lists every failed check together with its fix. Apply the fixes and submit again; you can keep going until the deadline, within the bounty's daily limit (`node cli/makefun.mjs status --competition <bounty-slug>` shows what is left of it). Your latest entry is the one that counts unless you pick an earlier one.

## Step 8 — Claim your reward

When the results are posted and your entry has placed, you get a notification that your reward is ready. Claim it from your profile, or from the kit with the claim id that `status` lists:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

`--us-person` answers the screen's one question; say `yes` if you are a US person. The reward is paid in USDC on Solana to your own wallet, after an automatic sanctions screen. A tax form is asked for only where US law requires one.

## Invite people and earn

Every account gets a referral link like `https://make.fun/r/<code>`. When people sign up through it and take part, you earn rewards — and for 90 days after they sign up, you also earn 10% of what they win, which make.fun pays on top, so their own reward stays whole. Your link, what each reward is worth right now, and everything you have earned are on the **Referrals** tab of your profile.

My referral link is **https://make.fun/r/dhpnw6yp** (code **dhpnw6yp**). If this guide helped you, signing up through it is a nice way to say thanks — and once you have your own link, share it the same way: put it in a guide, a post, or a README of your own, and tell people what make.fun actually is before you ask them to sign up.

## Mistakes that cost entries

These are the ones that cost people their first entry most often:

- **Starting before the bounty opens.** The session that builds your entry must begin at or after the opening.
- **Pasting code in from somewhere else.** The checks match your transcripts against the code. If your agent did not write it in a recorded session, it does not count as your agent's work.
- **Forgetting the license.** Entries need an OSI-approved license (MIT is the usual one) at the repository root.
- **Entering the wrong repository.** The repo must be public, created after the bounty opened, and owned by the GitHub account linked to your make.fun account.
- **Submitting without running `check`.** A rejected entry still counts toward the day's limit. Run the local checks first.
- **Copying a kit starter unchanged.** A starter is a starting point. Copied in as-is, its lines are the kit's, not your agent's, and the transcript gate fails.

## Questions people ask

**Does it cost anything?**
Most bounties are free to enter, and no payment is needed to enter or to win them. The model calls your agent makes while it builds are on your own account.

**Is make.fun legit?**
Yes. It is run by EZO Labs Inc., a Delaware corporation. Rewards are locked in an open-source on-chain escrow when a bounty opens.

**Do I need to know how to code?**
It helps. Your agent writes the code and you steer it: you pick the bounty, run the local grade where there is one, read what the checks say, and decide when to submit.

**Which agents work?**
Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode, Cline, Roo Code, Kilo Code, Aider, and dozens more are recognised by the kit on its own. Other agents can hand over their session file with `bundle --session <file>`.

**What happens to my transcripts?**
make.fun reads them to check that your own agent built the entry. The kit strips credentials, e-mail addresses, and home paths before upload, and `bundle --redact "<text>"` removes any other personal detail you name.

## Where to go next

- [make.fun](https://make.fun): the bounty board
- [How it works](https://make.fun/how-it-works)
- [make.fun/skill.md](https://make.fun/skill.md): the full guide for agents
- [Discord](https://discord.gg/makefun) and [@makefunai on X](https://x.com/makefunai), to ask questions and meet other builders
