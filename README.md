# Hospitality-beregnere

Samling af selvstændige, indlejrbare beregnere til restaurant-/hotelkunder (hospitality). Hver beregner er én selvstændig HTML-fil uden eksterne afhængigheder (ingen CDN-scripts, ingen fonts, ingen API-kald) — klar til at blive limet ind i et CMS' HTML-blok.

© Steen Olesen — steenolesen.com. Brug uden tilladelse er ikke tilladt.

## Beregnerne

| Mappe | Beregner | Hvad den viser |
|---|---|---|
| `cltv/` | Kundens livstidsværdi | CLTV ud fra ordreværdi, købsfrekvens og kundeforholdets længde |
| `leadvalue/` | Værdien af dine leads | Omregner lead-volumen og konvertering til kroneværdi pr. lead |
| `breakup/` | Break Up-beregneren | Omsætning i risiko ved kundeafgang/churn (stamkunder vs. engangskunder) |
| `evc/` | Værdien af 1 e-mail | Værdien af én e-mailadresse i databasen |
| `fpl/` | Løftestangen — Vækstrapport | Samlet vækstrapport der kombinerer flere håndtag (konvertering, avance, transaktioner, loyalitet) |
| `mersalg/` | Mersalgsberegneren | Ekstra profit ved at indføre et mersalgstilbud |
| `mgc/` | Avance-beregner | Sammenligning/beregning af bruttoavance |

Mapperne `cltv/` og `leadvalue/` har både `index.html` (embed-versionen) og `preview.html` (fuld side, bruges til udvikling/gennemsyn — indeholder samme widget, bare med egen `<head>`/side-styling i stedet for at være pakket som indsætbart snippet).

## Se en beregner lokalt

Ingen build nødvendig — åbn filen direkte i browseren:

```bash
open cltv/index.html
```

Eller kør en simpel lokal server hvis du vil teste relative stier/CORS-adfærd:

```bash
npx serve .
```

## Sådan indlejres en beregner

Hver `index.html` er skrevet til at kunne indsættes direkte i et CMS-felt der accepterer rå HTML/kode (fx en "custom HTML"-blok i WordPress, Webflow, HubSpot m.fl.):

1. Åbn den relevante `index.html`.
2. Kopiér hele filens indhold.
3. Indsæt det i CMS'ets HTML-blok på siden, hvor beregneren skal vises.

Når en beregners domæne er whitelistet (se domain-lock nedenfor), kan embed i stedet ske via en `<iframe>` der peger på den hostede URL — så opdateres alle indlejringer automatisk, uden manuel copy-paste, når filen ændres.

## Domain-lock

Hver beregners script tjekker `window.location.hostname` mod en indbygget whitelist. På et ikke-godkendt domæne viser widgeten kun en byline ("Denne beregner er udviklet af Steen Olesen.") i stedet for selve beregneren — det er tilsigtet kopibeskyttelse, ikke en fejl. `detmindrebureau.dk` (og `localhost`) er bekræftet whitelistet i `cltv/` og `fpl/`; resten obfuskerer listen i scriptet, så tjek/udvid den pr. beregner før et nyt domæne (fx en GitHub Pages-URL eller en klients CMS-domæne) skal kunne vise widgeten.

## Status / hosting

Hostet via GitHub Pages: `https://steen-olesen.github.io/hospitality-beregnere/<mappe>/`. Bemærk domain-lock ovenfor — den rå GitHub Pages-URL virker kun hvis `steen-olesen.github.io` er whitelistet i den enkelte beregner.
