# KARPININKAMS.LT — automatizacijų srautai (HANDOFF)

**Statusas 2026-10-04:** 4 srautai / **9 laiškai**, copy įdėtas, QA švarus.
Welcome srautą (Flow 1) Lukas daro atskirai per ChatGPT - čia jo nėra.

**2026-10-04 Luko sprendimai:** nuolaidos kodas iš `cart-03` išimtas (klausimyne jo nebuvo),
po pirkimo palikti 2 laiškai (`post-03` lojalumas išimtas), **winback srautas ištrintas**,
`post-02` papildytas tiksliu atsiliepimo keliu. Viskas sukelta į repo `elaiskai/karpinkaireal`.

## ⚠️ Copy šaltinis

2026-09-28 `lt_copy.py` grąžino **401 `token_revoked`**, tad pagal 09-26 fallback taisyklę pirmąją copy
versiją parašė Claude Opus 5. **2026-10-04 Codex auth veikia** - `cart-03` ir `post-02` copy jau
pergeneruota per `lt_copy.py`. Likusius 7 laiškus galima pervaryti bet kada:

```bash
python3 _gen_copy.py                 # visi
python3 _gen_copy.py cart-02         # vienas
```

## Srautai

| Aplankas | Flow | Laiškų | Trigeris | Delay'ai |
|---|---|---|---|---|
| `02-cart/` | Apleistas krepšelis | 3 | Added product to cart | +1 val. / +8 val. / +24 val. |
| `03-checkout/` | Apleistas apmokėjimas | 2 | Started checkout | +45 min. / +12 val. |
| `04-browse/` | Naršymo apleidimas | 2 | Viewed product (inStock) | +3 val. / +2 d. (tik neatidariusiems) |
| `05-post-purchase/` | Po pirkimo | 2 | Order placed / fulfilled | iškart / +10 d. |

## Laiškų turinys

| Failas | Blokai | Nuolaida |
|---|---|---|
| `cart-01` | priminimas + krepšelis + CTA + pastaba | ne |
| `cart-02` | krepšelis + 4 patikinimo blokai + pagalbos blokas | ne |
| `cart-03` | tamsus hero + krepšelis + CTA + nuoroda į akcijas | ne |
| `checkout-01` | „liko tik apmokėjimas" + užsakymo prekės + CTA | ne |
| `checkout-02` | pagalba + Paysera/terminų blokai + kontaktai | ne |
| `browse-01` | peržiūrėta prekė + panašios prekės + pastaba apie likutį | ne |
| `browse-02` | tamsus hero + peržiūrėta prekė + panašios + pagalbos blokas | ne |
| `post-01` | padėka + užsakytos prekės + 4 lūkesčio blokai + kontaktai | ne |
| `post-02` | įvertinimo prašymas + 3 žingsnių panelė, **be CTA mygtuko** (spaudžiama pati prekė) | ne |

## Dizainas

FOX stilius pagal `brand.md`: fonas `#202020` / `#141414`, oranžinis `#F58C23`, Oswald (DIDŽIOSIOMIS) + Ubuntu.
Plotis `width:100%;max-width:600px`, breakpoint 620px. Patikinimo blokai mobile stack'inasi po vieną (`.stack`) —
patikrinta 375px playwright render'iu.

**Be logotipo, be footer'io, be paveikslų.** Omnisend logo ir footer prideda natyviai (CLAUDE.md 8 ir 9 taisyklės).
Hero paveikslų nėra - dizainas laikosi ant tipografijos. Codex auth 10-04 veikia, tad hero galima pridėti
per `gen_image.py`, bet **tik pagal „pagavai-paleisk" ribojimus** (jokios žuvies ant kranto).

Produktų blokai — Omnisend natyvūs, lokaliai rodomi kaip mock, push'inant įterpiami per markerius:
`<!--SPLIT:cart-->`, `<!--SPLIT:viewed-->`, `<!--SPLIT:popular-->` (`python3 _split_out.py`).

Merge tag'ai: `{{abandonedCheckoutUrl}}` (cart + checkout), `{{lastViewedProductUrl}}` (browse) —
abu patikrinti Pirk Patogiai srautuose.

## ⚠️ Turinio pastabos

- **`browse-02`** plane buvo numatytas kaip „ta pati prekė kitu kampu". Kadangi prekė dinaminė, copy negali
  kalbėti apie konkretų modelį, tad kampas pakeistas į pagalbą apsispręsti. Jei Eduardas norės konkretaus
  turinio, reikės siaurinti flow iki vienos kategorijos.
- **`post-02`** neturi CTA mygtuko sąmoningai: įvertinimo forma gyvena tos pačios prekės puslapyje, į kurį
  veda pats produktų blokas. Tikslus kelias (patikrinta gyvai 2026-10-04): prekės puslapyje skirtukas
  „Įvertinimai" -> forma „Parašyti įvertinimą" (žvaigždutės, vardas, tekstas) -> mygtukas „Tęsti".
  Registruotis nereikia. Atsiliepimų svetainėje vos keli, tad copy neteigia, kad jų daug.

## ⛔ Blokeriai prieš siuntimą

1. **OpenCart → Omnisend integracija** — be jos cart / checkout / browse / post-purchase trigeriai negyvi
2. **Siuntėjo adresas** — `info@boilis.lt` ar `info@karpininkams.lt` (`_build.py` konstanta `EMAIL`)
3. **Domeno autentifikacija** (SPF/DKIM/DMARC), kitaip Omnisend 409 `email-unverified-domain`
4. **„Nemokamas pristatymas nuo 60 €"** — prieštaravimas svetainėje, žr. `_facts.md`. Copy to nemini

## Komandos

```bash
cd /workspace/clients/karpininkams/automations
python3 _build.py                 # visi srautai
python3 _build.py 04-browse       # vienas aplankas
python3 _split_out.py             # Omnisend push versija su markeriais -> _omnisend/
python3 _qa.py                    # nuorodos 200 + diakritikai + em-dash + trūkstami raktai
python3 _render_all.py            # 375px mobile + 900px desktop PNG į _render/
python3 _preview_build.py         # iframe galerija į _pages/
python3 _push_repo.py             # viskas į elaiskai/karpinkaireal
```

Eiga: Luko approval → Omnisend push (`--split`) → test send → Eduardo approval → enable.
