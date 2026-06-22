# Empirijski primjer — uzmite s GitHuba i pokrenite

Cilj: pokazati da ovo **nije teorija**. Klonirate ovaj repozitorij i u nekoliko minuta vidite radni
okvir na djelu kroz **dva mala pokusa**.

## Korak 0 — priprema (≈ 5 min)

Preduvjeti (vidi [`../01-postavljanje/README.md`](../01-postavljanje/README.md)): Claude Code, git, Quarto.

```bash
git clone https://github.com/lusiki/AI-radionica-za-istra-iva-e.git
cd AI-radionica-za-istra-iva-e
```

Otvorite mapu u **VS Codeu** i pokrenite Claude Code panel (ili u terminalu utipkajte `claude`).
Za prvi pokus instalirajte Quarto: `winget install --id Posit.Quarto -e`.

---

## Pokus 1 — "Renderiraj i provjeri" *(vještina + pravilo provjere)*

**Što utipkate:**
```
/render
```
(ili običnim jezikom: *"Renderiraj prezentaciju."*)

**Što gledate:**
1. Claude pokrene `quarto render` nad `slides/talk.qmd`.
2. **Provjeri da je `slides/talk.html` stvarno nastao** — i tek tada javi "gotovo".
3. Otvorite `slides/talk.html` u pregledniku → špica je tu.

**Poanta:** agent ne tvrdi uspjeh "iz mašte" — provjeri rezultat (*pravilo provjere*). Jedna naredba
daje **ponovljiv** ishod. *(Ako Quarto nije instaliran, `/render` pošteno STANE i kaže vam da ga
instalirate — i to je dio poante.)*

---

## Pokus 2 — "Suparnička petlja" *(agenti + kritičar / ispravljač)*

Neobavezno, ali poučno: prvo **ubacite malu grešku** u `slides/talk.qmd` — npr. tvrdnju bez pokrića
("Agentska AI je 100% točna.") ili učinite neki slajd predugačkim. Tako vidite petlju kako je hvata.

**Što utipkate:**
```
/review-deck
```
(ili: *"Pregledaj špicu i popravi probleme."*)

**Što gledate:**
1. Razašalju se `deck-critic` i `audience-reviewer` (oba **samo čitaju**) → nalazi po težini
   (Kritično / Veliko / Malo) + ocjena 0–100.
2. `deck-fixer` (čita i piše) popravi **najgore prvo**.
3. `deck-critic` **ponovno** provjeri u svježem kontekstu → nova ocjena. Petlja do čistog prolaza.

**Poanta:** kritičar ne smije uređivati (pa nema razloga biti popustljiv), ispravljač ne smije sam sebe
odobriti (pa kritičar ponovno provjerava). To je **recenzija**, automatizirana — i hvata ono što
provjera pravopisa ne bi (tvrdnju bez pokrića, obrnuti predznak, nedosljedan pojam).

---

## Bonus — plan-first uživo

Utipkajte: *"Dodaj završni slajd 'Hvala' i renderiraj."* Gledajte kako Claude **prvo pokaže plan** i
čeka vaše odobrenje prije nego dotakne datoteku. Vi ostajete glavni.

## Što ste vidjeli

Oba pokusa imaju isti ritam: **plan → djeluj → provjeri → pregledaj → vaše odobrenje.** To je cijeli
radni okvir u malom — na vašem stvarnom projektu, a ne na igrački.
