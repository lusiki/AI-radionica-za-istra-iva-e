# AI radionica za istraživače

**Agentska AI za metodološka istraživanja** — materijali za radionicu *i* mali radni primjer
"harnessa" (radnog okvira) koji ta radionica objašnjava.

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
├─ index.html                # interaktivni pregled gradivnih blokova (klikni za primjer)
├─ slides/talk.qmd           # prezentacija (Quarto → RevealJS): "Od chata do delegiranja"
├─ resources/                # prateći materijali za ponijeti
│   ├─ glossary.md           #   pojmovnik: od riječi iz chata do agentskih riječi
│   └─ README.md             #   plan kompleta resursa
├─ harness-map/README.md     # komentirana mapa cijelog radnog okvira (za učenje)
├─ CLAUDE.md                 # "ustav" projekta — pravila koja Claude čita svake sesije
└─ .claude/                  # sam radni okvir (the harness):
    ├─ rules/                #   priručnici (rules) — učitavaju se po potrebi (po putanji)
    ├─ skills/               #   gumbi (skills) — /render, /proofread, /commit, /review-deck
    ├─ agents/               #   ekipa (agents) — deck-critic, deck-fixer, audience-reviewer
    └─ constitutional-governance.md   # ustavno upravljanje (članci I–VI)
```

## Pet gradivnih blokova *(the building blocks)*

Cijeli sustav stoji na pet slojeva; svaki ima nadimak na običnom jeziku. Engleska imena zadržana su i
navedena u zagradama.

| Sloj | Nadimak | Što je |
|---|---|---|
| `CLAUDE.md` | **Ustav** | jedna kratka stranica kućnih pravila, čita se svake sesije |
| Rules | **Priručnici** | priručnici koji se pojave samo kad su relevantni (po putanji datoteke) |
| Skills | **Gumbi** | imenovani recepti — naredbe poput `/render`, `/proofread`, `/commit` |
| Agents | **Ekipa** | uski specijalisti, svaki provjerava jednu stvar |
| Settings + Hooks | **Automatski sustavi** | dozvole i alarmi koji se sami okidaju *(još nije izrađeno)* |

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
- **Brzi pregled svih blokova:** otvorite `index.html` u pregledniku — svaki naziv datoteke je poveznica na sam primjer.
- Počnite od prezentacije: [`slides/talk.qmd`](slides/talk.qmd) (ili renderirani HTML).
- Za "ispod haube": [`harness-map/README.md`](harness-map/README.md) — što je svaki blok, kako radi i zašto.

### 2. Za pokretanje (uživo)
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
- ⏳ Quarto još nije instaliran → špica još **nije renderirana** (pravilo provjere: ne tvrdimo da radi dok ne provjerimo).
- ⏳ Preostaje: 5. sloj (`settings` + `hooks`), kartica praga kvalitete + podsjetnik, objava na GitHub Pages.

## O pristupu

Repozitorij slijedi ustaljene obrasce za **agentski rad s alatom Claude Code** (Claude Code "harness"):
vitki ustav, pravila vezana uz putanju, vještine, specijalizirani agenti i suparnička petlja
kritičar–ispravljač. Cilj je pokazati te obrasce na konkretnom, malom primjeru.

*Autor / voditelj radionice: Luka Šikić.*
