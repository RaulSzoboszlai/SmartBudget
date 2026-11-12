# Cerințe SmartBudget

Prioritate: **Mare** = obligatoriu, **Medie** = opțional.

## Cerințe funcționale

### Autentificare
| ID | Descriere | Prioritate |
|---|---|---|
| FR1 | Utilizatorul își poate crea cont cu email și parolă (sign up). | Mare |
| FR2 | După sign up, sistemul trimite pe email un cod de verificare cu expirare, iar contul se activează doar după introducerea lui. La login se cer doar email și parolă. | Mare |
| FR3 | Dacă emailul nu poate fi trimis, aplicația afișează un mesaj clar de eroare. | Mare |
| FR4 | Utilizatorul se poate loga și deconecta (logout). | Mare |

### Categorii
| ID | Descriere | Prioritate |
|---|---|---|
| FR5 | Există categorii predefinite, disponibile tuturor utilizatorilor. | Mare |
| FR6 | Utilizatorul poate adăuga, edita și șterge categorii custom. | Mare |

### Tranzacții
| ID | Descriere | Prioritate |
|---|---|---|
| FR7 | Utilizatorul poate adăuga, vedea, modifica și șterge tranzacții (venit sau cheltuială). | Mare |
| FR8 | O tranzacție poate avea una sau mai multe categorii (predefinite sau custom). | Mare |
| FR9 | Datele tranzacției sunt validate pe server înainte de salvare. | Mare |
| FR10 | Suma unei tranzacții se reflectă în bugetele categoriilor asociate și în soldul total. | Mare |

### Plăți recurente
| ID | Descriere | Prioritate |
|---|---|---|
| FR11 | O tranzacție poate fi marcată ca recurentă, cu frecvență zilnică, săptămânală, lunară sau anuală. | Mare |
| FR12 | Sistemul generează automat tranzacția la data scadentă. | Mare |

### Bugete și alerte
| ID | Descriere | Prioritate |
|---|---|---|
| FR13 | Utilizatorul setează o limită de buget pentru o categorie sau un grup de categorii, pe o perioadă. | Mare |
| FR14 | La 80% din limită apare un avertisment în dashboard. | Mare |
| FR15 | La 100% (depășire) apare o alertă în dashboard. | Mare |

### Goals
| ID | Descriere | Prioritate |
|---|---|---|
| FR16 | Utilizatorul creează un goal de economisire cu o sumă țintă. | Mare |
| FR17 | Utilizatorul adaugă sume la goal și vede progresul. | Mare |

### Dashboard
| ID | Descriere | Prioritate |
|---|---|---|
| FR18 | Dashboard-ul afișează venituri, cheltuieli și sold. | Mare |
| FR19 | Dashboard-ul afișează starea bugetelor, progresul goal-urilor și plățile recurente. | Mare |
| FR20 | Datele din dashboard se actualizează în timp real, după fiecare modificare. | Mare |

### Statistici și export
| ID | Descriere | Prioritate |
|---|---|---|
| FR21 | Utilizatorul vede grafice de venituri/cheltuieli pe categorii și pe zile. | Mare |
| FR22 | Perioada poate fi aleasă dintr-un interval prestabilit sau personalizată. | Mare |
| FR23 | Utilizatorul poate exporta în CSV tranzacțiile și sinteza pentru perioada aleasă. | Mare |

### Panou admin
| ID | Descriere | Prioritate |
|---|---|---|
| FR24 | Adminul poate vedea, bloca și șterge utilizatori. | Mare |
| FR25 | Adminul poate gestiona categoriile predefinite. | Mare |

### Profiluri de cheltuieli
| ID | Descriere | Prioritate |
|---|---|---|
| FR26 | Utilizatorul poate crea profiluri separate (ex. „Vacanță") și le poate edita sau șterge. | Medie |
| FR27 | Tranzacțiile pot fi atribuite unui profil, iar profilul se vede izolat de bugetul general. | Medie |

## Cerințe nefuncționale

| ID | Categorie | Descriere |
|---|---|---|
| NFR1 | Securitate | Parolele se stochează hash-uite, nu în clar. |
| NFR2 | Securitate | Codul de verificare expiră după un timp scurt și se poate folosi o singură dată. |
| NFR3 | Securitate | Toate datele sunt validate pe server, nu doar în frontend. |
| NFR4 | Performanță | Răspunsurile API sunt rapide, iar dashboard-ul se actualizează fără refresh complet al paginii. |

## În afara scopului
- conectare la bănci prin Open Banking
- recomandări de investiții cu AI
- import CSV de tranzacții (posibil în viitor)
