# Philips-Startbild „Jetzt im Fernsehen" · Übergabe für Claude Code

Stand 17.11.2026, ausgearbeitet im Claude-Projekt „Meyborn CI". Diese Datei ist der Auftrag für eine erste Demo. Sie beschreibt das Ziel, den Aufbau, was technisch geprüft ist und was offen bleibt.

## Worum es geht

Im Haushalt laufen zwei Oberflächen im selben Meyborn-Design:

- **Fire TV** mit `fepe89/dumbtv`. Er hängt an **HDMI 1** des Philips. Sein Startbild zeigt Filmempfehlungen.
- **Philips** (Android TV, 55 Zoll, 4K) mit diesem Fork. Empfang über **Satellit**. Der Launcher läuft als `com.gathin.tvhome`.

Familie und Babysitter müssen auf einen Blick erkennen, welches System gerade läuft. Farben, Schrift, Kacheln und Fokus bleiben auf beiden gleich (Meyborn CI). Der Unterschied liegt im Hauptbereich: Der Fire TV zeigt **Filmempfehlungen**, der Philips zeigt **„Jetzt im Fernsehen"**, weil man am Philips fernsieht und nicht in Apps geht.

## Entscheidungen von Felix (verbindlich)

| Nr. | Entscheidung |
|---|---|
| 50 | Beide Fernseher teilen Kopfzeile, Farben, Schrift, Kacheln und Fokus. Sie unterscheiden sich im Hauptbereich: Fire TV Filmempfehlungen, Philips „Jetzt im Fernsehen". |
| 51 | Philips-Hauptbereich: links eine große Karte mit dem laufenden Sender, rechts eine anwählbare Senderliste mit den Reitern „Jetzt" und „20:15". Die Liste soll möglichst interaktiv sein, OK schaltet direkt auf den Sender. |
| 52 | Kopfzeile auf beiden Geräten gleich: Bullauge links neben Uhrzeit und Datum, rechts die runden Symbolknöpfe. Am Philips sind es drei: Eingänge, Netzwerk, Einstellungen. |
| 53 | Am Philips steht links neben dem Datum ein Umschalter „Fernseher / Fire TV". „Fernseher" ist aktiv, „Fire TV" wechselt auf HDMI 1. |
| 54 | Empfang am Philips über Satellit. Der Fire TV hängt an HDMI 1. |

Nr. 50 bis 54 stehen im Projekt in `02_ENTSCHEIDUNGEN.md`. In `fepe89/meyborn-ci` (`docs/ENTSCHEIDUNGEN.md`, `plattformen/fire-tv/VORGABEN.vorlage.md`) fehlen sie noch und müssen dort nachgetragen werden.

## Entwurf

- `entwurf/philips-jetzt-im-fernsehen.html` in diesem Ordner: der Entwurf als einzelne HTML-Seite, im Browser zu öffnen. Er ist in halber Größe gezeichnet (960 × 540), alle Pixelwerte darin also mal zwei nehmen.
- Design-Fläche „Meyborn CI", Seite „Fernseher · Philips", Artboard „Philips E · Jetzt im Fernsehen": https://claude.ai/artifact/LeVFgW8FS6CsNx1VCBhSg5
- Die Reiter „Jetzt / 20:15" sind im Entwurf noch nicht gezeichnet. Sie gehören über die Senderliste, anstelle der Zeile „Jetzt im Fernsehen".

Wo der Entwurf von `plattformen/fire-tv/VORGABEN.md` in `fepe89/meyborn-ci` abweicht, gilt VORGABEN.md. Beispiel: Das Datum ist im Entwurf kleiner als die dort festgelegte Text-Stufe.

## Aufbau (alle Maße in 1080p-Pixeln)

Hintergrund fest `#17132B`, Seitenrand links und rechts 96 px, kein Hintergrundbild, keine Verläufe, kein Glas, keine App-Farbe am Fokus.

### 1. Kopfzeile (wie am Fire TV)

- Links: Bullauge (`logo/svg/meyborn-zeichen-dunkel.svg` aus meyborn-ci, 80 px, nie unter 40 px), daneben Uhrzeit (Space Grotesk 600, 48 px) und darunter das Datum (Inter 400, 36 px, `#B9B4D6`).
- Daneben der Umschalter: Pille auf `#221C3D`, darin zwei Teile in Label-Stufe (Inter 600, 30 px).
  - „Fernseher" mit Lucide `tv`: aktiv, Fläche `#2ED3C6`, Text und Symbol `#14162B`. Nicht anwählbar, es ist der Hinweis auf das Gerät.
  - „Fire TV": weißer Text ohne Fläche, anwählbar. OK wechselt auf HDMI 1.
- Rechts: drei runde Symbolknöpfe auf `#332C55` mit weißen Lucide-Symbolen: Eingänge, Netzwerk, Einstellungen. Das sind die drei Knöpfe, die der Launcher heute schon hat.

### 2. Hauptbereich „Jetzt im Fernsehen" (Höhe 500 px, Abstand zwischen den Spalten 32 px)

**Links, große Karte (rund 55 % der Breite, Radius 20 px):**

- Fläche: ein Bild zur Sendung. Es gibt kein Live-Bild (siehe Machbarkeit). Ohne Bild: Fläche `#221C3D` mit Lucide `tv`.
- Unten links eine Textplatte in `#17132BE6`, Radius 20 px, wie im Empfehlungsbanner des Fire TV. Darin von oben nach unten:
  - Chip „Läuft jetzt": Fläche `#7459D0`, weißer Text, Label-Stufe. Das ist Stufe 2 des Dringlichkeitsmodells („steht bald an oder läuft").
  - Titel der Sendung: Space Grotesk 600, 48 px.
  - „Sender · Beginn bis Ende": Inter 400, 36 px, `#B9B4D6`.
  - Fortschrittsbalken: 8 px hoch, Spur `#3D3563`, Füllung Weiß. Nicht in Türkis, Türkis ist für Anwählbares und den Fokus reserviert.
  - „OK: Fernsehen starten": Label-Stufe.
- OK öffnet das Fernsehen auf dem laufenden Sender.

**Rechts, Senderliste:**

- Oben zwei Reiter „Jetzt" und „20:15" in Label-Stufe. Der aktive Reiter bekommt die türkise Pille (`#2ED3C6`, Text `#14162B`), der andere bleibt weiß ohne Fläche. Links und rechts wechselt den Reiter.
- Darunter vier bis fünf Zeilen, eine je Lieblingssender. Fläche `#221C3D`, Radius 14 px, Abstand 16 px.
  - Links der Sendername (Inter 600, 30 px), darunter die Sendung (Inter 400, 30 px, `#B9B4D6`).
  - Rechts „bis 20:15" bzw. im Reiter „20:15" die Dauer (Inter 400, 30 px, `#B9B4D6`).
- OK auf einer Zeile schaltet direkt auf diesen Sender.
- Nichts unter 30 px Schriftgröße.

### 3. App-Reihe

Unverändert nach VORGABEN.md: Überschrift „Apps" (Label-Stufe, gedämpft), Kacheln 256 × 144 px, Radius 14 px, Abstand 32 px, Marken-Kacheln mit dem eigenen Banner der App, Meyborn-Kachel (`#221C3D`, weißes Lucide-Symbol, Name) für TV-Guide, Smart Home und Player. Die Reihe steht hier unter dem Hauptbereich, nicht mehr als Dock im Mittelpunkt.

### Fokus und Bedienung

- Fokus überall gleich: türkiser Rahmen 6 px (`#2ED3C6`), Kachel vergrößert um Faktor 1,06. Kein Leuchtrand.
- Beim Öffnen liegt der Fokus auf der großen Karte.
- Rechts: Senderliste. Hoch von der Karte: Umschalter. Runter: App-Reihe.
- In der Liste: hoch und runter durch die Sender, links und rechts wechselt den Reiter, am linken Rand zurück zur Karte.

## Daten

Die Demo braucht eine kleine Datei mit Programmdaten. Vorschlag für das Format:

```json
{
  "stand": "2026-11-17T19:42:00+01:00",
  "sender": [
    {
      "id": "das-erste",
      "name": "Das Erste",
      "jetzt": {"titel": "…", "beginn": "19:30", "ende": "20:00", "bild": "…"},
      "primetime": {"titel": "…", "beginn": "20:15", "ende": "21:45"}
    }
  ]
}
```

Für die erste Demo reicht eine mitgelieferte Beispieldatei mit erfundenen Platzhaltern. Sie muss in der Oberfläche klar als Beispiel erkennbar sein, damit niemand sie für das echte Programm hält.

## Machbarkeit: was geprüft ist

- **Kein Live-Bild im Startbild.** Android gibt die Sender des eingebauten Tuners nur an die TV-App des Herstellers. Ein fremder Launcher bekommt das Bild ohne Root nicht. Quelle: https://source.android.com/docs/devices/tv
- **Keine Programmdaten vom Fernseher.** Die Sender- und Programmdatenbank (`TvContract`) dürfen nur privilegierte System-Apps vollständig lesen. Die Programmdaten müssen aus einer eigenen Quelle kommen.
- **Sender umschalten und laufenden Sender erkennen: laut Dokumentation möglich, am Gerät noch nicht getestet.** Der Philips ist in Home Assistant als `media_player.fernseher_im_wohnzimmer` eingebunden (Philips-TV-Integration `philips_js`, Quellenliste: Watch TV, HDMI 1 bis HDMI 4). Die Integration führt für Android-Geräte Senderwahl und Sendererkennung als unterstützt. Quelle: https://www.home-assistant.io/integrations/philips_js/
- **Wechsel auf HDMI 1: im Fork vorhanden.** Der Launcher schaltet Eingänge schon heute um (Eingänge-Menü, `launch_actions` mit `input:<input id>`, siehe `themes/README.md`). Die Kennung von HDMI 1 liefert `dumpsys tv_input` am Gerät.
- **Fernsehen starten: im Fork vorhanden** über `live_tv_package`.

## Offen (bitte mit Felix klären, nicht selbst festlegen)

1. **Quelle der Programmdaten** für die Satellitensender: noch nicht recherchiert. Denkbar ist ein Lauf auf dem Raspberry Pi, ähnlich dem nächtlichen Lauf für die Filmempfehlungen am Fire TV, nur häufiger.
2. **Schaltweg für den Senderwechsel:** über Home Assistant (Kopplung steht schon, braucht aber einen laufenden Home Assistant) oder direkt vom Launcher an die Schnittstelle des Fernsehers (eigene Kopplung nötig).
3. **Lieblingssender:** welche vier bis fünf, in welcher Reihenfolge.
4. **Bild zur Sendung:** woher es kommt, hängt von der Programmquelle ab.
5. **Rückweg vom Fire TV:** Der Fire TV kann den Eingang des Philips nicht umschalten. Dort ist „Fire TV" nur ein Hinweis.

## Auftrag für die Demo

**Stufe 1 (jetzt):** Das Startbild nach diesem Aufbau im Fork bauen, mit der Beispieldatei gefüllt und mit der Fernbedienung bedienbar. Fokus, Reiter, Umschalter und App-Reihe funktionieren. OK auf der großen Karte startet das Fernsehen, OK auf „Fire TV" wechselt auf HDMI 1. OK auf einer Senderzeile zeigt in Stufe 1 nur an, welcher Sender gewählt wäre.

**Stufe 2 (nach Rücksprache):** echter Senderwechsel, Erkennung des laufenden Senders, echte Programmdaten.

Vor dem Bauen einen kurzen Plan vorlegen: welche Dateien des Launchers betroffen sind und ob das Startbild als Theme-Einstellung, als Änderung am Launcher oder als Zusatz (`addons/`, Modul-Karte) entsteht.

## Regeln

- `AGENTS.md` dieses Repos gilt.
- Alle Werte kommen aus den Meyborn-Tokens: `plattformen/fire-tv/android/values/meyborn_colors.xml` und `meyborn_dimens.xml` in `fepe89/meyborn-ci`. Keine freien Farbwerte im Code. Fehlt ein Wert, wird er in `tokens/meyborn.tokens.json` ergänzt und neu erzeugt, nach Rücksprache mit Felix.
- Schriften Space Grotesk und Inter als Dateien im APK (SIL Open Font License). Symbole nur aus Lucide.
- Genau eine Akzentfarbe: Türkis `#2ED3C6` für Anwählbares, Aktives und den Fokus. Lila und Apricot tragen nur Dringlichkeit.
- In Home Assistant nichts anlegen oder ändern ohne Freigabe von Felix.
- Nichts am Fernseher installieren, während jemand fernsieht. Vorher fragen.
- Arbeit bleibt auf diesem Branch im Fork `fepe89/cleanyourtv`. Kein Pull Request an das Ursprungsprojekt.
