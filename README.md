# SmartBudget

SmartBudget este o aplicație web de tip Money Manager, făcută pentru materia Tehnologii Web. Te ajută să-ți urmărești veniturile și cheltuielile, să îți setezi bugete pe categorii și să economisești pentru obiective.

## Problema abordată

Mulți oameni nu știu exact pe ce se duc banii zilnic, nu se țin de bugetul lunar și uită de plățile recurente (facturi, abonamente). Nu există o soluție simplă, într-un singur loc, care să le arate clar cum stau cu banii și să îi avertizeze din timp când sunt aproape de limită.

## Utilizatori vizați

- tineri și studenți
- persoane active profesional
- familii care vor să-și monitorizeze finanțele personale

## Obiective

- **O1:** autentificare securizată (email, parolă și cod de verificare), funcțională până la prototip.
- **O2:** dashboard dinamic cu venituri, cheltuieli, starea bugetelor și progresul goal-urilor, în timp real.
- **O3:** modul de statistici cu filtrare pe intervale personalizate și export CSV corect formatat.
- **O4:** gestionarea tranzacțiilor cu categorii multiple și a bugetelor cu alerte, funcțională până la prototip.

## Funcționalități

**Obligatorii**
- autentificare cu cod trimis pe email
- tranzacții (venit/cheltuială) cu mai multe categorii, predefinite sau custom
- bugete pe categorii, cu alerte la apropierea sau depășirea limitei
- plăți recurente
- obiective de economisire (goals)
- dashboard principal
- statistici cu grafice și filtre pe perioadă
- export CSV
- panou de admin

**Opțional**
- profiluri de cheltuieli separate (ex. vacanță, renovare)

**În afara scopului:** conectarea la bănci prin Open Banking (tranzacțiile se introduc manual sau prin import CSV) și recomandări de investiții bazate pe AI.

## Tehnologii

MERN adaptat: **MySQL** în loc de MongoDB, deci MySQL, Express, React, Node.js.

- **React:** dezvoltare rapidă, single page application care consumă un REST API.
- **Express (Node.js):** același limbaj (JavaScript) ca în frontend, ecosistem mare.
- **MySQL:** bază de date relațională, ACID, potrivită pentru tranzacții financiare.
- **Altele:** JWT și bcrypt pentru autentificare, Nodemailer pentru codul pe email, node-cron pentru plățile recurente, Chart.js pentru grafice.

## Echipa

| Nume | Email | Responsabilități |
|---|---|---|
| Schipor Devis | devis.schipor05@e-uvt.ro | Dashboard, statistici, export CSV, panou admin |
| Szoboszlai Raul Cristian | raul.szoboszlai05@e-uvt.ro | Autentificare, categorii, tranzacții CRUD cu categorii multiple |
| Parfene Daniel Emanuel | daniel.parfene04@e-uvt.ro | Bugete și alerte, plăți recurente, goals, profiluri (opțional) |

## Documentație

| Document | Stare |
|---|---|
| [Cerințe](docs/requirements.md) | gata |
| [Cazuri de utilizare](docs/use-cases.md) | gata |
| [Wireframes (fișiere HTML)](docs/wireframes/) | gata |
| [Flux de navigare](docs/wireframes/flow.md) | gata |
| [Model de date și endpoint-uri](docs/data-model.md) | gata |
| [Arhitectură](docs/architecture.md) | gata |
| [Plan de implementare](docs/implementation-plan.md) | gata |
