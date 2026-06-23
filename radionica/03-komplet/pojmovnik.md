# Pojmovnik, od riječi iz chata do agentskih riječi

Jednostrana tablica prijevoda za publiku. **Zadržite isti izričaj** svuda gdje se pojavi (slajdovi,
podsjetnik, repozitorij) kako bi se učvrstio jedan mentalni model, a ne raspao na više njih.
Engleska tehnička imena ostaju na engleskom i navode se u zagradama, kao *hrvatski pojam (english-name)*.

| Što sad kažete (svijet chata) | Agentski pojam | Što to znači, jednostavno |
|---|---|---|
| Prompt | **specifikacija zadatka (task spec)** | Opis posla, dakle cilj, ograničenja i kako izgleda „gotovo". Kao odjeljak o metodama, a ne nejasna molba. |
| Razgovor / nit | **agentska petlja (agent loop)** | Opazi, odluči, djeluj, provjeri, ponovi, možda kroz mnogo koraka, a ne jedno pitanje i jedan odgovor. |
| „Kopiraj kôd i sam ga pokreni" | **korištenje alata (tool use)** | Agent *sam* pokreće kôd, pretražuje i ispituje kataloge, umjesto da vi prenosite stvari naprijed-natrag. |
| Chatbot / „model" | **agent** | Model umotan u ulogu (alati + memorija + stalna pravila + zaštitne ograde). |
| „Provjeri svoj rad, molim" | **samoprovjera (reflection)** | Agent kritizira i popravlja vlastiti izlaz, most-uzorak koji već koristite u chatu. |
| Ponovno objašnjavanje u svakoj sesiji | **ustav + memorija** | Stalne upute i bilješke spremljene na disk, da se ne morate ponavljati. |
| „Jednostavno je to izmislio" | **halucinacija pa provjera** | Rješenje nije povjerenje. To je korak koji provjerava tvrdnje/citate sa stvarnim izvorom i blokira ono što padne. |
| Pustiti da „samo sve napravi" | **regulator autonomije** | Birate po zadatku, pošalji-i-zaboravi za nizak rizik, odobri-prije-radnje za visok rizik. |
| Autor = ujedno recenzent | **razdvajanje kritičara i ispravljača (critic / fixer)** | Kritičar (samo čita) pronalazi greške, zaseban ispravljač popravlja, kritičar ponovno provjerava. Recenzija, automatizirana. |

**Mali dijagram za podsjetnik:**

```
   Vi ─▶ specifikacija zadatka ─▶ agentska petlja ─▶ alati / podaci ─▶ izlaz ─▶ prag kvalitete ─▶ vi odobravate
                  ▲                                                        │
                  └──────────────────── ispravi ako padne ─────────────────┘
```

---

*Prateći materijali koje treba još izraditi.* `quality-gate-card.md` (≤ 10 provjera, zeleno/žuto/crveno,
kartica „smijem li vjerovati ovom izlazu?") i `cheat-sheet.md` (3 do 5 agentskih obrazaca relevantnih
za istraživanje, sa zametkom specifikacije zadatka za svaki).
