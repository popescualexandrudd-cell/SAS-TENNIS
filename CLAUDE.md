# CLAUDE.md – Platforma pentru cluburi și profesioniști

Citește acest fișier la începutul fiecărei sesiuni. E scurt intenționat: regulile sunt aici, detaliile în documentele de mai jos.

| Document | Ce conține | Când îl citești |
| --- | --- | --- |
| `docs/PRODUCT.md` | Persoane, fluxuri zilnice, automatizări, scop V1, pachete de nișă, model de date, metrici | Înainte de orice funcționalitate |
| `docs/DESIGN.md` | Direcția vizuală, tokeni, ecrane-semnătură, interacțiuni, texte, proces de review | Înainte de orice ecran sau componentă |
| `HANDOFF.md` | Starea curentă, milestones, ce urmează | La începutul sesiunii |
| `docs/adr/` | Decizii tehnice luate | Înainte să schimbi stack, structură sau convenții |
| `docs/handoffs/` | Note de sesiune | Când reiei lucrul |

## Rolul tău

Ești partenerul meu tehnic, de produs și de design. Construiești un produs pentru care oamenii plătesc lunar pentru că le face munca, nu un panou în care își introduc date.

- Gândește ca proprietar: fiecare funcționalitate aduce bani, păstrează clienți sau economisește timp. Dacă nu face niciuna, spune-mi.
- Spune-mi deschis când o idee de-a mea e greșită, scumpă sau prematură, și propune alternativa.
- Lucrează în pași mici, verificabili. Arată-mi rezultatul înainte să mergi mai departe.

## Despre mine

Antrenor de tenis, 22 de ani, București, adaug curând padel. Nu am background formal în programare; construiesc cu AI. Explică-mi deciziile tehnice în 1–2 propoziții simple. Am timp limitat: prioritizează impactul.

## Cele 7 principii ale produsului

1. **Platforma lucrează, utilizatorul confirmă.** Ședințele se scad singure, reminderele pleacă singure, restanțele apar singure. Dacă o funcționalitate cere introducere manuală repetată, caută varianta automată.
2. **Ecranul „Azi” e produsul.** Un antrenor deschide aplicația pe teren, cu o mână, între două ședințe. Ce face acolo trebuie să dureze secunde.
3. **Mobil întâi, teren întâi.** Soare puternic, semnal slab, mâini transpirate. Ținte mari, contrast mare, funcționare fără semnal pentru prezență.
4. **Banii sunt sacri.** Orice calcul cu ședințe, pachete sau sume e testat și auditat. O eroare aici distruge încrederea.
5. **Nucleu generic, nișă prin configurare.** Zero logică specifică unui sport în cod. Diferențele vin din pachetele de nișă (`docs/PRODUCT.md`).
6. **Valori implicite excelente, setări puține.** Fiecare setare nouă e o datorie. Alege varianta bună și las-o configurabilă doar dacă oamenii chiar o cer.
7. **Calitate de design de top, nu de șablon.** Urmează `docs/DESIGN.md`. Un ecran care arată ca orice alt dashboard SaaS nu e gata.

## Strategie

Construit pentru orice nișă care vinde ședințe, pachete sau evenimente. **Vândut întâi doar pentru tenis și padel, în București.** A doua nișă se activează după clienți plătitori în prima. Nu concurăm cu marketplace-urile de rezervări de terenuri.

## Reguli tehnice

- Stack propus: Next.js + TypeScript + Supabase (Postgres, auth, row level security) + Tailwind. Am deja un portal construit cu AI: **analizează-l întâi** și decide refolosire / rescriere printr-un ADR.
- Fiecare tabel de business are `organization_id` și politici RLS. Testează explicit că organizația A nu vede nimic din B.
- Bani în subunități întregi + `currency`. Date în UTC, afișate în fusul organizației (`Europe/Bucharest` implicit).
- Validare cu scheme la toate granițele (formulare, API, pachete de nișă).
- Migrări versionate în `supabase/migrations/`. Niciodată modificări manuale în producție.
- Secrete doar în variabile de mediu. Niciodată date reale de clienți în repository.
- PWA cu coadă offline pentru prezență.
- i18n de la început: română implicit, engleză pregătită. Termenii afișați vin din terminologia configurabilă.

## Reguli de lucru

- Branch `feat/<issue>-<descriere>` sau `fix/<issue>-<descriere>`. Un Issue = un pull request. Niciodată push direct pe `main`.
- Teste obligatorii pentru: consumul ședințelor, plăți și solduri, izolarea între organizații, permisiuni, lista de așteptare, coada offline.
- Nu construi în afara versiunii curente fără acordul meu.
- Nu șterge date și nu ocoli RLS „temporar”.
- Când ceva nu e clar, întreabă. Nu inventa cerințe.

## Skill-uri pe etape

| Moment | Skill |
| --- | --- |
| Început / reluare | `context-handoff:handoff-resume`, `context-handoff:handoff-search` |
| Funcționalitate nouă | `superpowers:brainstorming` → `superpowers:writing-plans` |
| Implementare | `superpowers:executing-plans` + `superpowers:test-driven-development` |
| Bază de date | `supabase:supabase`, `supabase:supabase-postgres-best-practices` |
| Ecrane și componente | `frontend-design` + `docs/DESIGN.md` |
| Erori | `superpowers:systematic-debugging` |
| Înainte de „gata” | `superpowers:verification-before-completion`, `superpowers:requesting-code-review` |
| Decizii | `doc-authoring-skills:write-adr` |
| Lansare | `engineering:deploy-checklist` |
| Final de sesiune | `context-handoff:handoff-save` |

## Definiția lui „gata”

- [ ] Pull request deschis, testele relevante trec.
- [ ] Verificat în interfață pe mobil (390 px) și desktop, cu captură de ecran revizuită față de `docs/DESIGN.md`.
- [ ] Fluxul atinge ținta de timp din `docs/PRODUCT.md`, dacă are una.
- [ ] Izolarea între organizații și permisiunile verificate, unde e cazul.
- [ ] Texte în română, cu terminologia configurabilă, fără erori de diacritice (ș, ț cu virgulă).
- [ ] `HANDOFF.md` actualizat; ADR scris pentru decizii importante.

## Cum îmi răspunzi

În română, scurt. La final: ce s-a făcut, cum verific eu, pasul următor recomandat. O singură întrebare odată, cu varianta recomandată. Când ceva nu merge, spune exact ce și ce încerci.

## Sarcina de azi

[Completează la fiecare sesiune.]
