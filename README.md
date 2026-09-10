# cletos.nl — website

Eén statische pagina: `index.html` + `styles.css`. Geen framework, geen JavaScript, geen cookies. Gehost op GitHub Pages onder het domein cletos.nl (domein bij TransIP).

## Wat is wat

- `index.html` — de tekst en de opbouw van de pagina
- `styles.css` — kleuren, lettertype en indeling
- `CNAME` — vertelt GitHub Pages welk domein bij deze site hoort
- `assets/` — foto's en andere bestanden (nu nog leeg; hier komt de foto van Bas)

Lokaal bekijken: open `index.html` in een browser. Meer is niet nodig.

## Eén keer: live zetten

1. **GitHub-repo aanmaken** (publiek; GitHub Pages op een gratis account vereist dat) en deze map pushen. Bijvoorbeeld:
   ```bash
   gh repo create cletos-website --public --source=. --push
   ```
2. **Pages aanzetten** in de repo: Settings → Pages → Source "Deploy from a branch", branch `main`, map `/ (root)`. Vul bij "Custom domain" `cletos.nl` in en vink "Enforce HTTPS" aan zodra dat kan (na de DNS-stap).
3. **DNS bij TransIP** (Domeinen → cletos.nl → DNS). Verwijder het parkeer-A-record en zet:

   | Naam | Type | Waarde |
   |---|---|---|
   | `@` | A | `185.199.108.153` |
   | `@` | A | `185.199.109.153` |
   | `@` | A | `185.199.110.153` |
   | `@` | A | `185.199.111.153` |
   | `www` | CNAME | `streefkerkshipping.github.io.` |

   Doorlooptijd: meestal binnen een uur, soms tot 24 uur. Daarna in GitHub "Enforce HTTPS" aanvinken.
4. **E-mail**: maak bij TransIP een doorstuuradres `bas@cletos.nl` → je eigen mailbox, vóór de DNS-stap. Anders staat er een mailadres op de site dat niet bestaat.

## Daarna: iets aanpassen

Tekst wijzigen in `index.html`, dan:
```bash
git add -A && git commit -m "Tekst bijgewerkt" && git push
```
Binnen een minuut staat het live.

## Nog te doen vóór live-gang

- [ ] Foto van Bas in `assets/` en het fotoslot in `index.html` vervangen
- [ ] btw-id in de footer invullen (wettelijk verplicht)
- [ ] Doorstuuradres bas@cletos.nl aanmaken bij TransIP
- [ ] Lettertype zelf hosten in `assets/fonts/` in plaats van via Google Fonts (privacy: dan gaat er géén verzoek naar Google)
