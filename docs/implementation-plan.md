# Plan de implementare

Avem cam 6 săptămâni, așa că planul are 6 sprint-uri de câte o săptămână. Sunt orientative, nu ne luăm strict după ele.

## Justificarea tehnologiilor

| Tehnologie | De ce |
|---|---|
| React | dezvoltare rapidă, single page application, consumă API-ul REST |
| Node.js + Express | același limbaj (JavaScript) în frontend și backend, ușor de pornit |
| MySQL | relațională și ACID, potrivită pentru tranzacții financiare și pentru legăturile many-to-many |
| JWT + bcrypt | autentificare simplă fără sesiuni pe server, parole hash-uite |
| Nodemailer | trimite codul de verificare pe email, cu tratarea erorilor |
| node-cron | generează tranzacțiile din plățile recurente, în același proces cu Express |
| Chart.js | grafice pentru statistici, ușor de folosit în React |

## Strategia de versionare

Git + GitHub, fără pull request-uri.

- `dev` este branch-ul pe care lucrăm zilnic.
- Când ceva merge, facem merge din `dev` în `main`. `main` rămâne varianta stabilă.
- Commit-uri mici, cu mesaje clare (de exemplu `add login endpoint`).
- `git pull` înainte de `git push`, ca să evităm conflictele.
- Fiecare lucrează în folderele și fișierele modulului lui, ca să ne suprapunem cât mai puțin.

## Planificare pe sprint-uri

| Sprint | Conținut | Rezultat |
|---|---|---|
| 1 | Setup proiect (repo, client și server, conexiune MySQL, schema SQL), autentificare (register, verify, login) | utilizatorii se pot înregistra cu cod pe email și se pot loga |
| 2 | Categorii (predefinite și custom), tranzacții CRUD cu categorii multiple, bugete cu alerte | se pot adăuga tranzacții și bugete |
| 3 | Dashboard, statistici cu grafice, export CSV | **prototip funcțional** (O1-O4) |
| 4 | Goals, plăți recurente cu job node-cron | goals și recurente funcționale |
| 5 | Panou admin, profiluri de cheltuieli (opțional), finisări de interfață | toate funcționalitățile gata |
| 6 | Teste manuale, rezolvat bug-uri, completat documentația | versiunea finală |

Dacă nu ajungem la tot, profilurile (opționale) rămân la urmă.

## Prioritizarea activităților

| Prioritate | Ce intră | Când |
|---|---|---|
| Mare (obligatoriu) | autentificare cu cod, categorii, tranzacții, bugete și alerte, dashboard, statistici, export CSV, goals, plăți recurente, admin | sprint-urile 1-5 |
| Medie (opțional) | profiluri de cheltuieli | sprint 5, dacă mai avem timp |

Cerințele detaliate sunt în [requirements.md](requirements.md).

## Repartizarea responsabilităților

| Membru | Sarcini | Sprint-uri |
|---|---|---|
| Schipor Devis | dashboard, statistici, export CSV, panou admin | 3 și 5 |
| Szoboszlai Raul Cristian | setup autentificare, categorii, tranzacții CRUD cu categorii multiple | 1 și 2 |
| Parfene Daniel Emanuel | bugete și alerte, goals, plăți recurente, profiluri (opțional) | 2, 4 și 5 |

Setup-ul proiectului din sprint 1 îl facem împreună. Sprint 6 e pentru toți. Repartizarea e orientativă și ne ajutăm între noi dacă cineva rămâne în urmă.
