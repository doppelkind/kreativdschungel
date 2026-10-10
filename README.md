# kreativdschungel.de

Statische Website, eine Seite. Kein Build, kein Framework — die Dateien gehen
so wie sie sind auf jeden Hoster.

```
index.html       die komplette Seite (Struktur, CSS, JavaScript)
schriften.css    @font-face-Regeln für die lokalen Schriften
fonts/           Literata + Shantell Sans als woff2, 350 KB
favicon.svg      Monstera-Blatt, das Icon im Browser-Tab
robots.txt       erlaubt Suchmaschinen alles, verweist auf die Sitemap
sitemap.xml      eine URL; bei weiteren Seiten hier ergänzen
vercel.json      Caching für Schriften + drei Sicherheits-Header
```

## Vor dem Veröffentlichen ausfüllen

1. **Den schwarzen Streifen oben in `index.html` löschen** (`<div class="demo-bar">`).
2. **Amazon-Links**: fünfmal `ASIN-HIER-EINSETZEN` ersetzen. Die ASIN steht auf
   der Amazon-Produktseite unter „Produktinformationen“.
3. **Buchdaten**: Titel, Klappentexte, Altersangaben, Seitenzahlen in den drei
   `<article class="book">`-Blöcken.
4. **Leseprobe**: der Text steht zweimal drin — sichtbar im `<div class="spread">`
   und im Array `doppelseiten` unten im `<script>`. Beide anpassen.
5. **Impressum**: alle `[eckigen Klammern]` im `<footer>`. Pflicht nach § 5 DDG,
   sobald die Seite geschäftsmäßig ist. Fehlendes Impressum ist der häufigste
   Abmahngrund bei kleinen Websites.
6. **Hoster im Datenschutz** eintragen (Name und Anschrift des Anbieters).
7. **Cover**: `<svg class="cover">…</svg>` durch `<img class="cover" src="cover-1.jpg" alt="…">`
   ersetzen, sobald echte Cover vorliegen.
8. **Rezensionen**: die drei gestrichelten Platzhalter in `#stimmen` entweder mit
   echten Zitaten füllen oder die ganze Sektion löschen. Erfundene Bewertungen
   sind nach § 5 UWG unzulässig.
9. **`vorschaubild.png`** anlegen (1200 × 630 px) — das Bild, das beim Teilen in
   WhatsApp oder Facebook erscheint. Ohne diese Datei bleibt die Vorschau leer.

## Veröffentlichen

Die Seite liegt auf GitHub und wird von Vercel automatisch veröffentlicht.
Jeder Push auf `main` löst ein neues Deployment aus — ein eigener Upload-Schritt
entfällt.

### Etwas ändern

```bash
cd "/Users/sebastianmentzel/Desktop/Objektlupe/kreativdschungel-website"
# Datei bearbeiten, dann:
git add -A
git commit -m "Klappentext von Band 2 überarbeitet"
git push
```

Nach rund 30 Sekunden ist die Änderung live. Die Historie bleibt erhalten:
`git log --oneline` zeigt alle Stände, `git revert <commit>` nimmt einen zurück.

### Vorschau vor dem Livegang

Für größere Änderungen einen Zweig nehmen:

```bash
git checkout -b neue-texte
git push -u origin neue-texte
```

Vercel baut daraus eine eigene Vorschau-Adresse, die `kreativdschungel.de` nicht
anfasst. Passt alles, den Zweig auf GitHub mergen — dann geht es live.

### Lokal ansehen

```bash
cd "/Users/sebastianmentzel/Desktop/Objektlupe/kreativdschungel-website" && python3 -m http.server 8788
```

Dann `http://localhost:8788` im Browser öffnen. Über `file://` funktionieren die
Schriften nicht, weil der Browser sie dort aus Sicherheitsgründen blockiert.

## Domain verbinden

`kreativdschungel.de` erst registrieren (Netcup, INWX, United Domains, IONOS —
5–15 € im Jahr), dann im Vercel-Projekt unter **Settings → Domains** eintragen.
Vercel zeigt daraufhin die Werte an, die beim Registrar gesetzt werden:

| Typ | Name | Wert |
|---|---|---|
| A | `@` | `76.76.21.21` |
| CNAME | `www` | `cname.vercel-dns.com` |

Immer die Werte nehmen, die Vercel selbst anzeigt — sie können abweichen. Bis die
Änderung greift, dauert es zehn Minuten bis 24 Stunden. Das TLS-Zertifikat stellt
Vercel danach selbst aus.

## Datenschutz

Die Seite lädt nichts von fremden Servern: Schriften liegen lokal, es gibt keine
Cookies, keine Analyse, kein Kontaktformular. Dadurch braucht sie kein
Cookie-Banner.

Vercel ist als Hoster im Datenschutzabschnitt eingetragen. Zwei Dinge musst du
dort noch erledigen: die Anschrift gegen Vercels eigene Datenschutzerklärung
prüfen, und im Vercel-Konto den **Auftragsverarbeitungsvertrag** abschließen.
Vercel sitzt in den USA — ohne diesen Vertrag fehlt die Rechtsgrundlage für die
Übermittlung der Zugriffsdaten ins Drittland. Wenn du später Statistiken willst, nimm etwas ohne Cookies
(Plausible, Fathom) — sonst wird das Banner doch fällig.
