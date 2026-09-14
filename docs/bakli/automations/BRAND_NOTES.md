# Bakli automatizacijos · 2026-09-11

## Lokalizuotų vaizdo pataisų užklausos

Naudotas integruotas `image_gen` įrankis. Abu rezultatai išsaugoti `bakli/automations/heroes/feedback-20260911/` kaip `phone-personalized.jpg` ir `scent-personalized.jpg`.

Telefono užklausa:
```text
Use case: precise-object-edit. Edit target: the attached official Bakli product photograph. Make ONE very localized change: add the small, elegant, readable initials "A. M." laser-engraved into the upper-middle blank cognac leather area, below the camera and above the thumb. The lettering follows the angle and perspective of the phone, dark brown recessed laser marks, modest size but visible in a 600px email. Preserve exactly the existing official photo: phone and case geometry, camera lens count and positions, black rim, the original Bakli logo near the bottom, hand, fingernails, all edges, shadows, lighting, leather texture, beige background and square crop. Do not regenerate or redesign the product. No other text, decoration, hearts, packaging or added objects. Output one square product photograph at high resolution.
```

Automobilio kvapo užklausa:
```text
Use case: precise-object-edit. Edit target is the attached official Bakli leather car fragrance photograph. Add only the small readable Lithuanian personalization "Gero kelio!" laser-engraved in dark brown into the blank leather area ABOVE the existing Bakli logo, centered on the leather rectangle. Align the words to the rectangle perspective and camera angle. The lettering must look recessed into real leather. Preserve the complete original Bakli logo and all its lettering exactly unchanged. Preserve EXACTLY the product rectangle and dimensions, border embossing, leather color and texture, cord, hole, bottle shape and size, black dropper, box, paper, background, shadows and square crop. Do not redesign or invent products or accessories. Only add the personal engraving; nothing else.
```

Peržiūrėti 6 flow: Welcome (3 laiškai, atskira privati `elaiskai/bakli` repozitorija), krepšelis (3), checkout (2), naršymas (2 ir ankstesnis variantas), po pirkimo (3 ir suderinamumo kopija), winback (2).

Pataisos pagal kliento komentarus:
- Welcome navigacija ir personalizavimo CTA veda į https://www.bakli.lt/lt/populiariausios-prekes.
- Dovanų hero matomas tikras Scott pakabuko graviravimas. Kiti anksčiau generuoti produktų hero pakeisti oficialiomis Bakli nuotraukomis.
- Telefono dėklui pridėti inicialai „A. M.“, automobilio kvapui – „Gero kelio!“. Abu yra personalizavimo maketo pavyzdžiai, paremti tikromis produkto nuotraukomis, redaguoti integruotu image_gen įrankiu. Tai nėra naujos produkto fotografijos.
- Odos priežiūros hero ir CTA veda į https://www.bakli.lt/lt/iki-30-eur/bakli-balzamas-odos-gaminiu-prieziurai-250ml. Paminėta, kad balzamas tinka lygiai odai; netinka veliūrui, zomšai, nubukui ir verstai odai, kaip nurodyta produkto puslapyje.
- Pašalintas atsiliepimo prašymas iš priežiūros laiško. Ankstesnis trečiasis atsiliepimo laiškas pakeistas dovanų idėjų laiško kopija; pagrindinis failas `03-atraskite-daugiau.html`. Atsiliepimo užklausą siunčia TVS.
- Sutvarkytas flow sąrašas: įtrauktas winback ir nuoroda į Welcome, pataisytos pasenusios antraštės.

Nuotraukų šaltiniai (tikrinta 2026-09-11):
- https://www.bakli.lt/lt/50-70-eur/marco-pinigines-ir-scott-pakabuko-rinkinys – 7-oji galerijos nuotrauka, tikra žinutė ant pakabuko.
- https://www.bakli.lt/lt/dovanos-moterims/telefono-deklas-crazy-horse – 2-oji galerijos nuotrauka, pridėti inicialai.
- https://www.bakli.lt/lt/dovanos-vyrams/pinigines-jacob-crazy-horse-su-spaude-ir-odinio-automobilio-kvapo-rinkinys – 4-oji galerijos nuotrauka, pridėta žinutė.
- https://www.bakli.lt/lt/iki-30-eur/bakli-balzamas-odos-gaminiu-prieziurai-250ml – originalus 250 ml produkto vaizdas.
- Piniginių ir pakabukų kategorijų originalai iš esamo Welcome paketo: `95d9c31f1c22f62c3c2c58c57f782d99-500x500-maxq.jpg` ir `a372aa0f952b42d908eb2107dd4519cd-500x500-maxq.jpg`.

Failai yra GitHub peržiūros ir importo šaltiniai. Šiuo darbu Omnisend automatizacijos nekeičiamos. Dinaminius krepšelio, checkout ir peržiūrėto produkto blokus bei jų paskirties nuorodas užpildo esama Omnisend integracija. Welcome teisinį footerį ir atsisakymą prideda Omnisend wrapper. Naujų hero nuorodos susietos su konkrečiu viešos vaizdų repozitorijos commit.

## 2026-09-11 patikra

17 HTML failų (15 pagrindinių laiškų ir 2 ankstesni variantai) patikrinti naršyklėje 600 ir 390 px pločiuose: 0 trūkstamų vaizdų, 0 horizontalaus slinkimo. Welcome preflight: 169/169. Vizualiai peržiūrėtas dovanų graviravimas, telefono inicialai, automobilio kvapo žinutė bei balzamo blokas. Po pirmos peržiūros balzamo vaizdas sumažintas iki 440 px ir patikrintas pakartotinai. Visuose siunčiamuose failuose vaizdų adresai yra HTTPS; personalizavimo CTA nevartoja informacinės kategorijos, atsiliepimo CTA pašalinti. ZIP atnaujintas su HTML peržiūromis; Omnisend siuntimas ar live flow pakeitimai neatlikti.
