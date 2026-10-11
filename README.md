# kreativdschungel.de

Statische Website für zwei Bücher von Sebastian Mentzel. Eine Seite, kein Build,
kein Framework — die Dateien gehen so wie sie sind auf jeden Hoster.

| Buch | ASIN |
|---|---|
| Weihnachten im kleinen Walddorf — Mein Weihnachts-Wimmelbuch | `B0HL3NRJ7P` |
| Tierkinder entdecken Berufe — Kleine Tiere, große Träume | `B0HKYQXX5G` |

```
index.html       die komplette Seite (Struktur, CSS, JavaScript)
schriften.css    @font-face-Regeln für die lokalen Schriften
fonts/           Baloo 2 + Nunito als woff2, 132 KB
bilder/          zwei Cover, Logo, sechs Wimmelbilder, sechs Ausmalbilder
vorschaubild.png 1200x630, erscheint beim Teilen in WhatsApp und Pinterest
favicon.svg, robots.txt, sitemap.xml, vercel.json
```

Alle Bilder stammen aus den Druckdateien in `Desktop/Tierkinder` und
`Desktop/Wimmelbuch`. Die Farben im `:root`-Block sind aus beiden Covern
ausgelesen: Titelblau und Orange vom Malbuch, Tannengrün und Rot vom
Wimmelbuch. Jedes Buchkapitel trägt die Farben seines Covers.

## Vor dem Veröffentlichen ausfüllen

Titel, ASINs, Buchdaten und Autorenname stehen richtig drin. Offen ist:

1. **Altersangabe des Wimmelbuchs klären.** Die Rückseite nennt „ab 2 Jahren“,
   die Titelseite im Buch „ab 4 Jahren“. Das widerspricht sich und steht auch
   bei Amazon. Entscheiden, dann an allen drei Stellen vereinheitlichen.
2. **Den dunklen Streifen oben in `index.html` löschen** (`<div class="hinweis">`).
3. **E-Mail-Adresse** — an zwei Stellen: Abschnitt Kontakt und Impressum.
4. **Impressum**: Straße, PLZ, Ort und die Zeile zur Umsatzsteuer. Pflicht nach
   § 5 DDG, sobald die Seite geschäftsmäßig ist.
5. **Text über dich** im Abschnitt „Über mich“ — zwei kurze Absätze.
6. **Zwei offene Antworten** im Frageteil: weitere Titel und Kita-Mengen.
7. **Hoster im Datenschutz**, sobald entschieden ist, wo die Seite liegt.
8. **Pinterest-Code** in `<meta name="p:domain_verify">`, sobald die Seite live ist.

Alle offenen Stellen sind mit `class="fuell"` ausgezeichnet und erscheinen auf
der Seite orange.

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
