# kreativdschungel.de

Statische Website für zwei Bücher von Sebastian Mentzel. Eine Seite, kein Build,
kein Framework — die Dateien gehen so wie sie sind auf jeden Hoster.

| Buch | ASIN |
|---|---|
| Weihnachten im kleinen Walddorf — Mein Weihnachts-Wimmelbuch | `B0HL3NRJ7P` |
| Tierkinder entdecken Berufe — Kleine Tiere, große Träume | `B0HKYQXX5G` |
| Das lustige Tier-Malbuch — 40 Motive von sportlichen Tieren | `B0H2L4VM4R` |

```
index.html       die komplette Seite (Struktur, CSS, JavaScript)
schriften.css    @font-face-Regeln für die lokalen Schriften
fonts/           Baloo 2 + Nunito als woff2, 132 KB
bilder/          drei Cover, Logo, sechs Wimmelbilder, sechs Ausmalbilder
vorschaubild.png 1200x630, erscheint beim Teilen in WhatsApp und Pinterest
favicon.svg, robots.txt, sitemap.xml, vercel.json
```

Alle Bilder stammen aus den Original-Druckdateien der Bücher. Die Farben im `:root`-Block sind aus beiden Covern
ausgelesen: Titelblau und Orange vom Malbuch, Tannengrün und Rot vom
Wimmelbuch. Jedes Buchkapitel trägt die Farben seines Covers.

## Vor dem Veröffentlichen ausfüllen

Titel, ASINs, Buchdaten und Autorenname stehen richtig drin. Offen ist:

1. **Innenseiten des Tier-Malbuchs nachliefern.** Für dieses Buch lag nur die
   Coverdatei vor, deshalb fehlt dort der „Blick ins Buch“. Sobald die
   Innenseiten-PDF da ist, lassen sich wie bei den anderen Büchern Motive
   herausziehen.
2. **Altersangabe des Wimmelbuchs klären.** Die Rückseite nennt „ab 2 Jahren“,
   die Titelseite im Buch „ab 4 Jahren“. Das widerspricht sich und steht auch
   bei Amazon. Entscheiden, dann an allen drei Stellen vereinheitlichen.
3. **Den dunklen Streifen oben in `index.html` löschen** (`<div class="hinweis">`).
4. **E-Mail-Adresse** — an zwei Stellen: Abschnitt Kontakt und Impressum.
5. **Impressum**: Straße, PLZ, Ort und die Zeile zur Umsatzsteuer. Pflicht nach
   § 5 DDG, sobald die Seite geschäftsmäßig ist.
6. **Text über dich** im Abschnitt „Über mich“ — zwei kurze Absätze.
7. **Zwei offene Antworten** im Frageteil: weitere Titel und Kita-Mengen.
8. **Hoster im Datenschutz**, sobald entschieden ist, wo die Seite liegt.
9. **Pinterest-Code** in `<meta name="p:domain_verify">`, sobald die Seite live ist.

Alle offenen Stellen sind mit `class="fuell"` ausgezeichnet und erscheinen auf
der Seite orange.

## Veröffentlichen

**Hosting: GitHub Pages. Domain: one.com.** Jeder Push auf `main` veröffentlicht
die Seite automatisch — es gibt keinen separaten Upload-Schritt.

### Etwas ändern

```bash
git add -A
git commit -m "Impressum ausgefüllt"
git push
```

Nach ein bis zwei Minuten ist die Änderung live. `git log --oneline` zeigt alle
Stände, `git revert <commit>` nimmt einen zurück.

### Lokal ansehen

```bash
python3 -m http.server 8788
```

Dann `http://localhost:8788` aufrufen. Über `file://` funktionieren die
Schriften nicht, weil der Browser sie dort blockiert.

### Domain verbinden

Die DNS-Einträge werden bei one.com gesetzt, unter **Domain → DNS
Einstellungen**. Für GitHub Pages sind das vier A-Einträge und ein CNAME:

| Typ | Name | Wert |
|---|---|---|
| A | `@` | `185.199.108.153` |
| A | `@` | `185.199.109.153` |
| A | `@` | `185.199.110.153` |
| A | `@` | `185.199.111.153` |
| CNAME | `www` | `doppelkind.github.io` |

Der bestehende A-Eintrag auf `46.30.211.38` (Parkseite von one.com) wird dabei
ersetzt. Bis die Änderung greift, dauert es zehn Minuten bis 24 Stunden. Das
TLS-Zertifikat stellt GitHub danach selbst aus.

### Wichtig: robots.txt

Die Datei sperrt derzeit alle Suchmaschinen aus — absichtlich, solange das
Impressum unvollständig ist. Nach dem Ausfüllen den auskommentierten Block
darin aktivieren, sonst findet Google die Seite nie.

## Nach dem Livegang

1. **robots.txt freigeben** (siehe oben)
2. **Pinterest-Domain bestätigen**: Einstellungen → Beanspruchte Konten →
   Website beanspruchen → HTML-Tag. Den Code statt
   `HIER-DEN-CODE-VON-PINTEREST-EINSETZEN` eintragen, pushen, bestätigen.
3. **Rich Pins freischalten** über den URL-Debugger von Pinterest.
4. **Pin-Ziele umstellen** von Amazon auf die Website (geht pro Pin, ohne ihn
   neu anzulegen).
5. **Google Search Console** einrichten und die Sitemap einreichen.

## Datenschutz

Die Seite lädt nichts von fremden Servern: Schriften liegen lokal, es gibt keine
Cookies, keine Analyse, kein Kontaktformular. Dadurch braucht sie kein
Cookie-Banner.

GitHub ist als Hoster im Datenschutzabschnitt eingetragen, die Domain liegt bei
one.com. GitHub gehört zu Microsoft und sitzt in den USA, deshalb steht der
Absatz zur Drittlandsübermittlung in der Datenschutzerklärung. Prüfe die
Anschrift gegen GitHubs eigene Angaben und schließe den
Auftragsverarbeitungsvertrag ab. Wenn du später Statistiken willst, nimm etwas ohne Cookies
(Plausible, Fathom) — sonst wird das Banner doch fällig.
