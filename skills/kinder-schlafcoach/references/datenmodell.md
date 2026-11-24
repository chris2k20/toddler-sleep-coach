# Datenmodell Schlafprotokoll

Ein Protokoll je Kind. Eine Zeile je lokalem Kalendertag (Europe/Berlin, bzw. Zeitzone aus dem Kinderprofil). Die Nacht gehört zu dem Tag, an dessen Abend sie beginnt.

## Tagesfelder

| Feld | Bedeutung | Beispiel |
|---|---|---|
| `datum` | lokales Datum des Tages | 2026-11-24 |
| `first_awake` | erstes Aufwachen am Morgen | 06:40 |
| `final_awake` | endgültig wach, falls nach kurzer Unterbrechung wieder eingeschlafen; sonst gleich `first_awake` | 07:10 |
| `out_of_bed` | aus dem Bett genommen, getrennt vom Aufwachen | 07:25 |
| `nap1_start`, `nap1_end` | erster Tagschlaf, tatsächlich geschlafen | 12:04, 12:42 |
| `nap1_ort` | Bett, Auto, Kinderwagen, Trage, Kita | Auto |
| `nap1_unterbrechung` | Wachphase im Tagschlaf in Minuten, sonst leer | 10 |
| `nap1_geweckt` | von Erwachsenen geweckt: ja/nein | nein |
| `nap2_…` | zweiter Tagschlaf (jüngere Kinder), gleiche Felder | |
| `muede_vorher`, `muede_nachher` | Müdigkeit kurz: niedrig/mittel/hoch/unbekannt | hoch |
| `routine_start` | Beginn Abendroutine | 19:05 |
| `hingelegt` | ins Bett gelegt | 19:35 |
| `night_sleep_onset` | tatsächlich eingeschlafen | 20:30 |
| `einschlafen_entspannt` | ja/nein/unbekannt | ja |
| `nachtwach` | Liste: Start–Ende, Intensität (leicht/mittel/stark) | 02:10–02:40 mittel |
| `night_quality` | Elternurteil gut/mittel/schlecht/unbekannt | gut |
| `krank` | nein, oder Stichwort (Fieber, Husten, Zahnen) ohne Nebendetails | Husten |
| `besonderes` | Reise, Kita-Eingewöhnung, Zeitumstellung, Besuch | Reise |
| `prognose_fenster` | vorhergesagtes Einschlaffenster des Abends | 19:00–20:00 |
| `prognose_bevorzugt` | bevorzugte Uhrzeit | 19:30 |
| `abweichung_min` | 0, wenn im Fenster; sonst Minuten vor (−) oder nach (+) dem Fenster | +30 |
| `konfidenz` | niedrig/mittel/hoch | niedrig |
| `elternbewertung` | freier Kurzkommentar der Eltern | „war okay“ |

## Regeln

- **Gemessen vs. geschätzt:** Geschätzte Zeiten mit `~` kennzeichnen (`~20:10`). Nie als gemessen ausgeben.
- **Unbekannt bleibt unbekannt:** fehlende Werte leer oder `unbekannt`, nie auffüllen.
- **Korrekturen ersetzen** den alten Wert im selben Tag; das alte Wert-Paar optional im Änderungslog.
- **Wachfenster** nur zwischen Zeiten derselben lokalen Tagesbasis rechnen. Zeitumstellung als Sonderfall markieren (`besonderes: Zeitumstellung`).
- **Zeit im Bett ist nicht Schlafzeit**, sobald Wachphasen bekannt sind: Nachtschlaf = Morgen-Aufwachen minus Einschlafen minus Nachtwachphasen.
- **Abgeleitete Werte** (Wachfenster vormittags = `nap1_start − final_awake`, nachmittags = `night_sleep_onset − letztes nap_end`, Gesamtschlaf 24 h) werden berechnet, nicht gespeichert, oder als eigene Spalte klar als abgeleitet markiert.

## Abschnitte im Protokoll

1. **Kinderprofil-Verweis** (Rufname, Profilversion)
2. **Aktuelle Modellparameter** mit Datum und Anzahl Beobachtungen
3. **Neue Tagesmeldungen** (Tageszeilen wie oben)
4. **Lernnotizen** (versioniert: Datum, n, alte Spanne, neue Spanne, Gegenbeispiele)
5. **Änderungslog** (nur echte Regeländerungen)
