# Julian's Pokemon

Een vrolijk, tekstloos Pokémon-achtig verzamelspel voor Julian (5 jaar): vijf gebieden (weide-hub, jungle met lantaarntjes, dorp/boerderij, strand met palmen en zee, besneeuwde bergen), 150 in code getekende wezentjes (compleet, net als generatie 1), beurtgevechten met type-aanvallen, een mik-vangspel, een bootje en een verzamelboek waarin je je actieve metgezel kiest. Alles zit in één bestand (`index.html`) met `start.png` (startscherm) en `icon.png` (app-icoon) als enige afbeeldingen. Volledig offline speelbaar in Safari op iPad, landscape.

- **Starten:** `Julian` (groen) = Julians vaste profiel. `GUEST` (erboven, even groot) opent één tussenscherm met links de lopende spellen als langwerpige tegeltjes (avatar, naam en aantal gevangen wezentjes) en rechts het aanmaken van een nieuw spel: kies daar een hoofdpersoon en vul een naam in. Een nieuw spel begint altijd vers. Elk spel bewaart onder zijn eigen sleutel, dus meerdere kinderen kunnen op hetzelfde apparaat spelen zonder elkaars voortgang te raken. Een bestaand gast-spel van vroeger komt automatisch in de lijst als "Gast".
- **Lopen/varen:** tik ergens — Julian loopt erheen en stapt aan de waterlijn vanzelf in/uit het bootje.
- **Reizen:** vanuit de weide-hub gaan vier poorten naar de andere gebieden — rotspoort links (jungle), houten poort boven (dorp), ijspoort rechts (besneeuwde bergen) en palmpoort onder (strand). Elk gebied heeft dezelfde poort terug.
- **Moeilijkheid:** elk gastspel heeft een niveau — **Makkelijk** (het spel zoals het altijd was, en de standaard voor Julians profiel), **Gewoon** of **Moeilijk**. Je kiest het bij het aanmaken van een spel en past het later aan met het gekleurde chipje op het tegeltje in het spelersscherm. Wat er verandert:

  | | Makkelijk | Gewoon | Moeilijk |
  |---|---|---|---|
  | mikring per ronde | 1,85 s | 1,37 s | 1,06 s |
  | venster dubbele klap | 0,26 s | 0,19 s | 0,15 s |
  | ballen per gevecht | onbeperkt | 5 | 3 |
  | maatjes per gevecht | onbeperkt | 4 | 3 |
  | slaap na flauwvallen | tot het eind van het gevecht | 1 gevecht | 3 gevechten |
  | extra hartjes tegenstander | – | 0–1 | 1–2 |
  | kans op dubbele klap tegenstander | – | 13 % | 26 % |
  | zeldzame wezens | normaal | schaarser | het schaarst |

  Raken de ballen op, dan huppelt het wezentje weg en ga je zonder vangst naar buiten. Zijn alle maatjes op, dan trekt Julian zich terug. Geen van beide is een game over: je loopt gewoon weer verder. Het spel zorgt er altijd voor dat er minstens één maatje wakker is.
- **Wie woont waar:** de 150 wezentjes zijn over de vijf gebieden verdeeld op thema, en verschijnen op zeldzaamheid — kleine wezentjes vaak, imposante zelden en de legendes bijna nooit.
- **Vechten:** het actieve wezentje (kies in het boek, groene gloed = actief) valt aan met de 💥-knop. Mik met de ring: klein = raak, allerkleinst (goud) = dubbele klap.
- **Krachtaanval:** de meeste wezentjes (alles met vier of meer hartjes, plus een reeks bekende kleintjes — 117 van de 150) hebben een tweede aanval op de paarse 🌟-knop. Dat is dezelfde aanval als de gewone, maar dan in bulk en van boven naar beneden: een regen van elf projectielen die op de tegenstander inslaat. Altijd twee hartjes, maar de mikring raast twee keer zo snel — moeilijker te raken, en zonder dubbele-klap-bonus. De twee aanvalsknoppen staan naast elkaar onder Julians eigen wezentje. Vangen gaat met hetzelfde mik-spelletje zodra de hartjes leeg zijn; vluchten kan altijd met 🏃.
- **Flauwvallen:** raken de hartjes van je maatje op, dan gaat het slapen en opent het boek zodat Julian meteen een ander wezentje kiest. Na het gevecht is de slaper weer helemaal fit. Elk wezentje vecht met het aantal hartjes dat het zelf heeft.
- **Boek in het gevecht:** de 📖-knop werkt ook tijdens een gevecht.
- **Knoppen rechtsboven:** 📖 het boek (groot), daaronder 🏠 terug naar het startscherm (lichtrood, klein — bewaart eerst de voortgang) en 🔊 het geluid (even klein).
- **De hoofdpersonen:** alle vier de aanzichten (voor, achter, beide zijkanten) zijn opgebouwd naar het startscherm-artwork, met verlopen in plaats van vlakke kleurvlakken, weefsel- en leertextuur, haarslierten en tapse contourlijnen. LivEa deelt dezelfde bouw en maatvoering en verschilt in palet, blond lang haar met een staart en een strikje. Van achteren valt haar haar over nek en bovenrug, dus die zie je niet en de rugzak zit eronder.

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
- `herstel.html` — controle- en herstelpagina: toont per opgeslagen spel hoeveel wezentjes erin zitten, kan voortgang van het ene blok naar het andere kopiëren en alles veiligstellen als tekst. Open haar op hetzelfde adres als het spel, anders leest ze een andere opslag.
- `start.png` — startscherm-artwork
- `icon.png`, `icon-512.png`, `apple-touch-icon.png`, `manifest.json` — app-icoon en web-app-manifest
- `Dockerfile`, `docker-compose.yml`, `.dockerignore` — deploy-artifacts
- `assets/julian-avatar.svg` — avatar van Julian, afgeleid van het aangeleverde artwork
