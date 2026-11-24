<p align="center"><a href="README.md">English</a> · <b>Deutsch</b></p>

# 🌙 Kinder-Schlafcoach

**Ein KI-Skill, der Mittagsschlaf und Schlafenszeit deines Kleinkinds plant und danach seine eigenen Hausaufgaben kontrolliert.**

Du schickst die Uhrzeiten. Er sagt dir, wann die Abendroutine losgehen sollte, trägt den Tag ins Protokoll ein und prüft am nächsten Abend, ob die Prognose von gestern gestimmt hat. Nach ein paar Wochen kennt er *dein* Kind und nicht nur eine Alterstabelle.

[![License: MIT](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
![Claude](https://img.shields.io/badge/Claude-Skill-d97757)
![ChatGPT](https://img.shields.io/badge/ChatGPT-Projekt-10a37f)
![Codex](https://img.shields.io/badge/Codex-Skill-black)
![Alter](https://img.shields.io/badge/Alter-12%20Monate%E2%80%936%20Jahre-brightgreen)
![Sicherheit](https://img.shields.io/badge/stellt%20keine%20Diagnosen-orange)

---

## So sieht das aus

> **Du:** 7:10 wach, Mittagsschlaf im Auto 12:04–12:42
>
> **Coach:** Kurzer Autoschlaf (38 Min.), also heute früher mit der Abendroutine anfangen. Ab etwa 18:30 auf Müdigkeit achten, Einschlafen grob 19:00–20:00 planen, bevorzugt 19:30. Wirkt sie schon erschöpft, früher. Reise-Sonderfall, keine neue Regel. Notiert.
>
> **Du:** 19:41 eingeschlafen
>
> **Coach:** Notiert. Letztes Wachfenster 6:59 h. Prognose 19:00–20:00 → getroffen (11 Min. nach der bevorzugten Zeit). 4 der letzten 5 Prognosen lagen im Fenster.

Keine App, kein Abo, kein Konto. Er läuft in der KI, die du ohnehin nutzt.

## Was anders ist

| Übliche Schlaf-Apps | Kinder-Schlafcoach |
|---|---|
| Wachfenster nach Alter, für jedes Kind gleich | Startet mit groben Altersspannen, wechselt nach 5 guten Tagen auf Median und Quartile **deines Kindes** |
| Eine Vorhersage, ob sie stimmte, erfährst du nie | **Bewertet jede Prognose** gegen das tatsächliche Einschlafen und nennt seine Trefferquote |
| Eine schlechte Nacht → „zu viel Mittagsschlaf!“ | Erklärt einzelne Abende nicht zur Ursache. Schreibt „nicht geklärt“, wenn es nicht geklärt ist |
| Drängt auf möglichst frühes Zubettgehen | **Schlafbedarf vor Uhrzeit.** Kein regelmäßiges Kappen des Mittagsschlafs für 20:00 Uhr |
| Deine Daten auf fremden Servern | Dein Protokoll liegt, wo *du* willst: Notion, Google Doc, ChatGPT-Page oder CSV |
| Kranktag = kaputte Statistik | Krankheit, Reise und Autoschlaf werden markiert und aus der Normalstatistik herausgehalten |

## Installation (2 Minuten)

ZIP aus dem [neuesten Release](../../releases/latest) laden: `kinder-schlafcoach.zip` (Deutsch) oder `toddler-sleep-coach.zip` (Englisch).

**Claude (claude.ai oder Desktop-App)**
Einstellungen → Funktionen → Skills → ZIP hochladen. Dann in einem Projekt: *„Schlafcoach: leg ein Profil für meine Tochter an, 26 Monate, Ziel eingeschlafen bis 20:15.“*

**Claude Code / Codex**
```bash
git clone https://github.com/chris2k20/toddler-sleep-coach.git
cp -R toddler-sleep-coach/skills/kinder-schlafcoach ~/.claude/skills/   # Claude Code
cp -R toddler-sleep-coach/skills/kinder-schlafcoach ~/.codex/skills/    # Codex
```

**ChatGPT**
Projekt anlegen, [`SKILL.md`](skills/kinder-schlafcoach/SKILL.md) in die Projektanweisungen kopieren und die Dateien aus [`references/`](skills/kinder-schlafcoach/references) als Projektdateien hochladen.

## Wie er lernt (ehrlich)

Die Skill-Datei ändert sich nie von selbst. Was lernt, ist **das Protokoll**:

1. Jede Nachricht mit Uhrzeiten wird eine Zeile (Korrekturen ersetzen, nichts wird aufgefüllt).
2. Jeden Abend wird die Prognose mit der Wirklichkeit verglichen: im Fenster oder wie viele Minuten daneben.
3. Alle 5 auswertbaren Tag-Nacht-Paare rechnet er die Wachfenster neu (Median, 25./75. Perzentil), getrennt nach Normal- und Sondertagen.
4. Regeln ändern sich nur mit Belegen, versioniert und mit Gegenbeispielen. Du siehst, warum.

Mehr dazu: [`datenmodell.md`](skills/kinder-schlafcoach/references/datenmodell.md) und eine [Beispielwoche](examples/example-week.csv).

## Sicherheit zuerst

Ein Planungshelfer, **kein Medizinprodukt** und kein Ersatz für die Kinderärztin oder den Kinderarzt.

- Bei Fieber, Infekt oder anhaltendem Husten schaltet er auf Erholung und hört auf zu optimieren.
- Atemnot, blaue Lippen oder ein kaum weckbares Kind → er sagt dir, sofort 112 zu rufen.
- Unter 12 Monaten nur Protokoll, keine Wachfenster-Prognosen für Babys.
- Faustwerte für Wachfenster sind als solche gekennzeichnet. Belegt zitiert werden nur die [AASM-Spannen zum Gesamtschlaf](skills/kinder-schlafcoach/references/altersorientierung.md).

## Datenschutz

Rufname statt Name, Geburtsmonat statt Geburtsdatum, keine Adressen, keine medizinischen Nebendetails. Der Skill teilt und exportiert nichts ungefragt. Ein Profil je Kind, Geschwister werden nie vermischt.

## FAQ

**Geht das auch für Babys?** Nur als Protokoll. Unter 12 Monaten bestimmen Mahlzeiten und Entwicklung den Schlaf, und sicherer Schlaf ist Sache von Hebamme und Kinderarzt.

**Brauche ich einen Tracker oder eine Kamera?** Nein. Getippte oder diktierte Uhrzeiten reichen.

**Mehrere Kinder?** Ja, ein Profil und ein Protokoll je Kind.

**Schläft mein Kind dann durch?** Keine Versprechen. Er hilft dir, Mittagsschlaf und Schlafenszeit gut zu timen, und zeigt dir, was bei deinem Kind wirklich funktioniert.

## Mitmachen

Ideen, Übersetzungen und Rückmeldungen aus dem Alltag sind willkommen. Mach ein Issue auf, besonders wenn eine Prognose weit daneben lag: genau das braucht die Lernschleife. Bitte nie echte Kinderdaten in Issues posten.

## Lizenz

[MIT](LICENSE). Keine medizinische Beratung.
