# kreativdschungel.de

Statische Website für das Malbuch „Tierkinder entdecken Berufe“. Eine Seite,
kein Build, kein Framework — die Dateien gehen so wie sie sind auf jeden Hoster.

```
index.html       die komplette Seite (Struktur, CSS, JavaScript)
schriften.css    @font-face-Regeln für die lokalen Schriften
fonts/           Baloo 2 + Nunito als woff2, 132 KB
bilder/          Cover, Logo, sechs Ausmalbilder, Titelseite
vorschaubild.png 1200x630, erscheint beim Teilen in WhatsApp und Pinterest
favicon.svg      Monstera-Blatt, das Icon im Browser-Tab
robots.txt       erlaubt Suchmaschinen alles, verweist auf die Sitemap
sitemap.xml      eine URL; bei weiteren Seiten hier ergänzen
vercel.json      Caching für Schriften + drei Sicherheits-Header
```

Cover, Ausmalbilder und Markenfarben stammen direkt aus den Druckdateien in
`Desktop/Tierkinder`. Die Farben im `:root`-Block von `index.html` sind aus der
Coverdatei ausgelesen, damit Website und Buch zusammenpassen.

## Vor dem Veröffentlichen ausfüllen

Buchdaten, Titel, ASIN und Autorenname stehen bereits richtig drin. Offen ist nur
noch das Persönliche und das Rechtliche:

1. **Den dunklen Streifen oben in `index.html` löschen** (`<div class="hinweis">`).
2. **E-Mail-Adresse** — steht an zwei Stellen: im Abschnitt Kontakt und im
   Impressum. Derzeit `post@kreativdschungel.de` als Platzhalter.
3. **Impressum**: Straße, PLZ und Ort sowie die Zeile zur Umsatzsteuer. Pflicht
   nach § 5 DDG, sobald die Seite geschäftsmäßig ist. Ein fehlendes Impressum ist
   der häufigste Abmahngrund bei kleinen Websites.
4. **Text über dich** im Abschnitt „Über mich“ — zwei kurze Absätze.
5. **Zwei offene Antworten** im Frageteil: weitere Malbücher und Kita-Mengen.
6. **Hoster im Datenschutz** eintragen, sobald entschieden ist, wo die Seite liegt.
7. **Pinterest-Code** in `<meta name="p:domain_verify">`, sobald die Seite live ist.

Alle offenen Stellen sind im Quelltext mit `class="fuell"` ausgezeichnet und
erscheinen auf der Seite orange.

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
