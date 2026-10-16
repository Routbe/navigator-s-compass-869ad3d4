# Plan: verbeterpunten ROUT (design, admin, e-mail, scrollen)

## Eerst: de ROUT-code moet blijvend in dit project staan
De ROUT-bestanden zijn opnieuw verdwenen uit dit project (alleen het lege startsjabloon staat er). Voordat iets hieronder kan, zet ik de code terug op een manier die blijft bewaren (bestand per bestand opslaan in plaats van in één keer kopiëren), en controleer ik bij elke volgende stap dat ze er nog staan.

## 1. Design-editor
- **Achtergrond & Visual FX**: ROUT-presets veel kleiner maken; op mobiel standaard een raster van 4 per rij, inklapbaar.
- **Knoppen & Typografie**: dezelfde "aanpassen"-knop per onderdeel als bij Achtergrond.
- **Hoekafronding**: opties die er hetzelfde uitzien vervangen door duidelijk verschillende stappen (scherp, licht, middel, rond, pil), met een voorbeeldje per optie.
- **Knopstijl & vorm**: opties zonder zichtbaar verschil samenvoegen of aanpassen. Nieuwe keuze: knop als **ronde bol (alleen icoon)** of **balk met naam**. Bij de bol blijft de naam voor schermlezers bestaan, en verschijnt bij het kiezen een melding dat dit minder duidelijk is voor slechtzienden.
- **"Made with ROUT"-voetnoot**: standaard aan. Pro-leden kunnen hem uitzetten; Pro geldt voor alle profielen van een geverifieerde gebruiker, niet per profiel apart.

## 2. Inlogmail naar @rout.be-adressen komt niet aan
- Uitzoeken waarom: waarschijnlijk wordt de mail vanaf hallo@rout.be naar hetzelfde domein gestuurd en daar tegengehouden, of klopt de domeininstelling niet. Ik controleer de verzendlogboeken en de domeinstatus.
- Verzenden via een apart afzendadres (bijv. noreply@notify.rout.be) zodat @rout.be-ontvangers wel mail krijgen, zowel bij gewone login als bij admin-login.

## 3. Admin-portaal
- **Schermen openen volledig zonder zijbalk** (Verificaties & aanvragen, Cadeaubonnen): binnen de normale admin-indeling met zijbalk tonen.
- **Verificaties & aanvragen**: tabbladen *Nieuw*, *In behandeling*, *Goedgekeurd*, *Afgewezen/mislukt*, met wie de aanvraag deed en wanneer.
- **OAuth-apps verifiëren**: dezelfde indeling met statussen; afgehandelde apps verplaatsen naar hun eigen tab in plaats van bovenaan te blijven staan.
- **Cadeaubonnen**: knop "Cadeaubon aanmaken" (bedrag of Pro-duur, aantal, vervaldatum), met kopieerbare codes.
- **"Publiek profiel"-link**: altijd naar rout.be/gebruiker, niet naar rout.dlp.li.
- **Mede-admins**: de admin-rol wordt nu niet goed opgeslagen bij de login, waardoor ze niet binnen kunnen. Admin-rol op één veilige plek in de database bewaren, server-zijdig controleren, en alleen bestaande admins mogen admins toevoegen of verwijderen (met logboek).

## 4. Eigen badges
- Uploads met transparante achtergrond (PNG/WebP/SVG) behouden; geen witte achtergrond meer toevoegen. Voorbeeld op een geblokte achtergrond.

## 5. Kleine ergernissen: scrollen
- Profiel hub: bij het openen/sluiten van een map blijft de pagina op dezelfde plek, het geopende onderdeel blijft in beeld.
- Bij het sluiten van een pop-up springt de pagina niet meer naar boven.
- Ook de rest van de editor en het admin-portaal nalopen op hetzelfde soort sprongen.

## Controle
Typecontrole en alle tests draaien; nieuwe tests voor: voetnoot standaard aan, Pro geldt voor alle profielen, alleen admins kunnen admins maken, profiel-link gebruikt rout.be. Daarna in de preview ingelogd doorlopen.

## Technische details
- Admin-rol: aparte rollentabel + server-check i.p.v. veld op het gebruikersprofiel; Better Auth-sessie leest de rol uit de database.
- Scrollen: `preventScrollReset`/focus-herstel bij dialogen uitzetten, `scroll-margin` + `scrollIntoView({block:"nearest"})` bij accordeons.
- Publieke URL uit één instelling (canonieke site-URL) halen.
