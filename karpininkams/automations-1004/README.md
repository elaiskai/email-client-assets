# KARPININKAMS.LT - Omnisend automatizaciju srautai

**Atnaujinta 2026-10-04.** 4 srautai, **9 laiskai**. Welcome srauta Lukas daro atskirai.

Gyva perziura: <https://elaiskai.github.io/karpinkaireal/index.html>

## Kas repo viduje

| Kelias | Kas tai |
|---|---|
| `omnisend/<srautas>/<laiskas>.html` | **Omnisend push versija** - vietoj produktu tinklelio palikti markeriai `<!--SPLIT:cart-->`, `<!--SPLIT:viewed-->`, `<!--SPLIT:popular-->`. Laiskas keliamas custom-HTML bloku, o markerio vietoje idedamas natyvus Omnisend produktu blokas. |
| `docs/*.html` | Lokali perziura su **mock** produktu tinkleliais (GitHub Pages serve'ina is `/docs`) |
| `copy/*.txt` | Copy saltinis - `KEY: tekstas` formatas, generuotas per `lt_copy.py` |
| `HANDOFF.md` | Pilnas perdavimo dokumentas: trigeriai, delay'ai, sprendimai, blokeriai |

## Srautai

| Srautas | Laiskai | Trigeris | Delay'ai |
|---|---|---|---|
| `02-cart` | cart-01, cart-02, cart-03 | Added product to cart | +1 val. / +8 val. / +24 val. |
| `03-checkout` | checkout-01, checkout-02 | Started checkout | +45 min. / +12 val. |
| `04-browse` | browse-01, browse-02 | Viewed product (inStock) | +3 val. / +2 d. (tik neatidariusiems) |
| `05-post-purchase` | post-01, post-02 | Order placed / fulfilled | iskart / +10 d. |

## 2026-10-04 pakeitimai

- **Isimtas nuolaidos kodas is `cart-03`.** Klausimyne jokio kodo nebuvo, svetaineje viesas kodas taip pat neegzistuoja. Treciasis laiskas dabar yra paskutinis priminimas plius nuoroda i akciju skilti (~1 700 prekiu su 11-50 % nuolaidomis).
- **Po pirkimo srautas sutrumpintas iki 2 laisku** - `post-03` (lojalumo taskai) isimtas.
- **`post-02` gavo tiksliu zingsniu panele**, kaip palikti ivertinima: prekes puslapyje skirtukas „Ivertinimai" -> forma „Parasyti ivertinima" -> mygtukas „Testi". Patikrinta gyvai, registruotis nereikia. Didelio CTA mygtuko nera specialiai - forma gyvena tos pacios prekes puslapyje, i kuri veda produktu blokas.
- **Winback srautas istrintas** (buvo 3 laiskai).

## Dizainas

FOX stilius: fonas `#202020` / `#141414`, oranzinis akcentas `#F58C23`, Oswald (DIDZIOSIOMIS) + Ubuntu.
Plotis `width:100%;max-width:600px`, breakpoint 620px, blokai mobile stack'inasi po viena.
Be logotipo, be footer'io, be hero paveikslu - Omnisend logo ir footeri prideda natyviai.

## Blokeriai pries enable

1. **OpenCart -> Omnisend integracija** - be jos cart / checkout / browse / post-purchase trigeriai negyvi
2. **Siuntejo adresas** - `info@boilis.lt` ar `info@karpininkams.lt`
3. **Domeno autentifikacija** (SPF / DKIM / DMARC), kitaip Omnisend 409 `email-unverified-domain`
4. **„Nemokamas pristatymas nuo 60 EUR"** - prestatavimas svetaineje nesutampa, copy to nemini

## Build

Saltinis: `/workspace/clients/karpininkams/automations/`

```bash
python3 _gen_copy.py          # copy per lt_copy.py (Codex / ChatGPT prenumerata)
python3 _build.py             # lokali perziura (mock produktu blokai)
python3 _split_out.py         # Omnisend versija i _omnisend/
python3 _qa.py                # nuorodos 200 + diakritikai + em-dash + truksta copy
python3 _render_all.py        # 375px mobile + 900px desktop PNG
python3 _preview_build.py     # iframe galerija i _pages/
python3 _push_repo.py         # viskas i sita repo
```
