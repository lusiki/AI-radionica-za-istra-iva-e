# AI radionica za istraživače

**Agentska AI za metodološka istraživanja** — materijali za radionicu *i* mali radni primjer
"harnessa" (radnog okvira) koji ta radionica objašnjava.

**🌐 Živa prezentacija (web):** <https://lusiki.github.io/AI-radionica-za-istra-iva-e/>

### 📱 Skenirajte za otvaranje na mobitelu

Usmjerite kameru telefona na ovaj QR kod — otvorit će živu prezentaciju.

<img src="assets/qr-prezentacija.png" alt="QR kod — otvara https://lusiki.github.io/AI-radionica-za-istra-iva-e/" width="220" height="220">

> **Cilj radionice:** pomoći metodološkim istraživačima da naprave iskorak od *chat-promptanja*
> (razgovora s AI-jem radi jednog odgovora) prema **agentskom radu** — gdje AI-ju *povjeravate* cijeli
> zadatak: on ga planira, izvršava, provjerava vlastiti rad i vraća se tek na vaše odobrenje.

Ovaj repozitorij je namjerno i **sam sićušna instanca** tog radnog okvira: dok čitate kako je posložen,
gledate sam okvir na djelu. *(Medij je poruka.)*

---

## Što je ovdje

```
.
├─ README.md                 # ova stranica
├─ index.qmd                 # prezentacija kao web-dokument (Quarto) → docs/index.html
├─ primjeri.qmd              # primjeri datoteka (s pločicama) → docs/primjeri.html
├─ setup.qmd                 # sučelja, preduvjeti, cijene (web) → docs/setup.html
├─ vjezba.qmd                # vođena vježba (web) → docs/vjezba.html
├─ pregled.html              # interaktivni pregled gradivnih blokova (klikni za primjer)
├─ docs/                     # objavljena web-stranica (GitHub Pages)
├─ slides/talk.qmd           # prezentacija (Quarto → RevealJS): "Od chata do delegiranja"
├─ resources/                # prateći materijali za ponijeti
│   ├─ glossary.md           #   pojmovnik: od riječi iz chata do agentskih riječi
│   └─ README.md             #   plan kompleta resursa
├─ harness-map/README.md     # komentirana mapa cijelog radnog okvira (za učenje)
├─ setup/README.md           # sučelja, preduvjeti i cijene
├─ demos/README.md           # empirijski primjer: dva pokusa s GitHuba
├─ CLAUDE.md                 # "ustav" projekta — pravila koja Claude čita svake sesije
└─ .claude/                  # sam radni okvir (the harness):
    ├─ rules/                #   priručnici (rules) — učitavaju se po potrebi (po putanji)
    ├─ skills/               #   gumbi (skills) — /render, /proofread, /commit, /review-deck
    ├─ agents/               #   ekipa (agents) — deck-critic, deck-fixer, audience-reviewer
    └─ constitutional-governance.md   # ustavno upravljanje (članci I–VI)
```

## Pet gradivnih blokova *(the building blocks)*

Cijeli sustav stoji na pet slojeva; svaki je stvarna datoteka u projektu. Engleska imena su zadržana
jer ih alat tako traži.

| Sloj (datoteka) | Što je |
|---|---|
| `CLAUDE.md` · `AGENTS.md` | kratka stranica kućnih pravila, čita se svake sesije |
| `.claude/rules/*.md` | priručnici koji se pojave samo kad su relevantni (po putanji datoteke) |
| `.claude/skills/*/SKILL.md` | imenovani recepti — naredbe poput `/render`, `/proofread`, `/commit` |
| `.claude/agents/*.md` | uski specijalisti, svaki provjerava jednu stvar |
| `.claude/settings.json` (+ hooks) | dozvole i alarmi koji se sami okidaju *(još nije izrađeno)* |

`CLAUDE.md` je naziv u Claude Codeu; `AGENTS.md` je isti, vendor-neutralan oblik koji koriste GPT / Codex i drugi alati.

**Srce sustava — suparnička petlja *(adversarial loop)*:** **kritičar (deck-critic)** samo čita i
nabraja greške (ne smije uređivati), **ispravljač (deck-fixer)** ih popravlja (ne smije odobriti
vlastiti rad), pa kritičar ponovno provjeri — u krug do čistog prolaza. To je naprosto recenzija
*(peer review)*, automatizirana. Pokreće je vještina `/review-deck`.

Detaljno objašnjenje svakog bloka, s točnim datotekama i analogijama, je u
[`harness-map/README.md`](harness-map/README.md).

## Jezična konvencija

- Sadržaj namijenjen publici (slajdovi, resursi) i mapa za učenje su na **hrvatskom**.
- Strojni dio (`CLAUDE.md`, `rules`, `agents`, governance) ostaje na **engleskom** — to su upute AI-ju.
- Engleska tehnička imena zadržana su i navedena u zagradama: *hrvatski pojam (english-name)*.
  Nazivi naredbi (`/render`) ostaju na engleskom jer ih Claude Code tako poziva.

## Kako koristiti

### 1. Za čitanje / učenje
- **Žive web-stranice (GitHub Pages):**
  - Prezentacija: <https://lusiki.github.io/AI-radionica-za-istra-iva-e/>
  - Primjeri datoteka: <https://lusiki.github.io/AI-radionica-za-istra-iva-e/primjeri.html>
  - Postavljanje, sučelja i cijene: <https://lusiki.github.io/AI-radionica-za-istra-iva-e/setup.html>
  - Vođena vježba: <https://lusiki.github.io/AI-radionica-za-istra-iva-e/vjezba.html>
- **Brzi pregled svih blokova:** otvorite `pregled.html` u pregledniku — svaki naziv datoteke je poveznica na sam primjer.
- Počnite od prezentacije: [`slides/talk.qmd`](slides/talk.qmd) (ili renderirani HTML).
- Za "ispod haube": [`harness-map/README.md`](harness-map/README.md) — što je svaki blok, kako radi i zašto.

### 2. Za pokretanje (uživo)
Sučelja, preduvjeti i cijene → [`setup/README.md`](setup/README.md). Dva gotova pokusa korak-po-korak → [`demos/README.md`](demos/README.md).

Preduvjeti: [Claude Code](https://claude.ai/code), [Quarto](https://quarto.org), `git`.
1. Instalirajte Quarto: `winget install --id Posit.Quarto -e` (pa ponovno otvorite ljusku).
2. **Renderirajte špicu:** u Claude Codeu utipkajte `/render` — provjerava da se HTML *stvarno* izgradio.
3. **Pokrenite suparničku petlju:** `/review-deck` razašalje `deck-critic` + `audience-reviewer` (samo
   čitaju), preda nalaze `deck-fixer`-u, kritičar ponovno provjeri, i tako dok ne bude čisto — pa ocijeni 0–100.
4. **Vođena vježba** (≈ 20 min) je na dnu [`harness-map/README.md`](harness-map/README.md).

### 3. Za prilagodbu
Forkajte repozitorij, zamijenite sadržaj špice svojim, prilagodite pravila i agente. Počnite malo
(ustav + 2–3 vještine) i rastite kako otkrivate da vam treba — *strop, a ne pod.*

## Trenutno stanje

- ✅ Blokovi: ustav, 4 pravila, ustavno upravljanje, 4 vještine, 3 agenta.
- ✅ Prezentacija + pojmovnik + mapa za učenje (na hrvatskom).
- ✅ Interaktivni pregled (`pregled.html`), postavljanje + cijene (`setup/`), empirijski primjer (`demos/`).
- ✅ Objavljena web-prezentacija: Quarto dokument (`index.qmd`) → `docs/`, GitHub Pages.
- ✅ Quarto instaliran; prezentacija renderirana i objavljena na GitHub Pages.
- ⏳ Preostaje: 5. sloj (`settings` + `hooks`), kartica praga kvalitete + podsjetnik.

## O pristupu

Repozitorij slijedi ustaljene obrasce za **agentski rad s alatom Claude Code** (Claude Code "harness"):
vitki ustav, pravila vezana uz putanju, vještine, specijalizirani agenti i suparnička petlja
kritičar–ispravljač. Cilj je pokazati te obrasce na konkretnom, malom primjeru.

*Autor / voditelj radionice: Luka Šikić.*
