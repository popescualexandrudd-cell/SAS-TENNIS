# DESIGN.md – Direcția de design

## 1. Ideea centrală: „tabela de scor a antrenorului”

Produsul se folosește pe teren, în picioare, între două ședințe, uneori în soare puternic. Inspirația nu e un dashboard SaaS, ci **tabela de scor**: cifre mari, contrast clar, starea se înțelege dintr-o privire de la doi metri.

Trei consecințe care definesc tot designul:

1. **Culoarea înseamnă informație.** Interfața e neutră; culoarea apare aproape doar acolo unde spune ceva (starea pachetului, o restanță, un client nou). Când totul e colorat, nimic nu mai e urgent.
2. **Un singur element memorabil: inelul de pachet.** Fiecare avatar de client are în jur un inel care arată ședințele rămase și starea. E semnătura vizuală a produsului. Restul interfeței e liniștit și disciplinat, ca să-l lase să vorbească.
3. **Viteza e o calitate vizuală.** Un ecran care apare instant și răspunde la atingere fără întârziere arată mai bine decât unul frumos și lent.

## 2. Ce evităm (semnele unui produs generat sau de șablon)

- Carduri identice cu colțuri rotunde și aceeași umbră gri peste tot; gradienți decorativi.
- Etichete ALL-CAPS deasupra fiecărui titlu; meta-texte legate cu „ · ”; săgeți „→” lipite de butoane.
- Un cuvânt colorat sau italic în mijlocul titlului.
- Fundal crem cu accent teracotă; fundal aproape negru cu accent verde-acid; font monospace pentru date.
- Animații de intrare pe fiecare secțiune și hover pe fiecare card.
- Dashboard cu 12 widget-uri. Proprietarul vrea 3 cifre, apoi detalii la cerere.
- Dialoguri „Ești sigur?” pentru acțiuni reversibile.
- Inter / font-ul implicit al framework-ului, ales din inerție.

## 3. Tokeni (punct de pornire, validați în faza de design)

### Culori – mod luminos

| Token | Hex | Rol |
| --- | --- | --- |
| `bg` | `#EDF0EF` | Fundalul aplicației (gri rece, ca betonul tribunei) |
| `surface` | `#FFFFFF` | Liste, foi, panouri |
| `ink` | `#16222C` | Text principal și butoanele principale |
| `ink-muted` | `#56636E` | Text secundar |
| `line` | `#D5DBDD` | Separatoare |
| `status-ok` | `#18794D` | Pachet activ, plătit |
| `status-warn` | `#9A6200` | ≤ 2 ședințe, expiră curând |
| `status-due` | `#C23F2A` | Restanță |
| `status-idle` | `#7B858C` | Inactiv, fără pachet |
| `status-new` | `#2D49C8` | Client nou, prima ședință |

- Contrast verificat pe `surface`: `ink-muted`, `status-ok`, `status-warn`, `status-due` și `status-new` trec de 4,5:1 (pot fi folosite ca text); `status-idle` trece de 3:1 și se folosește doar ca grafic (inel), nu ca text.
- **Butoanele principale sunt `ink`**, nu colorate. Culoarea rămâne rezervată stărilor.
- **Starea nu se transmite doar prin culoare:** inelul are și grad de umplere, iar restanța are un glif propriu, ca să fie lizibilă și pentru daltoniști.
- **Brandul organizației** (logo + o culoare) apare pe pagina publică, pe email-uri și în antetul aplicației. Nu colorează interfața de lucru, ca să nu concureze cu stările.

### Mod întunecat
Pentru sesiunile de seară, sub nocturnă. Aceleași roluri, cu contrast verificat (WCAG AA). Culorile de stare se ajustează ca luminozitate, nu ca nuanță, ca să-și păstreze sensul.

### Mod teren (contrast maxim)
Comutator în antetul ecranului „Azi”, reținut pe dispozitiv. Text negru pur pe alb pur, ținte de minimum 56 px, inele mai groase, fără griuri subtile. Gândit pentru soare direct și o mână ocupată.

### Tipografie

O singură familie sans-serif, aleasă deliberat după trei criterii, testate înainte de decizie:
1. **Diacritice românești corecte:** ș și ț cu virgulă dedesubt (nu cu sedilă), în toate greutățile.
2. **Cifre tabulare**, ca sumele și numărul de ședințe să se alinieze în coloane.
3. **Lizibilitate la dimensiuni mici și în lumină puternică.**

Candidați de testat (nu de ales din reflex): Instrument Sans, Hanken Grotesk, IBM Plex Sans. Decizia se notează ca ADR, cu capturi de ecran comparative.

Scară (mobil): 13 / 15 / **17 (corp)** / 20 / 24 / 32 / 44. Corpul e 17 px, nu 14: aplicația se citește în mișcare. Cifrele-cheie (ședințe rămase, sume, cele 3 cifre ale proprietarului) folosesc dimensiunile mari, cu greutate fermă. Titlurile sunt în sentence case.

### Formă, spațiu, adâncime

- Grilă de 4 px; ritmul principal 8 / 16 / 24.
- Raze cu ierarhie, nu una pentru tot: 8 px controale, 14 px blocuri de ședință în cronologie, cerc pentru avatare. Listele sunt rânduri cu separatoare, nu carduri.
- Adâncimea doar unde există cu adevărat un strat: foile de jos (bottom sheets) și meniurile. Fără umbre decorative.

## 4. Inelul de pachet (semnătura)

```
   ╭───╮      inel complet verde      = pachet activ, multe ședințe
  │ AP │      inel parțial chihlimbar  = ≤ 2 ședințe rămase
   ╰───╯      inel roșu + glif         = restanță
              inel gri punctat         = fără pachet activ
              punct albastru           = client nou / prima ședință
```

- Gradul de umplere = ședințe rămase / total. Pentru abonamente lunare = zile rămase din perioadă.
- Atingerea lungă pe avatar arată detaliul: „6 din 8 ședințe, expiră pe 30 noiembrie, plătit”.
- Cititorul de ecran anunță același lucru în cuvinte.
- **Singurul moment de animație al produsului:** la marcarea prezenței, inelul scade cu o treaptă (aprox. 200 ms), cu vibrație scurtă pe dispozitivele care o suportă. Respectă „reduce motion”.

## 5. Arhitectura navigației

**Mobil:** bară de jos cu patru secțiuni: **Azi**, **Clienți**, **Bani**, **Mai mult**. Butonul de adăugare stă în antetul fiecărei secțiuni și adaugă ce are sens acolo (ședință în „Azi”, client în „Clienți”, încasare în „Bani”).

**Desktop:** bară laterală îngustă, lista în centru, panoul de detaliu în dreapta (clientul sau ședința selectată), ca să nu se piardă contextul.

## 6. Ecranele-semnătură

### „Azi” (mobil)

```
┌──────────────────────────────┐
│ Joi, 12 nov        ☀ Mod teren│
│ 6 ședințe, 1 restanță         │
├──────────────────────────────┤
│ 16:00  Grupă copii, Teren 2   │
│  (◔AP) (●MI) (◑DR) (○IO)      │  ← tap = prezent, ține apăsat = altceva
│        ⚠ Ioana: fără pachet   │
├──────────────────────────────┤
│ 17:00  Individual, Teren 1    │
│  (◕VC)   Vlad, 2 rămase       │
│          Reînnoiește pachetul │
├──────────────────────────────┤
│ 18:00  liber                  │
│        Umple locul            │
└──────────────────────────────┘
[ Azi ] [ Clienți ] [ Bani ] [ Mai mult ]
```

- Ședința curentă e evidențiată; ședințele trecute se estompează.
- Problemele (fără pachet, restanță, ultima ședință) apar **în contextul ședinței**, cu acțiunea alături. Nu într-un panou separat de notificări.

### Fișa clientului
Sus: avatar cu inel, nume, nivel, telefon cu buton direct de WhatsApp și apel. Apoi, în ordinea importanței: pachetul curent și soldul, următoarele ședințe, progresul (V2), istoricul, notițele. Pentru minori, tutorele e vizibil imediat sub nume.

### „Bani”
Sus, o singură cifră: **suma de încasat**. Dedesubt trei liste scurte: restanțe (sortate după vechime), pachete de reînnoit, încasări recente. Fiecare rând are acțiunea principală la un tap: „Trimite reminder”, „Reînnoiește”, „Marchează plătit”.

### Programare rapidă (foaie de jos)
Client (căutare cu ultimii clienți sugerați) → serviciu (precompletat după ultima ședință) → zi și oră (sloturi libere evidențiate) → recurență (o dată / săptămânal). Patru alegeri, fiecare cu o valoare implicită bună.

### Onboarding
Un pas pe ecran, progres vizibil, valori precompletate din pachetul de nișă. Ultimul ecran nu e „Felicitări”, ci „Azi”-ul utilizatorului, cu prima ședință.

### Pagina publică
Prima impresie a clubului sau a antrenorului în fața unui client nou. Deschide cu ce caută vizitatorul (programe, evenimente apropiate, cum se înscrie), în brandul organizației. Rapidă, fără tracking inutil, arată bine când e trimisă pe WhatsApp sau Instagram (imagine de previzualizare și titlu corect).

## 7. Principii de interacțiune

- **Anulare în loc de confirmare.** Acțiunile reversibile se fac imediat, cu un toast „Anulează” timp de câteva secunde. Confirmarea explicită rămâne doar pentru ce e ireversibil (ștergeri, trimiteri de bani).
- **UI optimist.** Prezența și plățile apar instant; sincronizarea se face în fundal.
- **Offline vizibil, nu alarmant.** Un indicator discret „Salvat pe telefon, se sincronizează” când nu e semnal.
- **Formulare scurte.** O coloană, valori implicite inteligente, tastatură numerică pentru sume, prefix +40 la telefon, fără câmpuri obligatorii inutile (nume + telefon ajung pentru un client nou).
- **Acțiunea principală e mereu în zona degetului mare** pe mobil.
- **O singură foaie deschisă odată.** Fără dialoguri suprapuse.
- **Ținte de minimum 48 px** (56 px în modul teren).

## 8. Textele (microcopy)

Vocea: un asistent de antrenor calm și competent. Scurt, direct, cald. Verbe simple, sentence case, fără umplutură. Utilizatorului i ne adresăm cu „tu”; șabloanele de mesaje către clienți și părinți au o variantă cu „dumneavoastră”, aleasă de organizație.

| În loc de | Scrie |
| --- | --- |
| „Submit” / „Trimite formularul” | „Salvează clientul” |
| „Operațiune efectuată cu succes!” | „Prezența a fost salvată” |
| „Eroare 500” | „Nu am putut salva. Verifică semnalul; încercăm din nou automat.” |
| „Nu există date” | „Nicio ședință azi. Programează una sau adaugă un client.” |
| „Restanță detectată” | „Mihai are 320 lei de plătit, de 12 zile” |

Exemplu de reminder de plată (șablon editabil):

> Bună, Ana! Pachetul de 8 ședințe pentru Matei (320 lei) nu apare încă achitat. Poți plăti la următorul antrenament sau prin transfer în contul [IBAN]. Mulțumesc!

Reguli: acțiunea păstrează același nume pe tot fluxul („Reînnoiește” → „Pachet reînnoit”); erorile spun ce s-a întâmplat și ce urmează, fără scuze vagi; numerele și datele sunt în format românesc (12 noiembrie, 1.250 lei).

## 9. Accesibilitate și performanță (podea de calitate, nu opțiuni)

- WCAG 2.2 AA: contrast 4,5:1 pentru text, focus vizibil, etichete pe toate câmpurile, inelele descrise în cuvinte pentru cititoarele de ecran.
- Respectă „reduce motion” și mărimea textului setată pe telefon.
- Buget de performanță: ecranul „Azi” util în < 1,5 s pe un telefon Android mediu, pe 4G; interacțiunile răspund în < 100 ms; fără biblioteci grele fără motiv.

## 10. Procesul de design (înainte și în timpul codului)

1. **Sistemul de design întâi.** Tokenii și componentele de bază (avatar cu inel, bloc de ședință, rând de bani, foaie de jos, toast cu anulare, stare goală) se definesc într-un Design System (artifact de tip Design System sau Figma), înainte de ecrane.
2. **Ecranele-semnătură înainte de cod.** „Azi”, fișa clientului, „Bani”, programarea rapidă, onboarding-ul și pagina publică. Pentru „Azi” se fac 2–3 direcții diferite și se alege una argumentat.
3. **Review pe capturi de ecran** la fiecare pull request, la 390 px și 1280 px, în modurile luminos, întunecat și teren, față de lista de mai jos.
4. **Testul de teren:** pe un telefon real, afară, cu o mână. Dacă ceva nu se vede sau nu se nimerește, nu e gata.
5. **Testul cu oameni:** 3 antrenori, sarcini cronometrate (vezi `docs/PRODUCT.md`, secțiunea 12).

### Lista de verificare pentru fiecare ecran
- [ ] Se înțelege în 2 secunde ce e important pe ecran?
- [ ] Culoarea apare doar unde transmite o stare sau o acțiune principală?
- [ ] Acțiunea principală e la un tap și în zona degetului mare?
- [ ] Arată bine în modul teren, în soare?
- [ ] Starea goală, încărcarea, eroarea și modul offline sunt proiectate, nu lăsate implicite?
- [ ] Textele sunt scurte, în română corectă, cu terminologia din pachetul de nișă?
- [ ] Ar putea fi confundat cu orice alt dashboard SaaS? Dacă da, revizuiește.
- [ ] Ce element poți scoate fără să pierzi nimic? Scoate-l.
