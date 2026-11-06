# PRODUCT.md – Specificația de produs

## 1. De ce există produsul

Antrenorii, instructorii și cluburile mici își conduc afacerea pe WhatsApp, în caiete și în Excel. Pierd bani din pachete neîncasate, pierd clienți care pleacă fără ca nimeni să observe și pierd ore pe săptămână cu organizare.

**Promisiunea:** *„Deschizi aplicația, vezi ziua, marchezi prezența, iar restul se face singur: ședințele se scad, banii se urmăresc, clienții primesc remindere.”*

Nu vindem „un sistem de management”. Vindem **ore câștigate și bani recuperați**, măsurabile.

### De ce e de 10 ori mai bun decât ce folosesc acum

| Situație | Azi (WhatsApp + caiet + Excel) | Cu platforma |
| --- | --- | --- |
| Cine vine azi? | Derulezi conversații | Ecranul „Azi”, deschis în 1 secundă |
| Câte ședințe mai are clientul? | Numeri în caiet | Inelul de pe avatar, actualizat automat |
| Cine îmi datorează bani? | Ții minte (sau nu) | Lista „Bani”, cu sume și vechime |
| Cer banii | Mesaj scris de mână, jenant | Un tap: mesaj politicos, cu suma, gata trimis pe WhatsApp |
| Pachetul se termină | Afli când e prea târziu | Propunere de reînnoire la 2 ședințe rămase |
| Clientul dispare | Observi după o lună | Alertă după 2–3 săptămâni de absență |
| Părintele întreabă de progres | Mesaj lung, improvizat | Fișă de progres clară (V2: rezumat automat) |

## 2. Persoane și ce vor să rezolve

**Profesionistul independent** (primul utilizator: eu, antrenor de tenis)
- Să știu în 2 secunde ce am azi și cine are probleme (pachet terminat, restanță).
- Să marchez prezența fără să mă opresc din antrenament.
- Să încasez la timp fără să par insistent.
- Să-mi umplu golurile din program.
- Să arăt profesionist în fața părinților și clienților noi.

**Proprietarul de club**
- Să văd luni dimineață, în 3 cifre, cum merge clubul.
- Să știu ce antrenor e plin, ce antrenor pierde clienți, ce terenuri stau goale.
- Să nu mai existe suprapuneri și haos la recepție.

**Recepția / administratorul**
- Programări, înscrieri și încasări rapide, fără să sune antrenorul.

**Părintele** (plătitorul, de multe ori)
- Știe programul, câte ședințe mai are copilul, cât are de plătit și ce progres face.

**Clientul adult**
- Vede programul, ședințele rămase, se înscrie la evenimente.

## 3. Fluxurile esențiale (cu ținte măsurabile)

Acestea sunt inima produsului. Orice funcționalitate există ca să le facă mai rapide.

### F1. Ziua antrenorului
1. Deschide aplicația → aterizează pe „Azi”.
2. Vede ședințele zilei în ordine, cu fiecare client și starea lui (inel de pachet, restanță, prima ședință, aniversare).
3. Marchează prezența: un tap pe avatar = prezent; ține apăsat = absent / anulat târziu.
4. Ședința se scade automat din pachet. Dacă pachetul ajunge la 2, apare propunerea de reînnoire.

**Ținte:** de la deschidere la ecranul util < 1,5 s pe un telefon mediu, pe 4G; marcarea prezenței pentru o grupă de 4 < 5 s; funcționează fără semnal și se sincronizează după.

### F2. Încasarea
1. Ecranul „Bani” arată: restanțe (cine, cât, de când), pachete de reînnoit, încasări recente.
2. Un tap pe „Trimite reminder” deschide WhatsApp cu un mesaj politicos, completat cu suma și instrucțiunile de plată.
3. Marcarea plății: sumă precompletată, metodă (numerar / card / transfer), un tap.

**Ținte:** de la „cine îmi datorează?” la reminder trimis < 10 s. Fiecare restanță are vechimea vizibilă.

### F3. Reînnoirea pachetului
- La ≤ 2 ședințe rămase sau ≤ 7 zile până la expirare: sugestie în „Azi” și în „Bani”.
- Un tap creează pachetul nou cu aceleași condiții; altul trimite mesajul de reînnoire.

**Țintă:** reînnoire în < 3 tap-uri.

### F4. Umplerea golurilor
- O ședință anulată eliberează un loc → aplicația sugerează clienții potriviți (listă de așteptare, clienți care au cerut mai multe ședințe, același nivel).
- Un tap trimite oferta pe WhatsApp.

### F5. Onboarding în 5 minute
1. Alege tipul de cont (independent / organizație) și nișa → pachetul de nișă aduce terminologia, nivelurile și serviciile tipice.
2. Ajustează serviciile și prețurile (precompletate).
3. Adaugă clienții: din contactele telefonului, din CSV sau manual (nume + telefon e suficient).
4. Programează prima ședință.

**Țintă:** de la cont nou la prima ședință programată < 10 minute, fără ajutor. Măsoară și optimizează.

### F6. Rezumatul săptămânal (duminică seara)
Email scurt: ședințe ținute, bani încasați, restanțe, clienți în risc, săptămâna următoare. Fără să deschidă aplicația, utilizatorul știe unde e.

### F7. Lunea proprietarului de club
Un ecran cu 3 cifre mari (încasări luna aceasta față de luna trecută, ocuparea, clienți în risc), apoi detaliile per antrenor și per resursă.

## 4. Automatizări (platforma lucrează)

| Automatizare | Declanșator | Ce face | Versiune |
| --- | --- | --- | --- |
| Consum ședință | Prezență marcată | Scade din pachetul activ potrivit | V1 |
| Reminder ședință | X ore înainte | Email (V1), WhatsApp API (V2) | V1 |
| Restanță | Pachet fără plată după X zile | Apare în „Bani”, sugerează reminder | V1 |
| Reînnoire | ≤ 2 ședințe sau ≤ 7 zile | Sugestie + mesaj pregătit | V1 |
| Listă de așteptare | Loc eliberat la eveniment | Promovează următorul, îl anunță | V1 |
| Rezumat săptămânal | Duminică, 19:00 | Email către profesionist / proprietar | V1 |
| Radar de retenție | Fără prezență de 2–3 săptămâni | Alertă + mesaj „ne e dor de tine” pregătit | V2 |
| Rezumat de progres | Lunar | Generat din notițe, trimis părintelui după aprobare | V2 |
| Umplere goluri | Ședință anulată | Sugestii de clienți + ofertă | V2 |

**WhatsApp în V1:** prin linkuri care deschid WhatsApp cu mesajul precompletat (fără API, fără cost, funcționează imediat). Integrarea cu API-ul oficial vine în V2, când volumul o justifică. Orice mesaj automat către clienți se trimite doar cu confirmarea utilizatorului în V1.

## 5. Scopul pe versiuni

### V1 – „Săptămâna antrenorului și un club pilot”
- Onboarding cu pachet de nișă (F5)
- „Azi” (F1) cu prezență offline
- Clienți: fișă, nivel, etichete, părinte/tutore cu acord, istoric, căutare
- Servicii și pachete: N ședințe, abonament lunar, limită pe săptămână, per ședință; reguli de anulare târzie
- Program: individual și grup, recurent, detectare suprapuneri (profesionist, resursă, client)
- „Bani”: încasări, restanțe, sold per client, remindere WhatsApp (F2, F3)
- Evenimente simple: capacitate, nivel, vârstă, listă de așteptare automată
- Pagina publică cu formular de înscriere configurabil și acord GDPR
- Mai mulți profesioniști pe organizație și roluri de bază (pentru clubul pilot)
- Import CSV de clienți
- Rezumat săptămânal pe email (F6), ecranul proprietarului (F7, varianta simplă)

**V1 e gata când:** eu îmi conduc săptămâna doar din platformă și un club pilot cu 3+ antrenori face la fel, timp de 2 săptămâni, fără WhatsApp sau caiet pentru evidență.

### V2 – „Retenție și bani online”
Radar de retenție, progres cu abilități și clipuri, rezumate de progres pentru părinți, portal client, resurse cu ocupare, rapoarte complete, plăți online și facturare, abonamentul platformei, WhatsApp API, umplerea golurilor.

### V3 – „Creștere”
Asistent AI de conținut, recomandări, mai multe locații, integrare calendar, aplicație mobilă nativă (dacă PWA nu ajunge), nișe noi la cerere.

### Niciodată (fără decizia mea explicită)
Marketplace de terenuri, descoperire de jucători, rețea socială, chat intern (WhatsApp există deja).

## 6. Pachete de nișă

Un pachet de nișă e **configurare versionată** (JSON validat cu schemă), aplicată la crearea organizației și editabilă oricând. Codul nu știe ce sport e.

| Element | Tenis | Școală de dans | Meditații |
| --- | --- | --- | --- |
| Terminologie | Antrenor, Sportiv, Antrenament, Teren | Instructor, Cursant, Curs, Sală | Profesor, Elev, Oră, Cabinet |
| Niveluri | Roșu, Portocaliu, Verde, Galben; Începător → Avansat | Începător, Intermediar, Avansat | Clasa a V-a … a XII-a |
| Abilități urmărite | Forehand, rever, serviciu, voleu, deplasare | Tehnică, ritm, coregrafie | Materii, note la teste |
| Servicii tipice | Individual, grup 2–4, grupă copii | Curs de grup, lecție privată | Oră individuală, grupă |
| Pachete tipice | 8 / 12 ședințe, lunar | Lunar, 8 clase | 10 ore |
| Resurse | Teren zgură, hard, padel | Sală mare, sală mică | Cabinet, online |
| Evenimente | Turneu, tabără, social padel | Spectacol, workshop | Simulare examen |
| Câmpuri extra | Mână dominantă, rachetă | Stil preferat | Școală, examen țintă |

Ordinea de pregătire: **tenis, padel**; apoi, doar la cerere reală: fotbal, înot, dans, yoga/pilates, arte marțiale, muzică, meditații, personal training, kinetoterapie.

**Regulă:** dacă o nișă nouă cere cod nou, oprește-te și discută cu mine. Probabil nucleului îi lipsește un concept generic.

### Terminologie: concepte interne → etichete afișate

| Intern (cod) | Etichete posibile |
| --- | --- |
| `Professional` | Antrenor, Instructor, Profesor, Terapeut |
| `Client` | Client, Elev, Sportiv, Membru, Cursant |
| `Guardian` | Părinte, Tutore |
| `Session` | Ședință, Lecție, Antrenament, Oră, Curs |
| `Offering` | Serviciu, Program, Curs, Clasă |
| `Package` | Pachet, Abonament, Card |
| `Resource` | Teren, Sală, Studio, Bazin, Cabinet |
| `Event` | Turneu, Tabără, Workshop, Competiție, Social |
| `Level` | Nivel, Centură, Grupă, Categorie |

## 7. Roluri și permisiuni

| Rol | Poate |
| --- | --- |
| Owner | Tot, inclusiv setări, rapoarte financiare, roluri, abonamentul platformei |
| Admin | Clienți, profesioniști, program, evenimente; fără abonamentul platformei |
| Professional | Clienții, programul, prezența și progresul alocate lui (vizibilitatea extinsă e configurabilă) |
| Recepție | Programări, înscrieri, încasări; fără rapoarte financiare |
| Client / Guardian | Propriul program, pachete, sold, progres; înscriere la evenimente (portal în V2) |
| Public | Pagina publică și formularul |

Permisiunile se verifică în baza de date (RLS) și pe server, nu doar în interfață. Un utilizator poate avea roluri în mai multe organizații.

## 8. Modelul de date (punct de pornire)

```
Organization         tip (independent | organization), plan, niche_pack_version, timezone, currency, locale
 ├── NicheConfig     terminologie, niveluri, abilități, câmpuri, reguli (versionat)
 ├── Location        (V3)
 ├── Resource        tip, disponibilitate
 ├── Membership      user × organizație × rol
 ├── Client          date, nivel, etichete, custom_fields, status
 │    ├── GuardianLink    client ↔ guardian, consimțământ (cine, când, pentru ce)
 │    ├── ClientPackage   din PackageTemplate; total, rămase, valabilitate, status
 │    ├── ProgressRecord  abilitate, nivel/scor, notă, media, autor (V2)
 │    └── Note
 ├── Offering        tip, durată, preț, capacitate
 ├── PackageTemplate tip (count | monthly | weekly_limit | per_session), reguli
 ├── Session         offering, profesionist, resursă, interval, recurență, status
 │    └── Attendance  client, status (present | absent | late_cancel), client_package consumat, sync_state
 ├── Event           tip, interval, preț, capacitate, nivel minim, vârstă
 │    └── Registration  client sau date publice, status (confirmed | waitlist | cancelled), poziție
 ├── Payment         sumă (subunități), monedă, metodă, dată, legătură (pachet | eveniment | ședință)
 ├── MessageLog      șablon, canal, destinatar, status (pentru remindere)
 ├── CustomFieldDefinition
 └── AuditLog        actor, acțiune, entitate, vechi → nou, moment
```

- `organization_id` pe tot, RLS pe tot.
- Prezența offline are id generat pe client și se sincronizează idempotent (de două ori sincronizat = o singură prezență).
- Ștergere soft pentru date de business; ștergere reală doar la cerere GDPR.

## 9. Securitate și GDPR

- Izolare strictă între organizații, testată automat.
- Minori: tutore obligatoriu, consimțământ înregistrat; media cu minori doar cu acord explicit.
- Export complet și ștergere la cerere pentru fiecare client.
- AuditLog pentru pachete, plăți, prezență, permisiuni.
- Fără date personale în URL-uri, loguri, erori. Paginile publice nu expun clienți.

## 10. Planurile platformei (ipoteze de validat)

| Plan | Pentru | Preț orientativ |
| --- | --- | --- |
| Pro | Profesionist independent | ~99 lei / lună |
| Club | Organizație mică | ~2.000–5.000 lei implementare + ~300–600 lei / lună |
| Multi-locație | Rețele | La cerere |

Funcționalitățile se activează prin feature flags pe plan.

## 11. Metrici de succes

Le instrumentăm din V1 (evenimente anonime, fără date personale):

| Metrică | Țintă inițială |
| --- | --- |
| Timp de la cont nou la prima ședință programată | < 10 minute |
| Timp median de marcare a prezenței per ședință | < 3 secunde |
| Profesioniști activi săptămânal / total | > 80% |
| Restanțe recuperate în 30 de zile | Măsurăm și creștem |
| Rata de reînnoire a pachetelor | Măsurăm și creștem |
| Timp de administrare economisit (declarat, lunar) | > 2 ore / săptămână |

## 12. Validare cu oameni reali

- Fiecare flux F1–F5 se testează cu cel puțin 3 antrenori reali înainte de a fi declarat terminat: le dai o sarcină, cronometrezi, observi unde ezită.
- Ezitarea e un bug de design. Notează-o în Issue.
