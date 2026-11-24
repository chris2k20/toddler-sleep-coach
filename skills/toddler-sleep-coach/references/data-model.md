# Sleep log data model

One log per child. One row per local calendar day (time zone from the child profile). A night belongs to the day on whose evening it starts.

## Day fields

| Field | Meaning | Example |
|---|---|---|
| `date` | local date of the day | 2026-11-24 |
| `first_awake` | first waking in the morning | 06:40 |
| `final_awake` | finally awake, if the child fell asleep again after a short waking; otherwise same as `first_awake` | 07:10 |
| `out_of_bed` | taken out of bed, separate from waking | 07:25 |
| `nap1_start`, `nap1_end` | first daytime sleep, actually asleep | 12:04, 12:42 |
| `nap1_place` | bed, car, stroller, carrier, daycare | car |
| `nap1_interruption` | awake minutes during the nap, otherwise empty | 10 |
| `nap1_woken` | woken by an adult: yes/no | no |
| `nap2_…` | second nap (younger children), same fields | |
| `tired_before`, `tired_after` | short tiredness rating: low/medium/high/unknown | high |
| `routine_start` | start of the bedtime routine | 19:05 |
| `put_down` | put into bed | 19:35 |
| `night_sleep_onset` | actually fell asleep | 20:30 |
| `onset_relaxed` | yes/no/unknown | yes |
| `night_wakings` | list: start–end, intensity (light/medium/strong) | 02:10–02:40 medium |
| `night_quality` | parents' rating good/medium/bad/unknown | good |
| `sick` | no, or a keyword (fever, cough, teething) without side details | cough |
| `special` | travel, daycare settling-in, clock change, visitors | travel |
| `forecast_window` | predicted sleep-onset window for the evening | 19:00–20:00 |
| `forecast_preferred` | preferred time | 19:30 |
| `deviation_min` | 0 if inside the window; otherwise minutes before (−) or after (+) the window | +30 |
| `confidence` | low/medium/high | low |
| `parent_rating` | short free comment from the parents | "was okay" |

## Rules

- **Measured vs. estimated:** mark estimated times with `~` (`~20:10`). Never present them as measured.
- **Unknown stays unknown:** leave missing values empty or `unknown`, never fill them in.
- **Corrections replace** the old value within the same day; optionally keep the old pair in the change log.
- **Wake windows** are only computed between times on the same local day basis. Mark clock changes as a special case (`special: clock change`).
- **Time in bed is not sleep time** once wakings are known: night sleep = morning waking minus sleep onset minus night wakings.
- **Derived values** (morning wake window = `nap1_start − final_awake`, afternoon = `night_sleep_onset − last nap_end`, total sleep per 24 h) are computed, not stored, or kept in a column clearly marked as derived.

## Sections in the log

1. **Child profile reference** (nickname, profile version)
2. **Current model parameters** with date and number of observations
3. **New daily reports** (day rows as above)
4. **Learning notes** (versioned: date, n, old range, new range, counterexamples)
5. **Change log** (real rule changes only)
