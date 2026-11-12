# Cazuri de utilizare SmartBudget

Cerințele (FR) sunt în [requirements.md](requirements.md).

## UC1: Înregistrare și verificare cu cod pe email

**Actor:** vizitator (utilizator neînregistrat)
**Precondiții:** nu are cont creat cu emailul respectiv.

**Pași principali**
1. Vizitatorul deschide pagina de Sign Up și introduce email și parolă.
2. Sistemul validează datele și creează contul în stare „neverificat".
3. Sistemul trimite pe email un cod de verificare cu expirare.
4. Vizitatorul introduce codul în aplicație.
5. Sistemul verifică codul și activează contul.
6. Utilizatorul este redirecționat către login/dashboard.

**Scenarii alternative**
- **2a.** Email deja folosit sau parolă invalidă: se afișează eroare, contul nu se creează.
- **3a.** Emailul nu poate fi trimis: se afișează un mesaj clar de eroare.
- **4a.** Cod greșit: eroare, utilizatorul poate reîncerca.
- **4b.** Cod expirat: utilizatorul poate cere un cod nou.

**Rezultat așteptat:** contul este activ și utilizatorul se poate loga cu email și parolă.

**Criterii de acceptare**
- [ ] Contul nu devine activ fără cod valid (FR2)
- [ ] Parola e salvată hash-uită (NFR1)
- [ ] Un cod expirat sau deja folosit este respins (NFR2)
- [ ] Eroarea la trimiterea emailului este afișată în interfață (FR3)

---

## UC2: Adăugare tranzacție cu categorii multiple

**Actor:** utilizator autentificat
**Precondiții:** este logat și există cel puțin o categorie (predefinită sau custom).

**Pași principali**
1. Utilizatorul apasă „Adaugă tranzacție".
2. Alege tipul (venit sau cheltuială), introduce suma, data și o descriere.
3. Alege una sau mai multe categorii.
4. (Opțional) Bifează „plată recurentă" și alege frecvența: zilnic, săptămânal, lunar sau anual.
5. Apasă „Salvează".
6. Serverul validează datele și salvează tranzacția.
7. Dashboard-ul își actualizează soldul și bugetele categoriilor alese.

**Scenarii alternative**
- **6a.** Sumă invalidă (zero, negativă sau text): serverul respinge cererea și se afișează eroare.
- **6b.** Nicio categorie aleasă: tranzacția nu se salvează, se cere cel puțin o categorie.
- **4a.** Dacă e bifată recurența, sistemul generează automat tranzacția și la următoarea dată scadentă.

**Rezultat așteptat:** tranzacția apare în listă, soldul e actualizat, iar suma se reflectă în bugetele categoriilor alese.

**Criterii de acceptare**
- [ ] Tranzacția se salvează cu mai multe categorii (FR7, FR8)
- [ ] Datele invalide sunt respinse de server (FR9)
- [ ] Soldul și bugetele se actualizează fără refresh complet (FR10, FR20)
- [ ] Tranzacția recurentă are frecvența salvată și se generează la scadență (FR11, FR12)

---

## UC3: Setare buget și primire alertă

**Actor:** utilizator autentificat
**Precondiții:** este logat și are cel puțin o categorie.

**Pași principali**
1. Utilizatorul intră în secțiunea Bugete și apasă „Buget nou".
2. Alege o categorie sau un grup de categorii, suma limită și perioada (de exemplu o lună).
3. Salvează bugetul.
4. Utilizatorul adaugă tranzacții de cheltuială pe categoriile respective (vezi UC2).
5. Sistemul calculează cheltuielile din perioadă față de limită.
6. La 80% din limită, dashboard-ul afișează un avertisment.
7. La 100% sau peste, dashboard-ul afișează o alertă de depășire.

**Scenarii alternative**
- **2a.** Limita este zero sau negativă: serverul respinge bugetul.
- **5a.** O tranzacție cu mai multe categorii: suma intră în fiecare buget al categoriilor asociate.
- **5b.** Dacă tranzacția este ștearsă sau modificată, starea bugetului se recalculează.

**Rezultat așteptat:** utilizatorul vede în dashboard cât a cheltuit din buget și primește avertisment sau alertă când e cazul.

**Criterii de acceptare**
- [ ] Bugetul se poate seta pe categorie sau grup de categorii, pe perioadă (FR13)
- [ ] La 80% apare avertisment (FR14)
- [ ] La 100% apare alertă de depășire (FR15)
- [ ] Starea bugetelor este vizibilă în dashboard (FR19)

---

## UC4: Statistici pe interval personalizat și export CSV

**Actor:** utilizator autentificat
**Precondiții:** este logat și are tranzacții salvate.

**Pași principali**
1. Utilizatorul deschide pagina Statistici.
2. Alege un interval prestabilit (de exemplu luna aceasta) sau o perioadă personalizată (data de început și de sfârșit).
3. Aplicația afișează graficele de venituri și cheltuieli pe categorii și pe zile.
4. Utilizatorul apasă „Export CSV".
5. Aplicația generează fișierul și îl descarcă local.

**Scenarii alternative**
- **2a.** Data de început este după cea de sfârșit: se afișează eroare și nu se aplică filtrul.
- **3a.** Nu există tranzacții în interval: se afișează un mesaj că nu sunt date, iar exportul nu se face.

**Rezultat așteptat:** utilizatorul vede graficele pentru perioada aleasă și primește un fișier CSV cu tranzacțiile și sinteza perioadei.

**Criterii de acceptare**
- [ ] Graficele se actualizează după intervalul ales (FR21, FR22)
- [ ] CSV-ul conține doar tranzacțiile din interval (FR23)
- [ ] CSV-ul include sinteza pe perioadă și se deschide corect în Excel (FR23)
