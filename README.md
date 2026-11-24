<p align="center"><b>English</b> · <a href="README.de.md">Deutsch</a></p>

# 🌙 Toddler Sleep Coach

**An AI skill that plans your toddler's nap and bedtime, and then checks its own homework.**

You text it the times. It tells you when to start the bedtime routine, logs the day, and the next evening it checks whether yesterday's forecast was right. After a few weeks it knows *your* child, not an age chart.

[![License: MIT](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
![Works with Claude](https://img.shields.io/badge/Claude-skill-d97757)
![Works with ChatGPT](https://img.shields.io/badge/ChatGPT-project-10a37f)
![Works with Codex](https://img.shields.io/badge/Codex-skill-black)
![Ages](https://img.shields.io/badge/ages-12%20months%E2%80%936%20years-brightgreen)
![Safety](https://img.shields.io/badge/never%20diagnoses-orange)

---

## What it looks like

> **You:** Up at 7:10, nap in the car 12:04–12:42
>
> **Coach:** Short car nap (38 min), so today starts the bedtime routine earlier. Watch for tiredness from about 18:30 and plan sleep onset for 19:00–20:00, ideally 19:30. If she already looks exhausted, go earlier. Travel exception, not a new rule. Logged.
>
> **You:** asleep 19:41
>
> **Coach:** Logged. Last wake window 6:59 h. Forecast 19:00–20:00 → hit (11 min after the preferred time). 4 of the last 5 forecasts were inside the window.

No app, no subscription, no account. It runs inside the AI you already use.

## Why it is different

| Typical sleep apps | Toddler Sleep Coach |
|---|---|
| Age-based wake windows for every child | Starts with rough age ranges, then switches to **your child's own** median and quartiles after 5 good days |
| A prediction, and you never know if it was right | **Grades every forecast** against the actual sleep onset and reports its hit rate |
| One bad night → "too much nap!" | Refuses to call single evenings a cause. Says "not resolved" when it isn't |
| Pushes for the earliest possible bedtime | **Sleep need before clock time.** No routine nap capping just to hit 20:00 |
| Your data on someone's server | Your log lives where *you* choose: a Notion page, Google Doc, ChatGPT page or a CSV |
| Sick day = a broken streak | Sick, travel and car-nap days are flagged and kept out of the normal statistics |

## Install (2 minutes)

Download the ZIP from the [latest release](https://github.com/chris2k20/toddler-sleep-coach/releases/latest): `toddler-sleep-coach.zip` (English) or `kinder-schlafcoach.zip` (German).

**Claude (claude.ai or desktop app)**
Settings → Capabilities → Skills → upload the ZIP. Then start a chat in a project: *"Sleep coach: create a profile for my daughter, 26 months, goal asleep by 20:15."*

**Claude Code / Codex**
```bash
git clone https://github.com/chris2k20/toddler-sleep-coach.git
cp -R toddler-sleep-coach/skills/toddler-sleep-coach ~/.claude/skills/   # Claude Code
cp -R toddler-sleep-coach/skills/toddler-sleep-coach ~/.codex/skills/    # Codex
```

**ChatGPT**
Create a project, paste [`SKILL.md`](skills/toddler-sleep-coach/SKILL.md) into the project instructions and upload the files from [`references/`](skills/toddler-sleep-coach/references) as project files.

## How it learns (honestly)

The skill file never changes itself. What learns is **the log**:

1. Every message with times becomes a row (corrections replace, nothing is filled in).
2. Every evening the forecast is compared with reality: inside the window or how many minutes off.
3. Every 5 usable day-night pairs it recomputes the wake windows (median, 25th/75th percentile), separately for normal and special days.
4. Rules only change with evidence, versioned, with counterexamples. You can see why.

Want the full picture? [`data-model.md`](skills/toddler-sleep-coach/references/data-model.md) and an [example week](examples/example-week.csv).

## Safety first

This is a planning helper, **not a medical device** and not a replacement for your pediatrician.

- With fever, infection or persistent cough it switches to rest mode and stops optimising.
- Breathing difficulty, blue lips or a child that is hard to wake → it tells you to call your local emergency number, immediately.
- Under 12 months it only logs. No wake-window forecasts for babies.
- Wake-window rules of thumb are labelled as such. The only cited numbers are the [AASM total-sleep ranges](skills/toddler-sleep-coach/references/age-orientation.md).

## Privacy

Nickname instead of name, birth month instead of birth date, no addresses, no medical side details. The skill never shares or exports anything unless you ask. One profile per child, siblings are never mixed.

## FAQ

**Does it work for babies?** Only as a log. Under 12 months sleep is driven by feeding and development, and safe-sleep guidance belongs to your midwife or pediatrician.

**Does it need a sleep tracker or camera?** No. Times you type (or dictate) are enough.

**Several children?** Yes, one profile and one log per child.

**Will it make my child sleep through the night?** No promises. It helps you time naps and bedtime well and shows you what actually works for your child.

## Contributing

Ideas, translations and real-world feedback are welcome. Open an issue, especially if a forecast was way off: that is exactly what the learning loop needs. Please never post real child data in issues.

## License

[MIT](LICENSE). Not medical advice.
