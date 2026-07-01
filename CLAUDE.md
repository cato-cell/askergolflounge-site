# Asker Golf Lounge – statisk nettside

## Hva dette er
askergolflounge.no er en statisk markedsførings- og bookingside for en privat, premium golfsimulator-lounge i Heggedal. Målet er å konvertere besøkende til bookinger via SimplyBook, og til kontakt for bedrift/samarbeid. Siden er både forretningsflate og en del av mediemerkevaren Asker Golf Lounge.

- Booking: alle «Book tid»- og pris-CTA-er peker til https://askergolflounge.simplybook.it
- Kontakt bedrift/samarbeid: skjema på forsiden via Web3Forms
- Posisjonering: privat premium lounge – IKKE et travelt simulatorsenter. «Hele loungen er din.»

## Teknisk stack og deploy
- Ren statisk HTML/CSS. Ingen rammeverk, ingen byggesteg. CSS og JS ligger inline i hver HTML-side (liten inline `<script>`: sticky nav, mobilmeny, reveal-on-scroll, fetch for kontaktskjema).
- GitHub-repo: cato-cell/askergolflounge-site → Cloudflare Pages.
- Cloudflare: production branch = main, build command = tom, output directory = /. Hver commit til main auto-deployer på ~30 sek.
- DNS på Cloudflare (nameservere: annabel/jay.ns.cloudflare.com). Canonical bruker www: https://www.askergolflounge.no/
- WordPress-hostingen beholdes KUN som fallback til den statiske stacken er bekreftet stabil. Ikke bygg noe nytt på WordPress.
- Bruk ROT-ABSOLUTTE stier på delte ressurser (/logo.png, /lounge-scaled.jpg osv.) så undersider funker.
- `.assetsignore` i rota holder denne CLAUDE.md ute av offentlig deploy (fila ligger i git, men serveres ikke på nett).

## Filer
- index.html – forsiden. All CSS ligger inline i én `<style>` i `<head>` (ca. linje 21–1671). Det finnes INGEN separat/ekstern CSS-fil.
- personvern.html → /personvern – GDPR-personvernerklæring (norsk)
- bookingvilkar.html → /bookingvilkar – bookingvilkår (norsk)
- 404.html – egendefinert 404-side (noindex)
- sitemap.xml, robots.txt
- Bilder i rota: lounge-scaled, 1-scaled, 2-scaled, 5-scaled, 6-scaled (hver som .jpg + .webp), chatgpt-image-5-apr-2026-18-44-06 (.png + .webp), logo.png, favicon.png
- pack/ – merkevarepakke (emblem/, full-logo/, icons/, social/), ikke referert fra sidene
- README.md, CLAUDE.md (sistnevnte ekskludert fra deploy via .assetsignore)
- MERK om «delt design»: nav, footer og designtokens er IKKE i én felles fil. Hver HTML-side har sin egen inline `<style>`; undersidene har i tillegg side-scopede stiler (.juridisk på personvern/bookingvilkar). Endres et delt element (nav/footer/tokens) må det oppdateres i HVER fil.

## Designsystem
- Uttrykk: mørk (near-black bakgrunn), premium, stilren, sportslig uten å være aggressiv, mobil-først. Én tydelig hovedhandling per seksjon.
- Sterke ekte bilder fra lounge/golf/produksjon prioriteres over stockbilder.
- Tydelig typografi, god kontrast, mye luft, få konkurrerende knapper.
- Unngå: for mange effekter, overdreven gull, mange fonter, små tekster, template-følelse.
- Designtokens (fra `:root` i index.html linje 27–41, og `#agl` linje 106):
  - Bakgrunn: `#05070b` (primær, near-black) og `#0b0f16` (sekundær/panel). Panel-flate `rgba(255,255,255,0.05)`, panel-kant `rgba(255,255,255,0.08)`.
  - Tekst: `#ffffff` (primær), `rgba(255,255,255,0.74)` (dempet).
  - Aksent: `#138A52` og `#1FB069` – begge GRØNNE. Soft: `rgba(19,138,82,0.16)`. NB: CSS-variablene heter `--agl-blue` / `--agl-blue-2` / `--agl-blue-soft`, men verdiene er grønne – ikke la navnet lure deg.
  - Radius: `18px` (`--agl-radius`). Maks innholdsbredde: `1200px` (`--agl-wrap`). Skygger: `--agl-shadow` / `--agl-shadow-strong`.
  - Font (display OG brødtekst): `-apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif` (systemstack, satt på `#agl`). Ingen web-font og ingen egen display-font; overskrifter skiller seg kun via størrelse/vekt/letter-spacing.

## Innholds- og språkregler
- Språk: norsk bokmål. Tone: personlig, direkte, troverdig, gjerne humoristisk – høres ut som Cato, ikke som et reklamebyrå.
- Forbudt: konsulentspråk, kunstige superlativer, generiske AI-klisjeer («magisk», «unik reise», «løfter opplevelsen» o.l.).
- All norsk tekst kvalitetssjekkes for særskriving/orddeling, bindestrek og staving før commit.

## Priser (ENESTE gyldige tall – live i SimplyBook)
- Ukedag (man–fre): 390 kr per time
- Helg (lør–søn): 490 kr per time
- Med coach: 690 kr per time (1 time med coaching)
- Køllelån er ALLTID inkludert.
- Leie til andre formål (filming, podcast, foto, arrangement): «ta kontakt for pris» – ingen fast tall på siden.
- Kapasitet: opptil 4 personer, helt privat i hele den bookede perioden.

## Booking
- System: SimplyBook.me (askergolflounge.simplybook.it), Basic-plan (årlig, 3 egendefinerte funksjoner, 100 bookinger/mnd).
- Tjenester: Leie 1 time man–fre (390), Leie 1 time lør–søn (490), Leie 1 time med Coaching (690). 2-timers via Service Add-ons.
- Kalender står på «Fleksibel» (daglig) visning for bedre mobil-UX på helgeslots.
- Avbestilling: gratis frem til 24 timer før booking.
- Betaling: kort og Vipps avtales ved kontakt. Vipps/Stripe via Accept Payments er IKKE koblet i SimplyBook ennå.

## Relaterte systemer
- E-postmarkedsføring: Brevo (delt konto med FinnOss.no – hold kampanjer og avsenderidentiteter STRENGT adskilt). Inneholder 254 historiske Amelia-kontakter, norsk 8-sifret SMS-format.
- Kontaktskjema: Web3Forms.
- E-post: Google Workspace (cato@askergolflounge.no).

## Faste fakta (footer/kontakt)
- Adresse: Heggedal Torg 18, 1389 Heggedal (gratis parkering rett utenfor)
- Telefon: +47 41 24 00 24
- E-post: cato@askergolflounge.no
- Foretak: Asd Media & Produktion AS · org. nr. 916 585 993 (overgang til NextNova planlagt – oppdater når endelig)
- Åpningstider: man 13–22 · tir 10–20 · ons 14–22 · tor 10–22 · fre 12–22 · lør 10–22 · søn 14–22
- LocalBusiness JSON-LD med disse åpningstidene ligger på forsiden.

## Forsidens seksjoner (faktisk rekkefølge og ankere i index.html)
Header (logo → #top + nav: Opplevelsen #why · Teknologi #tech · Galleri #gallery · Eksklusiv leie #leie · Priser #priser · Kontakt #kontakt · Book tid → #priser)
1. Hero #top («Hele loungen er din» + Book tid + Se loungen)
2. #why – «Hvorfor velge oss / Derfor velger folk Asker Golf Lounge» (3 punkter: 100 % privat / premium omgivelser / enkelt fra første steg)
3. (uten id) – «Opplevelsen / Mer enn bare simulator»
4. #tech – «Teknologi / Utstyr som løfter opplevelsen» (stats: 4K-visning / 4,30 m lerret / GCQuad)
5. #gallery – «Detaljene / Premium i hver detalj» (galleri-seksjon; nav-punktet «Galleri» peker HIT)
6. #leie – «Ekstra muligheter / Loungen kan også brukes til mer» (podcast/film/foto/arrangement)
7. #priser – «Priser / Tydelige priser. Enkelt valg.» (3 kort → SimplyBook)
8. #faq – «Spørsmål og svar / Ofte stilte spørsmål»
9. #kontakt – «For bedrifter og samarbeid» (Web3Forms-skjema)
10. #kontaktinfo – «Kontakt / Asker Golf Lounge» (adresse/e-post/telefon/åpningstider). Footer-lenkene (Personvern · Bookingvilkår) ligger nederst i denne seksjonen.
MERK: #kontakt = bedrift/samarbeid-skjemaet, IKKE den generelle kontaktinfoen (som er #kontaktinfo). Det finnes ingen egen «Galleri»-tittel – #gallery er seksjonen «Detaljene / Premium i hver detalj».

## Status (repo-tilstand pr. nå)
- [x] Statisk stack live på Cloudflare Pages, DNS migrert
- [x] Forside med alle hovedseksjoner over
- [x] /personvern, /bookingvilkar, 404, sitemap.xml, robots.txt
- [x] LocalBusiness JSON-LD, unike metatitler + canonical, lazy-loading (ikke-hero), WebP-bilder
- [x] Bedrift/samarbeid-kontaktskjema via Web3Forms
- [x] SimplyBook-kalender på «Fleksibel» visning
- [x] 254 kontakter importert til Brevo (norsk SMS-format, 1 dansk kontakt utelatt fra SMS-fil)
- [ ] Verifisere e-postlevering til cato@askergolflounge.no + bekrefte at www er aktiv i Pages
- [ ] Helge-add-on «1 time ekstra helg» (490 kr) koblet KUN til lør–søn-tjenesten
- [ ] Koble Vipps/Stripe via Accept Payments
- [ ] Re-engasjementepost til gamle Brevo-kontakter (start fersk – IKKE fra FinnOss-mal)
- [ ] Sjekke at Google Workspace-fakturering er separat fra Webhuset-hosting før kansellering
- [ ] Kansellere WordPress-hosting når stacken er bekreftet stabil
- [ ] Evt. cookie consent-banner (bookingwidget laster tredjepartsskript)

## Merkevare / medieplattform (kontekst)
- Etablert i norsk golfmiljø: YouTube 1500+ abonnenter (1M+ visninger), TikTok 5000, Instagram 600.
- Personlig merkevare rundt Cato. Michael (Catos sønn) var med i de tidligste YouTube-filmene, er lite involvert nå, kan komme inn igjen senere – ikke del av kjernemerkevaren nå.
- Den fysiske loungen beholdes som fullverdig del av konseptet (ingen aktiv salgsvinkling).

## Arbeidsmåte
Konklusjon først, korte og konkrete svar, én oppgave av gangen. Lever komplett kode/prompt i én klipp-og-lim-boks – aldri stykkevis. Foreslå enklere løsning når den finnes. Ikke endre fungerende løsninger uten grunn. Commit til main når en endring er ferdig (det deployer siden).
