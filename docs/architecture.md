# Arhitectură

Aplicația are 3 straturi: clientul React (SPA), API-ul REST făcut cu Express și baza de date MySQL. Frontend-ul vorbește cu backend-ul doar prin API.

## Diagrama de arhitectură

```mermaid
flowchart LR
    U[Utilizator / Admin] --> FE

    subgraph Client
        FE[React SPA<br/>React Router + Chart.js]
    end

    subgraph Server["Server Node.js + Express"]
        API[Rute REST]
        MW[Middleware<br/>JWT + roluri + validări]
        SRV[Servicii<br/>logica de business]
        CRON[Job node-cron<br/>plăți recurente]
        MAIL[Nodemailer]
    end

    DB[(MySQL)]
    SMTP[Server SMTP]

    FE -->|HTTP + JWT| API
    API --> MW --> SRV
    SRV -->|mysql2| DB
    CRON --> SRV
    SRV --> MAIL --> SMTP
    SMTP -.->|cod de verificare| U
```

## Componente

| Componentă | Tehnologie | Rol |
|---|---|---|
| Frontend | React (SPA), React Router, Chart.js | ecranele din wireframes, apelează API-ul |
| API | Node.js + Express | rute REST, validări, logica de business |
| Autentificare | JWT, bcrypt | login, parole hash-uite, middleware pentru roluri |
| Email | Nodemailer | trimite codul de verificare, cu tratarea erorilor |
| Joburi | node-cron | generează zilnic tranzacțiile din plățile recurente |
| Bază de date | MySQL (`mysql2`, fără ORM) | datele din [data-model.md](data-model.md), cu tranzacții SQL |

## Fluxuri principale

### Înregistrare cu cod pe email (UC1)

```mermaid
sequenceDiagram
    actor U as Utilizator
    participant FE as React
    participant API as Express
    participant DB as MySQL
    participant M as Nodemailer

    U->>FE: email + parolă
    FE->>API: POST /api/auth/register
    API->>API: validează datele, hash la parolă
    API->>DB: salvează user (neverificat) + cod cu expirare
    API->>M: trimite codul
    alt email trimis
        M-->>U: cod de verificare
        API-->>FE: 201, cere codul
        U->>FE: introduce codul
        FE->>API: POST /api/auth/verify
        API->>DB: verifică codul, activează contul
        API-->>FE: cont activ
    else email eșuat
        API-->>FE: eroare clară în interfață
    end
```

### Adăugare tranzacție cu categorii multiple (UC2)

```mermaid
sequenceDiagram
    actor U as Utilizator
    participant FE as React
    participant API as Express
    participant DB as MySQL

    U->>FE: completează formularul
    FE->>API: POST /api/transactions (JWT)
    API->>API: verifică JWT, validează datele și categoriile
    API->>DB: BEGIN
    API->>DB: INSERT în transactions
    API->>DB: INSERT în transaction_categories
    API->>DB: INSERT în recurring_payments (dacă e recurentă)
    API->>DB: COMMIT
    API-->>FE: tranzacția salvată
    FE->>API: GET /api/dashboard
    API->>DB: calculează sold, bugete, alerte
    API-->>FE: date actualizate
    FE-->>U: dashboard actualizat, fără refresh complet
```

## Structura proiectului

```
smartbudget/
├── client/                  # React
│   └── src/
│       ├── pages/           # Login, Dashboard, Tranzacții, Bugete...
│       ├── components/      # navbar, tabele, dialoguri, formulare
│       └── api/             # apelurile către backend
└── server/                  # Express
    └── src/
        ├── routes/          # auth, transactions, budgets, goals...
        ├── middleware/      # JWT, roluri, validări
        ├── services/        # logica de business
        ├── jobs/            # job-ul pentru plăți recurente
        └── db/              # conexiune MySQL, scripturi SQL
```

## Securitate

- Parolele se salvează cu bcrypt, nu în clar.
- Codul de verificare expiră și se poate folosi o singură dată.
- Rutele de după login cer JWT, iar rutele `/api/admin` cer și rol de admin.
- Fiecare utilizator vede doar datele lui: interogările filtrează după `user_id` din JWT.
- Datele sunt validate pe server, nu doar în React.
- Interogările SQL sunt parametrizate, ca să evităm SQL injection.
