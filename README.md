# Landesrecht Bremen

<p>
  <a href="https://github.com/Gesetze-fuer-KI/landesrecht-hb/actions/workflows/sync.yml"><img alt="Nächtlicher Abgleich" src="https://github.com/Gesetze-fuer-KI/landesrecht-hb/actions/workflows/sync.yml/badge.svg"></a>
</p>

**Das Landesrecht von Bremen für [Gesetze für KI](https://gesetze-fuer-ki.de):** Ihr KI-Assistent schlägt damit die aktuellen Landesgesetze nach. Alles zum Einrichten steht auf **[gesetze-fuer-ki.de](https://gesetze-fuer-ki.de)**.

---

<sub>Ab hier für Neugierige und alle, die mitmachen wollen.</sub>

## Was hier liegt

Alle Gesetze und Rechtsverordnungen der Freien Hansestadt Bremen in der heute geltenden Fassung, eine Textdatei (Markdown) je Gesetz. Verwaltungsvorschriften, Bekanntmachungen und Satzungen sind nicht enthalten. Ortsgesetze der Stadtgemeinden Bremen und Bremerhaven sind nicht enthalten: Sie sind Ortsrecht, wie Satzungen in anderen Ländern. Jede Nacht kommt als Commit hinzu, was sich geändert hat. Die Dateien sind auch für sich nutzbar: zum Lesen, Durchsuchen und Vergleichen von Fassungen.

## Quelle

| | |
|---|---|
| Land | Bremen |
| Portal | [Transparenzportal Bremen](https://www.transparenz.bremen.de) (transparenz.bremen.de) |
| Betreiber | Der Senator für Finanzen der Freien Hansestadt Bremen |
| Fassung | **nichtamtlich**, wie das Portal selbst sagt |

Die Texte sind die konsolidierten, **nichtamtlichen Fassungen** des Portals. Rechtlich maßgeblich ist allein, was im Gesetzblatt der Freien Hansestadt Bremen verkündet wurde.

## Wie der Abgleich läuft

Die [Action](.github/workflows/sync.yml) läuft jede Nacht um 02:07 UTC mit [`sync.py --land hb`](https://github.com/Gesetze-fuer-KI/gesetze-fuer-ki/blob/main/app/sync.py) aus [gesetze-fuer-ki](https://github.com/Gesetze-fuer-KI/gesetze-fuer-ki). Sie hält die robots.txt des Portals ein und stellt höchstens zwei Anfragen gleichzeitig.

Die Trefferliste des Portals nennt zu jeder Fassung eine eigene Kennung und den Stand. Neu geladen wird nur eine neue Fassung. Steht schon fest, wann die nächste Fassung gilt, wird sie an diesem Tag übernommen.

Der **erste vollständige Abgleich** kann mehrere Nächte dauern. Jeder Lauf hört rechtzeitig vor dem Zeitlimit von GitHub auf, merkt sich in `.sync/state.json`, wie weit er gekommen ist, und committet den Zwischenstand; der nächste Lauf macht dort weiter. Bis der erste Durchgang fertig ist, steht Bremen auf gesetze-fuer-ki.de als „im Aufbau“ und ist noch nicht durchsuchbar. Gesetze, die das Portal nicht mehr führt, werden erst nach einem vollständigen Durchgang gelöscht.

Hinweis für die Betreuung: GitHub pausiert geplante Workflows, wenn ein Repository 60 Tage lang keine Commits bekommt. Ein Lauf von Hand (**Actions → Sync → Run workflow**, `workflow_dispatch`) schaltet ihn wieder ein.

## Ein Gesetz finden

Die Dateien heißen nach dem Länderkürzel und der Kennung des Gesetzes auf dem Portal und liegen in einem Ordner nach den ersten zwei Zeichen dieser Kennung (`<ordner>/<kennung>.md`): `ta/hb-tariftvergabegbr.md` ist das Gesetz mit der Dokumentkennung `jlr-TariftVergabeGBRrahmen`. Jede Datei beginnt mit Metadaten (Land, Abkürzung, Titel, Stand, Quelle mit Link aufs Portal); danach folgen Gliederung und Vorschriften als Überschriften, jeweils mit einem unsichtbaren Kommentar, der die Kennung der Vorschrift trägt. Jede Datei beginnt mit der Namensnennung nach der Lizenz des Portals.

Der Ordner `.sync/` gehört dem Abgleich: `state.json` (Fortschritt und was er sich über die Gesetze merkt) und `commit-message.txt` (die Nachricht des letzten Commits).

## Änderungen ansehen

Auf GitHub: eine Datei öffnen und **History** klicken. Lokal:

```bash
git log -p -- <ordner>/<kennung>.md
```

Die Commit-Nachricht nennt je geändertem Gesetz eine Zeile mit Abkürzung und neuem Stand.

## Herkunft und Lizenz

Die Texte stehen unter der Lizenz [CC BY-NC-ND 3.0](https://creativecommons.org/licenses/by-nc-nd/3.0/) (Namensnennung, nicht kommerziell, keine Bearbeitung). Namensnennung: **Transparenzportal Bremen, Der Senator für Finanzen der Freien Hansestadt Bremen.** Einzelheiten in [LIZENZ.md](LIZENZ.md).

Fehler der Umwandlung bitte als [Issue](https://github.com/Gesetze-fuer-KI/gesetze-fuer-ki/issues) melden, alles andere an [kontakt@gesetze-fuer-ki.de](mailto:kontakt@gesetze-fuer-ki.de). Mehr unter [Daten und Grenzen](https://gesetze-fuer-ki.de/daten/).

---

<sub>Keine Rechtsberatung: Der Dienst liefert Gesetzestexte; maßgeblich ist die amtliche Fassung. · [Unterstützen](https://gesetze-fuer-ki.de/unterstuetzen/) · [Impressum](https://gesetze-fuer-ki.de/impressum/) · [Datenschutz](https://gesetze-fuer-ki.de/datenschutz/)</sub>
