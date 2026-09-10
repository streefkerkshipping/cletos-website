# cletos.nl — website

De website van Cletos: gewone HTML-pagina's en één stylesheet. Geen framework, geen JavaScript, geen cookies. Hij draait op **GitHub Pages** (gratis hosting van GitHub, rechtstreeks vanuit deze repo) onder het domein cletos.nl. Het domein staat bij TransIP.

## Wat is wat

- `index.html` — de voorpagina (intro, "Voor wie", nieuws)
- `diensten/`, `ai-zichtbaarheidsscan/`, `ai-automatisering/`, `ai-assistent/` — het aanbod en de prijzen
- `nieuws/`, `over-bas/`, `contact/` — de overige pagina's
- `styles.css` — kleuren, lettertypes en indeling (het `?v=`-nummer in de pagina's ophogen na een wijziging, anders tonen browsers de oude versie)
- `assets/` — foto, logo en favicon (de originelen staan lokaal en in `.gitignore`, niet in de repo)
- `CNAME` — vertelt GitHub Pages welk domein bij deze site hoort
- `robots.txt` — zegt tegen zoekmachines en AI-crawlers dat ze alles mogen lezen
- `sitemap.xml` — de lijst van alle pagina's voor zoekmachines. **Nieuwe pagina? Dan hier ook toevoegen.**
- `llms.txt` — een korte samenvatting van Cletos voor AI-systemen, met links naar de pagina's. **Prijs of dienst gewijzigd? Dan hier ook bijwerken.**

Lokaal bekijken: open `index.html` in een browser.

## Iets aanpassen

Tekst wijzigen in de pagina, dan:
```bash
git add -A && git commit -m "Wat je veranderd hebt" && git push
```
Binnen een minuut staat het live.

## Hoe het live staat

- **GitHub Pages:** repo `streefkerkshipping/cletos-website` (publiek; nodig voor gratis Pages), branch `main`, map `/ (root)`, custom domain `cletos.nl`.
- **DNS bij TransIP** (Domeinen → cletos.nl → DNS). De schakelaar "TransIP-instellingen" moet **UIT** blijven, anders zet TransIP de oude regels terug.

  | Naam | Type | Waarde |
  |---|---|---|
  | `@` | A | `185.199.108.153` |
  | `@` | A | `185.199.109.153` |
  | `@` | A | `185.199.110.153` |
  | `@` | A | `185.199.111.153` |
  | `www` | CNAME | `streefkerkshipping.github.io.` |

Controleren:
```bash
dig +short @ns0.transip.net cletos.nl A          # moet de vier 185.199-adressen geven
gh api repos/streefkerkshipping/cletos-website/pages --jq .https_certificate.state
```

## Nog te doen

- [ ] HTTPS-certificaat afwachten, daarna "Enforce HTTPS" aanzetten: `gh api -X PUT repos/streefkerkshipping/cletos-website/pages -F https_enforced=true`
- [ ] btw-id in de footer invullen op alle pagina's (wettelijk verplicht; nu "btw-id volgt")
- [ ] Lettertypes zelf hosten in `assets/fonts/` in plaats van via Google Fonts (dan gaat er geen verzoek naar Google en klopt de privacyzin in de footer volledig)
- [ ] Automatisch verlengen van cletos.nl aanzetten bij TransIP
