# Claude Code harness, komentirana mapa za učenje

Vaša referenca za razumijevanje stroja *iza* izvršne mape. Izlaganje prenosi **zašto**. Ovaj dokument
prenosi **kako**, s točnim datotekama, mehanikom i jednostavnom analogijom za svaki dio. Engleska
tehnička imena ostaju na engleskom i navode se u zagradama, kao *hrvatski pojam (english-name)*. Nazivi
naredbi (`/render`) ostaju na engleskom jer ih Claude Code tako poziva.

> **Kako ovo koristiti.** Pročitajte jednom od početka do kraja, a zatim napravite **vođenu vježbu** na
> dnu, u *ovoj* mapi. Petlju ćete razumjeti mnogo brže ako je jednom osjetite nego čitajući cijeli vodič.

---

## Sve u jednom dahu

Opišete što želite, običnim jezikom. Claude se ponaša kao glavni izvođač radova. Izradi nacrt, zatraži
vaše odobrenje, unajmi ekipu specijaliziranih pod-agenata, pregleda njihov rad, vrati ih da poprave što
ne valja i vraća se k vama tek kad posao prođe inspekciju. **Vi govorite, Claude vodi gradilište.**
Sve ostalo su instalacije, izgrađene tako da nikad ne morate misliti na instalacije.

---

## Pet slojeva (gdje svaki živi, što radi, analogija)

Sva konfiguracija projekta živi u skrivenoj mapi `.claude/` plus korijenski `CLAUDE.md`.

### 1. `CLAUDE.md`, Ustav *(Constitution)*
- **Gdje.** Korijen projekta. Čita se na **početku svake sesije.**
- **Mehanika.** *Vitka* stranica (~120 redaka, **tvrda granica ~150**). Razlog je tvrdo ograničenje.
  *Claude pouzdano slijedi tek ~100 do 150 uputa, a sustavski prompt već troši ~50.* `CLAUDE.md` **i**
  uvijek-uključena pravila dijele taj jedan proračun. Iznad ~150 redaka „Claude počinje tiho
  ignorirati pravila". Sav detalj seli u pravila vezana uz putanju.
- **Analogija.** Jednostranični silabus. Nabrojite 300 pravila i studenti ne slijede nijedno.

### 2. Pravila *(Rules)*, Priručnici
- **Gdje.** `.claude/rules/*.md`. Učitavaju se **automatski.**
- **Mehanika.** Ključni trik je **vezivanje uz putanju** preko retka `paths:` u zaglavlju datoteke,
  npr. `paths: ['**/*.R']` znači da se priručnik za R pojavi samo kad Claude dotakne `.R` datoteku.
  Inventar je **32 pravila**, od kojih je ~27 vezano uz putanju, samo ~5 je „uvijek uključeno" (bez `paths:`).
- **Analogija.** Profesor ne pamti svaki stilski priručnik. Pravi se pojavi na stolu kad ocjenjuje tu
  vrstu zadaće, a nestane kad nije potreban. Tako 32 pravila nikad ne zatrpaju pažnju modela.

### 3. Vještine *(Skills)*, Gumbi
- **Gdje.** `.claude/skills/<ime>/SKILL.md` (jedna mapa po vještini).
- **Mehanika.** `SKILL.md` je YAML zaglavlje (`name`, `description`, `argument-hint`) + numerirani
  koraci. Poziva se na dva načina, **eksplicitno** (utipkate `/proofread`) ili **automatski** (Claude
  pročita vaš zahtjev na običnom jeziku i odabere pravu vještinu). Inventar je **52 vještine.**
- **Analogija.** Imenovani recepti. Rijetko sami pritisnete gumb, imenujete cilj, a Claude pritisne pravi.

### 4. Agenti *(Agents)*, Ekipa
- **Gdje.** `.claude/agents/<ime>.md`. **Pozivaju ih vještine, nikad vi izravno.**
- **Mehanika.** Svaki agent je uski specijalist (gramatika, raspored/prelijevanje, R kôd, sadržaj
  struke, …). Zaglavlje fiksira `model`, `effort`, `maxTurns` (zaštita od beskonačne petlje),
  `tools`/`disallowedTools` (npr. kritičar **samo za čitanje**), `permissionMode`. Inventar je **18 agenata.**
  Orkestracijska vještina ih razašalje **paralelno**, pa sintetizira.
- **Analogija.** Specijalizirano osoblje koje voditelj raspoređuje. *„Jedan prompt koji istovremeno
  provjerava gramatiku, raspored, matematiku i kôd osrednje obavi sve od navedenog."*

### 5. Postavke + Okidači *(Settings + Hooks)*, Automatski sustavi
- **Gdje.** `.claude/settings.json` (dozvole + okidači) i `.claude/hooks/*.py`.
- **Mehanika.** **Dozvole** odlučuju što Claude smije bez nadzora. **Okidači (hooks)** se aktiviraju na
  događaje (Stop, PreCompact, PostToolUse, …). Inventar je **7 okidača** (bilježenje sesije, obavijest na
  radnoj površini, preživljavanje konteksta, monitor konteksta s upozorenjima na 40/55/65/80/90%,
  **zaštitne ograde za git** koje fizički blokiraju `git reset --hard` / `push --force`, pomiritelj
  zastarjelih brojeva) + pravi git pre-commit okidač.
- **Analogija.** Vatrodojava u zgradi. Ključni uvid glasi *„Pravila žive u kontekstu i mogu se sažeti i
  nestati. Okidači žive u settings.json i aktiviraju se **svaki put**, bez obzira na stanje konteksta."*
  Zato je provedba koja mora preživjeti dugu sesiju **okidač**, a ne uputa.

---

## Dvije ideje zbog kojih sve funkcionira

1. **Specijalisti pobjeđuju generalista.** (Sloj 4 gore.)
2. **Suparnička petlja *(adversarial loop)*** (srce). **Kritičar (deck-critic)** (samo čita, *ne može*
   uređivati) nabraja svaku grešku, a **ispravljač (deck-fixer)** (čita i piše) ih popravlja, pa kritičar
   ponovno provjerava. Ponavlja se dok krug ne pronađe ništa novo (**„petlja do iscrpljenja"**,
   konvergira nakon 2 prazna kruga, granica od 5 krugova je tek osigurač).
   - *Zašto radi.* „Kritičar ne može popravljati datoteke, pa nema poticaja umanjivati probleme.
     Ispravljač ne može odobriti sam sebe." Time se ubija promašaj „izgleda dobro". **To je recenzija.**

## Dva pravila koja održavaju poštenje

- **Prag 80 / 90 / 95.** Svaka datoteka ocijenjena od 0 do 100. **80** = sigurno za commit, **90** = spremno
  za isporuku (PR), **95** = izvrsnost, **ispod 80 = blokirano.** Primjeri odbitaka su prelijevanje
  jednadžbe −20, neispravan citat −15, tipfeler u jednadžbi −10. Git pre-commit okidač može provoditi ≥80 na svaki commit.
- **Pravilo provjere.** Claude ne smije reći „gotovo" dok stvarno nije kompajlirao / renderirao /
  pokrenuo izlaz. (Zato naša vještina `/render` *provjerava da HTML postoji* prije nego javi uspjeh.)

---

## Memorija, četiri ladice (+ zašto)

Duge sesije se **automatski sažimaju** (s gubitkom, čuvaju nedavne poteze, odbacuju sredinu). Živi chat
je jedino što ne preživi. Zato sve vrijedno čuvanja ide na **disk**:

| Ladica | Datoteka / mapa | Sadrži | Ažurira se |
|---|---|---|---|
| Ustav | `CLAUDE.md` | stalna pravila | rijetko |
| Dnevnik ispravaka | `MEMORY.md` | lekcije, preko oznake `[LEARN]`, da se greška ne ponovi | pri učenju |
| Planovi | `quality_reports/plans/` | strategija za trenutni zadatak | jednom po zadatku |
| Dnevnici sesija | `quality_reports/session_logs/` | **zašto** iza svake odluke | postupno |

*„Git bilježi **što**, a dnevnici sesija bilježe **zašto**."* Upareni okidači (`PreCompact` pa
`SessionStart`) sklone bilješku tik prije brisanja memorije i pročitaju je natrag kad se otvori sljedeća sesija.

## Kako teče stvarni posao

**Prvo plan** (samo čita, Claude izradi plan, spremi ga, vi odobrite), pa **način rada izvođača
*(contractor mode)*** (autonomno), dakle IZRADI, PROVJERI, PREGLEDAJ (paralelni specijalizirani agenti),
POPRAVI (od najgoreg), PONOVNO PROVJERI, OCIJENI, pa provjera je li konvergiralo, petlja ili predaja sažetka.
*Ništa ne sprema (commit) dok ne kažete.* Napomena. Orkestrator je **„izvršno okruženje, a ne demon"**,
ništa ga ne pokreće samo, odobrenje plana ga **ne** pokreće automatski. Čovjek je revizor neslaganja
koje petlja iznese na vidjelo.

## Trošak, obrazac raspodjele 70 / 20 / 10

Usmjeravanje modela po agentu, postavljeno retkom `model:` u svakoj datoteci agenta:

- **Haiku (brz/jeftin) ≈ 70%**, mehanički posao (izvlačenje, preoblikovanje, validacija, popravci nakon lekture)
- **Sonnet (srednji) ≈ 20%**, pregled/kritika
- **Opus (vrhunski) ≈ 10%**, visoka prosudba (urednik, recenzenti, provjera tvrdnji)

Ušteda u odnosu na sve-na-Opusu je **50 do 80%**, bez gubitka kvalitete na mehaničkoj razini. Drugi regulator
je **napor *(effort)*** (`low → medium → high → xhigh → max`). „Haiku + visok napor" može pobijediti
„Opus + nizak napor" na omeđenim zadacima. Pratite s `/cost` i `/usage`.

## Početak s punim okvirom (kad budete spremni)

Tri stvari, **instalirajte Claude Code, forkajte predložak harnessa, pa zalijepite jedan
početni prompt** koji imenuje vaš projekt. Claude pročita konfiguraciju, popuni vaše podatke, predloži
prilagodbe, pokaže plan, vi odobrite. Zatim *„počnite samo s `CLAUDE.md` i 2 do 3 vještine, ostalo dodajte
kako otkrijete da vam treba"*, **strop, a ne pod.**

---

## Kako se *ova* mapa preslikava na cijeli harness

Već stojite u (namjerno sićušnoj) instanci sustava:

| Cijeli harness | U ovom repozitoriju | Napomena |
|---|---|---|
| Ustav | [`../../CLAUDE.md`](../../CLAUDE.md) | vitak, ~1 stranica, upravo to dizajnersko pravilo |
| Pravila (priručnici) | `../../.claude/rules/` (4 datoteke) | 1 uvijek-uključeno + 3 vezana uz putanju, pokazuje trik s `paths:` |
| Ustavno upravljanje | [`../../.claude/constitutional-governance.md`](../../.claude/constitutional-governance.md) | Članci I do VI (inače opcionalno / dodaje se kasnije) |
| Vještine (gumbi) | `../../.claude/skills/{render,proofread,commit,review-deck}/` | `/review-deck` je orkestrator |
| Agenti (ekipa) | `../../.claude/agents/{deck-critic,deck-fixer,audience-reviewer}.md` | kritičar (samo čita) + ispravljač (čita/piše) + specijalist |
| Suparnička petlja | `/review-deck` povezuje kritičar, ispravljač pa ponovnu provjeru | srce, u malom |
| Specijalisti > generalist | `/proofread` (4 prolaza) + 2 različita agenta za pregled | gramatika / dosljednost / prelijevanje / tvrdnje / uokvirivanje |
| Pravilo provjere | `/render` provjerava da `.html` postoji | „ne reci gotovo bez provjere" |
| Prag kvalitete | `../../.claude/rules/quality-gates.md` | ocjena 80 / 90 / 95 |
| Razine modela (70/20/10) | `model:` u svakoj datoteci agenta | kritičar = sonnet, ispravljač = haiku, recenzent = sonnet |
| Ladice memorije | `~/.claude/.../memory/` | već bilježi ovaj projekt |
| Postavke + okidači | *(još nije izrađeno, sloj 5)* | jedini preostali dio, ponuđen sljedeći |

## Vođena vježba, odvrtite petlju jednom (≈ 20 min)

*Web-verzija ove vježbe je <https://lusiki.github.io/AI-radionica-za-istra-iva-e/vjezba.html>.*

1. **Instalirajte Quarto** (`winget install --id Posit.Quarto -e`, pa ponovno otvorite ljusku).
2. Zatražite od Claudea, običnim jezikom, *„Dodaj završni slajd 'hvala / pitanja' u špicu, pa je
   renderiraj."* Zatim gledajte kako **prvo planira**.
3. **Odobrite plan.** Gledajte način rada izvođača. Uredi `talk.qmd`, pokrene `/render` i **provjeri**
   da je HTML izgrađen prije nego javi gotovo.
4. Pokrenite `/proofread slides/talk.qmd` i pročitajte nalaze grupirane po težini.
5. Pokrenite `/commit` i gledajte kako **pita prije** `git init` i **prije** commita. *Vi* ostajete glavni.

Taj krug, plan, djeluj, provjeri, pregledaj, pa vaše odobrenje, *jest* cijeli harness u malom.
