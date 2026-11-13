# Chor anstimmen

Web-App (PWA) zum Anstimmen eines Männerchors (TTBB). Läuft auf Android in Chrome,
lässt sich auf dem Startbildschirm installieren und funktioniert danach offline.

## Funktionen
- Lieder mit Starttönen für Tenor 1, Tenor 2, Bass 1 und Bass 2 anlegen, bearbeiten und löschen
- Lied auswählen: Töne als grosse Tasten, einzeln antippen oder **Alle zusammen** / **Nacheinander** abspielen
- Klavierton wird in der App erzeugt (Web Audio), es braucht keine Sounddateien und kein Internet
- Export/Import aller Lieder als JSON-Datei (Teilen über Mail/WhatsApp/Drive oder als Download)
- Einstellungen: Stimmton a' (z.B. 440/442 Hz), Tondauer, Abstand bei „Nacheinander“

## Auf das Android-Handy bringen
Damit die App installiert werden kann und offline läuft, muss sie über **https** ausgeliefert werden.
Am einfachsten geht das mit GitHub Pages (kostenlos):

1. Ein neues GitHub-Repository anlegen und alle Dateien aus diesem Ordner hochladen.
2. Unter *Settings → Pages* den Branch `main` / Ordner `/` auswählen.
3. Die angezeigte URL (`https://<user>.github.io/<repo>/`) auf dem Handy in Chrome öffnen.
4. Im Chrome-Menü (⋮) **„Zum Startbildschirm hinzufügen“ / „App installieren“** wählen.

Andere Hoster wie Netlify oder ein eigener Webserver gehen genauso.

Lokal testen am PC: `python -m http.server 8000` in diesem Ordner starten und `http://localhost:8000` öffnen.

## Config-Datei (Export/Import)
```json
{
  "app": "chor-anstimmen",
  "version": 1,
  "stimmton_a4": 440,
  "lieder": [
    { "name": "Beispiel in D-Dur", "tenor1": "Fis4", "tenor2": "D4", "bass1": "A3", "bass2": "D3", "bemerkung": "optional" }
  ]
}
```
- Töne werden mit deutschem Notennamen und Oktavzahl angegeben (wissenschaftliche Oktavzählung, c' = `C4`):
  `C Cis D Es E F Fis G As A B H`. Achtung: `B` = B♭ und `H` = H.
  Akzeptiert werden auch `Des`, `Ges`, `F#3` und MIDI-Nummern (60 = c').
- `null` steht für ein Register ohne Ton.
- Beim Import kann man wählen: **zusammenführen** (gleiche Liednamen werden überschrieben) oder **alles ersetzen**.
- `beispiel-lieder.json` ist eine Beispieldatei zum Ausprobieren des Imports.

## Dateien
| Datei | Zweck |
|---|---|
| `index.html` | die ganze App (UI, Klangerzeugung, Speicher, Import/Export) |
| `manifest.webmanifest` | App-Name und Icons für die Installation |
| `sw.js` | Service Worker für den Offline-Betrieb |
| `icon-192.png`, `icon-512.png` | App-Icons |
