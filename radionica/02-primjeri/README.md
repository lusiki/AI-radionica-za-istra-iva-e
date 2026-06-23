# Empirijski primjer, uzmite s GitHuba i pokrenite

Cilj je pokazati da ovo **nije teorija**. Klonirate ovaj repozitorij i u nekoliko minuta vidite radni
okvir na djelu kroz **dva mala pokusa**.

## Korak 0, priprema (≈ 5 min)

Preduvjeti su Claude Code, git i Quarto (vidi [`../01-postavljanje/README.md`](../01-postavljanje/README.md)).

```bash
git clone https://github.com/lusiki/AI-radionica-za-istra-iva-e.git
cd AI-radionica-za-istra-iva-e
```

Otvorite mapu u **VS Codeu** i pokrenite Claude Code panel (ili u terminalu utipkajte `claude`).
Za prvi pokus instalirajte Quarto naredbom `winget install --id Posit.Quarto -e`.

---

## Pokus 1, "Renderiraj i provjeri" *(vještina + pravilo provjere)*

**Što utipkate:**
```
/render
```
(ili običnim jezikom, *"Renderiraj prezentaciju."*)

**Što gledate:**
1. Claude pokrene `quarto render` nad `slides/talk.qmd`.
2. **Provjeri da je `slides/talk.html` stvarno nastao** i tek tada javi "gotovo".
3. Otvorite `slides/talk.html` u pregledniku, špica je tu.

**Poanta.** Agent ne tvrdi uspjeh „iz mašte", nego provjeri rezultat (*pravilo provjere*). Jedna naredba
daje **ponovljiv** ishod. *(Ako Quarto nije instaliran, `/render` pošteno STANE i kaže vam da ga
instalirate, i to je dio poante.)*

---

## Pokus 2, "Suparnička petlja" *(agenti + kritičar / ispravljač)*

Neobavezno, ali poučno. Prvo **ubacite malu grešku** u `slides/talk.qmd`, npr. tvrdnju bez pokrića
(„Agentska AI je 100% točna.") ili učinite neki slajd predugačkim. Tako vidite petlju kako je hvata.

**Što utipkate:**
```
/review-deck
```
(ili *"Pregledaj špicu i popravi probleme."*)

**Što gledate:**
1. Razašalju se `deck-critic` i `audience-reviewer` (oba **samo čitaju**) i daju nalaze po težini
   (Kritično / Veliko / Malo) te ocjenu od 0 do 100.
2. `deck-fixer` (čita i piše) popravi **najgore prvo**.
3. `deck-critic` **ponovno** provjeri u svježem kontekstu i da novu ocjenu. Petlja do čistog prolaza.

**Poanta.** Kritičar ne smije uređivati (pa nema razloga biti popustljiv), ispravljač ne smije sam sebe
odobriti (pa kritičar ponovno provjerava). To je **recenzija**, automatizirana, i hvata ono što
provjera pravopisa ne bi (tvrdnju bez pokrića, obrnuti predznak, nedosljedan pojam).

---

## Bonus, plan-first uživo

Utipkajte *"Dodaj završni slajd 'Hvala' i renderiraj."* Gledajte kako Claude **prvo pokaže plan** i
čeka vaše odobrenje prije nego dotakne datoteku. Vi ostajete glavni.

## Što ste vidjeli

Oba pokusa imaju isti ritam, **plan, djeluj, provjeri, pregledaj, pa vaše odobrenje.** To je cijeli
radni okvir u malom, na vašem stvarnom projektu, a ne na igrački.
