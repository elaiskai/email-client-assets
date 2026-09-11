# Imunicija · winback · 10 € sugrįžimo bonusas

Atnaujinta 2026-09-11 pagal užduotį: abu esami winback laiškai papildyti asmeniniu 10 € sugrįžimo bonusu. Išlaikytas esamas maketas, logotipas, Montserrat / Roboto su Arial pakaitalais, #20b200, #333333 ir 600 px plotis. Bonusui pritaikytas #eaf4e4 fonas.

## Failai ir būsena

- `01-naujos-prekes.html` — pirmas laiškas po 90 d. be pirkimo; tema „Jums — 10 € sugrįžimo bonusas“.
- `02-parduokite-sena.html` — antras laiškas po dar 30 d.; tema „Atnaujinkite įrenginį su 10 € bonusu“.
- To paties pavadinimo `.txt` failai — tekstinės peržiūros.
- `bonus-before-code.html` ir `bonus-after-code.html` — tik bonuso HTML fragmentai jau surinktiems Omnisend laiškams.
- Peržiūros — `../_qa/*-bonus-600.png` ir `../_qa/*-bonus-390.png`.

**Pilni HTML ir TXT failai yra peržiūros. `XXXX-XXXX-XXXX` nėra aktyvus kuponas ar dinaminė žyma. Vien importuotas HTML negeneruoja kodų. Omnisend ar WooCommerce paskyra šiuo pakeitimu nekonfigūruota.**

Esamos produkto kortelės yra dinaminio rekomendacijų bloko peržiūros pavyzdžiai; kainos ir likučiai šio pakeitimo metu neatnaujinti. Omnisend laiškuose išlaikykite esamus natūralius produktų blokus.

## Įdėjimas į esamus Omnisend laiškus

Abiejuose **winback automatizacijos** laiškuose po įžangos įdėkite šiuos tris blokus:

1. Custom HTML su `bonus-before-code.html` turiniu.
2. Natūralų **Unique Discount** bloką.
3. Custom HTML su `bonus-after-code.html` turiniu.

Pilno maketo komentaruose `OMNISEND_UNIQUE_DISCOUNT_START` / `END` pažymėta kodo pavyzdžio vieta. Jos nereikia kopijuoti į siunčiamą laišką. HTML fragmentai jau turi subalansuotas lenteles ir neturi dokumento `head` / `body` žymų. CTA „Panaudoti 10 € bonusą“ jau yra apatiniame fragmente; natūraliame nuolaidos bloke išjunkite dubliuojamą CTA.

Unique Discount nustatymai:

- Cart discount → Fixed amount → **10**. Parduotuvės valiuta turi būti EUR.
- Įjungti **Reuse unique discount code in this workflow** abiem laiškams.
- Pasirinkti realų galiojimo laiką pagal parduotuvės pasiūlymo taisykles. Laiškus skiria 30 dienų: jei kodas tuo metu nebegalioja, Omnisend gali sugeneruoti naują.
- Minimali suma, taikymas akcijinėms prekėms ir derinimas su kitomis nuolaidomis nebuvo nurodyti; naudoti tik parduotuvės patvirtintas sąlygas. Makete šių pažadų nėra.
- Kodo sritis: #eaf4e4 fonas, tamsus #333333 tekstas, Montserrat / Arial, apie 20–23 px. Mobiliajame plotyje kodas turi tilpti vienoje eilutėje.

Jei unikalūs kuponai dar neįgalinti, WooCommerce Omnisend įskiepyje reikia atlikti „Enable unique discounts“ prijungimą. Automatizacijoje natūralus blokas sugeneruoja atskirą kodą gavėjui; įprasto kampanijos siuntimo elgsena skiriasi. Testiniuose laiškuose gali likti kodo pavyzdys — tai nepatvirtina kupono sukūrimo.

Šaltiniai, patikrinti 2026-09-11: [Omnisend: WooCommerce unique discounts](https://support.omnisend.com/en/articles/5846981-woocommerce-add-configure-discount-item), [Custom HTML item](https://support.omnisend.com/en/articles/1061866-add-configure-custom-html-item).

## Patikra prieš aktyvavimą

Per Omnisend / WooCommerce patikrinti dviejų testinių kontaktų atskirus kuponus, 10 € sumą atsiskaityme ir kodo pakartotinį naudojimą tame pačiame sraute. Sutvarkyti gavėjų išėjimą iš srauto po pirkimo. Realūs laiškai šios užduoties metu nesiųsti.

## Atlikta maketo patikra

Abu laiškai naršyklėje patikrinti 600, 390 ir 320 px pločiais: horizontalios slinkties nėra, paveikslėliai įkeliami. Peržiūrėjus desktop ir mobile vaizdus sumažinti vidiniai bonuso kortelės tarpai. Kodo pavyzdys telpa vienoje eilutėje. Tai HTML peržiūros patikra; tikro kupono sukūrimas ir atsiskaitymas dar netikrinti.
