# 00, Kreni ovdje 🧭

Ovaj repozitorij je **i sadržaj radionice i radni primjer** onoga što radionica uči, agentski
Claude Code okvir (*harness*). Drugim riječima, **medij je poruka**. Sama mapa je zamišljena tako
da je pročitate kao lekciju.

## Repozitorij na prvi pogled, tri sloja

Kad pogledate korijen mape, sve pada u **tri tipa stvari**:

| Sloj | Što je | Gdje |
|---|---|---|
| 🛠️ **STROJ** | sam okvir koji pokreće rad (engleski) | `CLAUDE.md` · `.claude/` · `pregled.html` |
| 📚 **RADIONICA** | gradivo koje okvir uči/proizvodi (hrvatski) | `index.qmd` · `slides/` · `radionica/` |
| ⚙️ **IZVEDENO** | ono što stroj *napiše* (ne dirate rukom) | `docs/` (objava) · `quality_reports/` (radna memorija) |

Pravilo koje time vidite bez ijedne riječi. **Vi uređujete izvor, stroj piše `docs/`.** To je
delegiranje, nadzor i ponovljivost, pretočeni u mape.

## Stroj ima pet slojeva, pročitajte ih ovim redom

1. **Ustav** *(Constitution)*, datoteka [`CLAUDE.md`](CLAUDE.md). Jedna vitka stranica kućnih pravila koju
   Claude čita na početku svake sesije.
2. **Pravila** *(Rules)*, mapa [`.claude/rules/`](.claude/rules/). Priručnici koji se učitavaju
   **automatski, ali samo kad su relevantni** (vezani uz putanju datoteke).
3. **Vještine** *(Skills)*, mapa [`.claude/skills/`](.claude/skills/). Imenovane naredbe (`/render`,
   `/proofread`, `/commit`, `/review-deck`). Vi imenujete cilj, Claude pritisne pravi gumb.
4. **Ekipa** *(Agents)*, mapa [`.claude/agents/`](.claude/agents/). Uski specijalisti (kritičar koji
   **samo čita**, ispravljač koji **ne smije sam sebe odobriti**, specijalist za publiku).
5. **Postavke + okidači** *(Settings + Hooks)*, **još nije izrađeno.** To je jedini sloj koji ovdje
   namjerno nedostaje, dodaje se sljedeći. (Iskrenost o tome što jest i što nije gotovo je dio poante.)

Za stiliziran, klikabilan pregled svih blokova otvorite [`pregled.html`](pregled.html) lokalno.
Dublju, komentiranu studijsku mapu cijelog okvira nađite u [`radionica/00-razumijevanje/mapa-okvira.md`](radionica/00-razumijevanje/mapa-okvira.md).

## Radionica, gradivo posloženo redom čitanja

- [`radionica/00-razumijevanje/`](radionica/00-razumijevanje/), **razumjeti ideju** (studijska mapa okvira)
- [`radionica/01-postavljanje/`](radionica/01-postavljanje/), **postaviti alate** (sučelja, preduvjeti, cijene)
- [`radionica/02-primjeri/`](radionica/02-primjeri/), **isprobati petlju jednom** (kloniraj s GitHuba + dva pokusa)
- [`radionica/03-komplet/`](radionica/03-komplet/), **ponijeti komplet** (pojmovnik + plan kompleta)

Web-verzije (prezentacija, primjeri, postavljanje, vježba) objavljene su na
**<https://lusiki.github.io/AI-radionica-za-istra-iva-e/>**. Njihovi izvori (`*.qmd`, `slides/`)
namjerno ostaju u korijenu jer bi premještanje promijenilo objavljene adrese (i QR kod).

## Petlja koju sve ovo služi

**Prvo plan, pa ga odobrite, pa izvođač radi (izradi, provjeri, pregledaj, popravi), pa vaše odobrenje.**
Taj ritam je cijeli okvir u malom. Vi ostajete glavni, ništa se ne sprema dok ne kažete.
