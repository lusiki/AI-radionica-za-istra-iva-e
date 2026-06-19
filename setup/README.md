# Postavljanje: sučelja, preduvjeti i cijene

Kratki praktični vodič — *kako* uopće raditi s AI-jem na ovaj (agentski) način, što vam treba i koliko
košta. *(Stanje: lipanj 2026. Cijene se mijenjaju — provjerite na službenom izvoru, vidi dno.)*

## 1. Načini rada — gdje "živi" agent

Razgovarate s istim Claudeom, ali kroz različita sučelja:

| Sučelje | Za koga | Što vidite | Agentski rad? |
|---|---|---|---|
| **Chat** (claude.ai / aplikacija) | svi, za učenje | prozor za razgovor | ❌ ne dira vaše datoteke |
| **Ekstenzija u VS Codeu** *(plugin)* | **netehnički — preporuka** | uređivač + panel, datoteke, gumbi | ✅ da |
| **Terminal / CLI** (`claude`) | onima kojima terminal ne smeta | tekstualna ljuska | ✅ da |
| **Desktop aplikacija** | alternativa VS Codeu | samostalna aplikacija | ✅ da |

**Što je terminal / CLI?** Prozor u koji *tipkate* naredbe umjesto da klikate. Zvuči zastrašujuće, ali
za ovo trebate zapamtiti samo jednu naredbu — `claude` — a sve ostalo radite običnim jezikom.

**Preporuka za radionicu:** počnite s **ekstenzijom u VS Codeu**. Terminal je skriven, vidite svaku
promjenu datoteke i klikom odobravate korake. Agenti, vještine i pravila rade jednako u svim sučeljima.

## 2. Preduvjeti

**Obavezno:**
- **Claude Code** — instalirajte ekstenziju iz VS Code Marketplacea *ili* native instalacijom
  (`curl -fsSL https://claude.ai/install.sh | bash`).
- **Claude račun** — pretplata (Pro ili Max) *ili* Anthropic API ključ.
- **Node.js 18+** — potreban za pokretanje Claude Codea (provjera: `node --version`).
- **git** — verzioniranje (provjera: `git --version`).

**Opcionalno (ovisno o projektu):**
- **Quarto** — za renderiranje slajdova (ova radionica): `winget install --id Posit.Quarto -e`
- **R / Python** — za figure i analizu podataka.
- **gh** (GitHub CLI) — za rad s pull requestovima.

## 3. Cijene

### Pretplate (uključuju Claude Code)
Claude Code **nema zasebnu cijenu** — koristi potrošnju iz vaše pretplate (zajednički 5-satni prozori).

| Plan | Cijena / mjesec | Za koga |
|---|---|---|
| **Claude Pro** | **~20 $** | pojedinci, povremena upotreba — *dovoljno za početak* |
| Claude Max 5× | ~100 $ | redoviti korisnici |
| Claude Max 20× | ~200 $ | intenzivan rad |

Napomene: od 15.6.2026. "headless" / Agent SDK upotreba troši zaseban kredit ($20 Pro / $100 Max 5× /
$200 Max 20×). Team Standard ($20/sjedalo) *ne* uključuje Claude Code; Team Premium ($100/sjedalo,
najmanje 5) uključuje.

### API (plaćanje po potrošnji)
Po milijun tokena (ulaz / izlaz):

| Model | Ulaz | Izlaz | Uloga (raspodjela 70/20/10) |
|---|---|---|---|
| **Haiku 4.5** | 1 $ | 5 $ | brz/jeftin — ~70% mehaničkog posla |
| **Sonnet 4.6** | 3 $ | 15 $ | srednji — ~20% pregleda |
| **Opus 4.8** | 5 $ | 25 $ | vrhunski — ~10% prosudbe |
| Fable 5 | 10 $ | 50 $ | najsposobniji (opcionalno) |

Štednje: skupna obrada (*batch*) −50%, predmemorija (*cache*) −90% na ponovljeni ulaz, kontekst od 1M
tokena bez doplate. Zbog raspodjele 70/20/10 račun je **50–80% niži** nego da sve ide na vrhunski model.

### Što odabrati
- **Za radionicu / početak:** **Claude Pro (~20 $/mj)** je dovoljan — ne treba API ni programiranje.
- API uzmite tek ako gradite automatizaciju izvan interaktivnog rada.

---

*Izvori / provjera (cijene se mijenjaju):* službeno na **anthropic.com/pricing** i **claude.com**.
*Stanje u ovom dokumentu: lipanj 2026.*
