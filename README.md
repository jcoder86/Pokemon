# Julian's Pokemon

Een vrolijk, tekstloos Pokémon-achtig verzamelspel voor Julian (5 jaar): vijf gebieden (weide-hub, jungle met lantaarntjes, dorp/boerderij, strand met palmen en zee, besneeuwde bergen), 150 in code getekende wezentjes (compleet, net als generatie 1), beurtgevechten met type-aanvallen, een mik-vangspel, een bootje en een verzamelboek waarin je je actieve metgezel kiest. Alles zit in één bestand (`index.html`) met `start.png` (startscherm) en `icon.png` (app-icoon) als enige afbeeldingen. Volledig offline speelbaar in Safari op iPad, landscape.

- **Starten:** `START` = Julians blijvende profiel; `Start as guest` = los gast-geheugen.
- **Lopen/varen:** tik ergens — Julian loopt erheen en stapt aan de waterlijn vanzelf in/uit het bootje.
- **Reizen:** vanuit de weide-hub gaan vier poorten naar de andere gebieden — rotspoort links (jungle), houten poort boven (dorp), ijspoort rechts (besneeuwde bergen) en palmpoort onder (strand). Elk gebied heeft dezelfde poort terug.
- **Wie woont waar:** de 150 wezentjes zijn over de vijf gebieden verdeeld op thema, en verschijnen op zeldzaamheid — kleine wezentjes vaak, imposante zelden en de legendes bijna nooit.
- **Vechten:** het actieve wezentje (kies in het boek, groene gloed = actief) valt aan met de 💥-knop. Mik met de ring: klein = raak, allerkleinst (goud) = dubbele klap. Vangen gaat met hetzelfde mik-spelletje zodra de hartjes leeg zijn; vluchten kan altijd met 🏃.
- **Flauwvallen:** raken de hartjes van je maatje op, dan gaat het slapen en opent het boek zodat Julian meteen een ander wezentje kiest. Na het gevecht is de slaper weer helemaal fit. Elk wezentje vecht met het aantal hartjes dat het zelf heeft.
- **Boek in het gevecht:** de 📖-knop werkt ook tijdens een gevecht.

## Lokaal openen

Open een terminal in deze map en start een simpele webserver, bijvoorbeeld in PowerShell:

```
python -m http.server 8000
```

Ga daarna in de browser naar `http://localhost:8000`. (Direct dubbelklikken op `index.html` werkt meestal ook, maar via een server laden manifest en iconen netjes mee.)

## Deploy (productie)

Productie draait via **Dokploy** op de VPS: koppel deze GitHub-repo als service, Dokploy bouwt de `Dockerfile` (nginx:alpine, statische bestanden) en draait de container met host-poort **3010** → container-poort 80 (zie `docker-compose.yml`). Zet er in Dokploy een subdomein voor en het spel is bereikbaar; op de iPad daarna via Safari → deelknop → **"Zet op beginscherm"** voor een fullscreen app met eigen icoon.

## Bestanden

- `index.html` — het volledige spel (alle code inline)
- `start.png` — startscherm-artwork
- `icon.png`, `icon-512.png`, `apple-touch-icon.png`, `manifest.json` — app-icoon en web-app-manifest
- `Dockerfile`, `docker-compose.yml`, `.dockerignore` — deploy-artifacts
- `assets/julian-avatar.svg` — avatar van Julian, afgeleid van het aangeleverde artwork
