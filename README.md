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

Alle Bilder stammen aus den Druckdateien in `Desktop/Tierkinder` und
`Desktop/Wimmelbuch`. Die Farben im `:root`-Block sind aus beiden Covern
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

**Hosting: Netlify. Domain: one.com.** Der Code liegt auf GitHub, Netlify holt
ihn von dort — jeder Push auf `main` veröffentlicht automatisch.

### Einmalig einzurichten

Diesen Schritt kann nur du machen, weil dafür ein Konto angelegt wird:

1. `app.netlify.com` öffnen → **Sign up with GitHub**. Kostenlos, keine
   Zahlungsdaten. Netlify fragt nach Zugriff auf deine Repositories —
   „Only select repositories" genügt, dort `kreativdschungel` auswählen.
2. **Add new site → Import an existing project → GitHub →** `kreativdschungel`
3. Build command leer lassen, Publish directory auf `.` setzen. Es gibt nichts
   zu bauen, die Seite ist fertiges HTML.
4. **Deploy.** Danach ist sie unter einer `…netlify.app`-Adresse erreichbar.

### Domain verbinden

Im Netlify-Projekt unter **Domain management → Add a domain** die Domain
`kreativdschungel.de` eintragen. Netlify zeigt dann die DNS-Werte an. Die
trägst du bei one.com unter **Domain → DNS Einstellungen** ein — in der Regel:

| Typ | Name | Wert |
|---|---|---|
| A | `@` | die IP, die Netlify nennt |
| CNAME | `www` | `dein-projekt.netlify.app` |

Immer die Werte nehmen, die Netlify selbst anzeigt. Der bestehende A-Record auf
`46.30.211.38` (one.coms Parkseite) wird dabei ersetzt. Bis die Änderung überall
greift, dauert es zehn Minuten bis 24 Stunden. Das TLS-Zertifikat stellt Netlify
danach automatisch aus.

### Etwas ändern

```bash
cd "/Users/sebastianmentzel/Desktop/Objektlupe/kreativdschungel-website"
git add -A
git commit -m "Impressum ausgefüllt"
git push
```

Nach rund einer Minute ist es live. `git log --oneline` zeigt alle Stände,
Netlify hält jede veröffentlichte Fassung vor und kann auf Knopfdruck
zurückrollen.

### Lokal ansehen

```bash
cd "/Users/sebastianmentzel/Desktop/Objektlupe/kreativdschungel-website" && python3 -m http.server 8788
```

Dann `http://localhost:8788` aufrufen. Über `file://` funktionieren die
Schriften nicht, weil der Browser sie dort blockiert.

### E-Mail-Postfach

Es gibt noch keines (kein MX-Eintrag). Zwei Möglichkeiten: bei one.com unter
**E-Mail** ein Postfach `post@kreativdschungel.de` dazubuchen, oder vorerst eine
bestehende Adresse ins Impressum schreiben. Rechtlich reicht beides.

## Nach dem Livegang

1. **Pinterest-Domain bestätigen**: Einstellungen → Beanspruchte Konten →
   Website beanspruchen → HTML-Tag. Den Code statt
   `HIER-DEN-CODE-VON-PINTEREST-EINSETZEN` eintragen, pushen, bestätigen.
2. **Rich Pins freischalten** über den URL-Debugger von Pinterest.
3. **Pin-Ziele umstellen** von Amazon auf die Website (geht pro Pin, ohne ihn
   neu anzulegen).
4. **Google Search Console** einrichten und die Sitemap einreichen:
   `https://kreativdschungel.de/sitemap.xml`

## Datenschutz

Die Seite lädt nichts von fremden Servern: Schriften liegen lokal, es gibt keine
Cookies, keine Analyse, kein Kontaktformular. Dadurch braucht sie kein
Cookie-Banner.

Netlify ist als Hoster im Datenschutzabschnitt eingetragen, die Domain bei
one.com. Zwei Dinge bleiben zu erledigen: die genaue Anschrift von Netlify aus
deren eigenem Impressum übernehmen — Firmenverzeichnisse nennen drei
verschiedene — und den **Auftragsverarbeitungsvertrag** abschließen. Er ist Teil
der Nutzungsbedingungen von Netlify; das unterschriebene Formular geht an
privacy@netlify.com. Netlify sitzt in den USA, deshalb steht der Absatz zur
Drittlandsübermittlung wieder in der Datenschutzerklärung. Wenn du später Statistiken willst, nimm etwas ohne Cookies
(Plausible, Fathom) — sonst wird das Banner doch fällig.
