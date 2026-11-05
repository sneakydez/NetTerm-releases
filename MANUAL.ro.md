# Manualul NetTerm

NetTerm este un client de terminal pentru Windows, pentru conectarea la routere, switch-uri, servere și
Raspberry Pi prin **SSH, Telnet, SFTP și FTP**, cu butoane care trimit comenzi sau parole dintr-un clic.

## 1. Instalare și deschidere

1. Descarcă `NetTerm.exe` de la https://github.com/sneakydez/NetTerm-releases/releases/latest
2. Salvează-l unde vrei (Desktop, `Documents\NetTerm`…). **Nu necesită instalare.**
3. Deschide-l cu dublu clic.
4. Dacă Windows afișează **„Windows a protejat computerul"**, apasă **Mai multe informații → Executare oricum**.
   Apare deoarece programul nu este încă semnat digital; nu este un virus.

Prima dată durează câteva secunde până se deschide, cât timp Windows îl analizează.

## 2. Primii pași

1. Apasă **＋ Sesiune nouă**.
2. Alege protocolul (**SSH**, **Telnet**, **SFTP** sau **FTP**). Portul se completează singur.
3. Scrie un **nume**, **hostul** (IP sau nume) și, dacă vrei, **utilizatorul** și **parola**.
4. Apasă **Salvează și conectează**.

Pentru a te conecta mai târziu: **dublu clic** pe sesiune în panoul din stânga.

## 3. Ecranul

| Zonă | La ce folosește |
|---|---|
| Panoul de sesiuni (stânga) | Sesiunile tale salvate, grupate și cu căutare |
| `☰` (sus în stânga) | Afișează sau ascunde panoul de sesiuni (`Ctrl+B`) |
| File | Una pentru fiecare conexiune. Punctul arată starea: verde conectat, galben se conectează, roșu deconectat. **Trage-le** pentru a schimba ordinea (`Ctrl+Tab` urmează această ordine) |
| `🔍` | Caută și filtrează în terminal (`Ctrl+Shift+F`) |
| `📡` | Trimitere multiplă: scrie în mai multe sesiuni simultan |
| `▥` | Ecran împărțit: vezi 1, 2 sau 4 terminale |
| `⚙` | Preferințe (`Ctrl+,`) |
| `?` | Acest manual (`F1`) |
| Bara de butoane | Butoanele tale de comenzi și parole |
| Bara de jos | Sesiunea activă, utilizatorul, hostul și starea; versiunea NetTerm |

## 4. Sesiuni

- **Grupuri:** scrie un grup când creezi sesiunea (de exemplu „Sediul central") și vor apărea grupate.
- **Căutare:** scrie în „Caută sesiune…" o parte din nume, IP sau grup.
- **Editare, duplicare sau ștergere:** clic dreapta pe sesiune sau creionul ✎ când treci cu mouse-ul.
- **Temă pe sesiune:** în formularul sesiunii, alege o temă proprie. De exemplu, „Producție (roșu)" pentru
  echipamentele critice, ca să nu greșești fereastra.
- **Cheie privată SSH:** în formular, „Cheie privată" → „Răsfoiește…".

### Dacă parola este greșită

NetTerm îți cere parola chiar în terminal (ce scrii nu se vede). Scrie-o și apasă `Enter`.
Dacă funcționează, apare un mesaj care îți oferă să o **salvezi** în sesiune. `Esc` anulează.

> După mai multe încercări eșuate, multe servere (OpenSSH, routere) **îți blochează IP-ul câteva minute**.
> Dacă vezi „Serverul a închis conexiunea", așteaptă și încearcă din nou.

### Reconectare

Dacă închizi o sesiune sau o închide echipamentul (`exit`, timp de inactivitate), apasă `Enter` în fila ei sau clic
dreapta pe filă → **Reconectează**.

Dacă conexiunea **se pierde** (repornirea echipamentului, întreruperea rețelei sau a VPN-ului), o sesiune SSH sau Telnet
**se reconectează singură**: face încercări din ce în ce mai rare (până la una la 30 s) timp de 15 minute. `Enter`
încearcă imediat, iar `Esc` anulează. Dacă parola eșuează, nu mai încearcă și ți-o cere, ca să nu îți fie blocat
utilizatorul. Nicio comandă nu se repetă, iar jurnalul continuă în același fișier. Minutele sau dezactivarea se aleg în
Preferințe → Terminal.

**Keepalive** (la 60 s, tot în Preferințe → Terminal) împiedică un firewall să taie o sesiune inactivă și ajută la
observarea mai rapidă a unei căderi. Nu împiedică închiderea pentru inactivitate configurată pe echipament.

## 5. Lucrul în terminal

- **Copiere:** selectează textul cu mouse-ul; se copiază singur. Și `Ctrl+Shift+C`.
- **Lipire:** clic dreapta, `Ctrl+Shift+V` sau `Ctrl+V`. Dacă textul are **mai multe linii**, NetTerm îți arată
  mai întâi configurația completă, cu numere de linie, și te întreabă dacă vrei să o lipești (ca MobaXterm):
  fiecare linie se execută ca o comandă. Se reglează în Preferințe → Terminal → „Întreabă înainte de a lipi".
- **Meniu contextual:** `Ctrl` + clic dreapta (sau setează clicul dreapta să deschidă mereu meniul, vezi
  Preferințe → Terminal). Opțiuni: Copiază, Lipește, **Evidențiază** cuvântul, Selectează tot, Golește ecranul.
- `Ctrl+C`, `Ctrl+Z`, `Tab`, săgețile… funcționează ca în orice terminal.
- Clic dreapta pe o **filă**: Reconectează, Deschide jurnalul, Golește ecranul, Închide.

### Căutare și filtrare în terminal

Apasă `🔍` sau `Ctrl+Shift+F` (dacă ai text selectat, îl caută direct).

- **Căutare:** scrie cuvântul. Toate potrivirile se marchează cu galben, iar cea curentă cu portocaliu;
  contorul arată „3 din 27". `Enter` merge la următoarea, `Shift+Enter` la cea anterioară, `Esc` închide.
- **Opțiuni:** `Aa` ține cont de majuscule, `ab` doar cuvinte întregi și `.*` folosește o expresie regulată
  (de exemplu `et-0/0/[0-3] +up +down` pentru a vedea interfețele căzute).
- **Filtrează liniile:** arată **doar liniile care conțin cuvântul**, ca un `| include`, dar peste ce ai
  deja pe ecran, fără a relansa comanda. Ideal pentru a verifica o configurație lungă.
  - **Cu cuvântul / Fără cuvânt:** include sau exclude (ca `| exclude`).
  - **Context:** arată în plus 1, 3 sau 5 linii în jurul fiecărei potriviri (cu gri).
  - Fă clic pe o linie pentru a merge la ea în terminal. **Copiază** copiază rezultatul; **Reîmprospătează**
    recitește terminalul dacă a sosit ieșire nouă.

`Ctrl+F` fără `Shift` nu se folosește pentru căutare, deoarece CLI-ul echipamentelor îl folosește pentru a muta cursorul.

### SFTP și FTP

Sesiunile SFTP/FTP deschid o consolă de fișiere. Scrie `help` pentru a vedea comenzile:

| Comandă | Ce face |
|---|---|
| `ls [cale]` | Listează directorul de la distanță |
| `cd <cale>` / `pwd` | Schimbă directorul / vezi unde ești |
| `get <dist> [local]` | Descarcă (implicit în dosarul Descărcări) |
| `put <local> [dist]` | Încarcă un fișier |
| `mkdir`, `rmdir`, `rm`, `mv` | Creează, șterge, redenumește |
| `lcd`, `lls`, `lpwd` | Dosar local |

## 6. Butoane personalizate

Apasă **＋ Buton** în bara de butoane.

- **Comenzi:** una sau mai multe linii; se trimit în ordine, cu întârzierea aleasă (util pentru
  `terminal length 0` + `show running-config`).
- **Parolă:** trimite o parolă salvată (de exemplu cea de `enable`) fără să apară vreodată pe ecran.
- **Apasă Enter la final:** bifează pentru a se executa direct.
- **Scurtătură de la tastatură:** fă clic în câmpul „Scurtătură" și apasă combinația (`Ctrl+Alt+1`, `F5`, `Ctrl+→`…).
  `Ctrl`+literă nu este permis, deoarece terminalul are nevoie de el (`Ctrl+C`, `Ctrl+D`…). Săgețile, Home, End,
  PgUp, PgDn și Insert au nevoie de `Ctrl` sau `Alt`. `Del` elimină scurtătura.
- **Culoare:** pentru a le deosebi dintr-o privire.

Clic dreapta pe un buton pentru a-l **edita, muta sau șterge**. Butonul se aplică filei active
(sau tuturor celor marcate, dacă trimiterea multiplă este activă).

### Editorul de taste

Pentru a atribui texte tastelor fără a crea butoane (ca „Keymap Editor" din SecureCRT):
**Preferințe → Taste**.

1. Alege modificatorii (`Ctrl`, `Alt`, `Shift`) și fă clic pe o tastă de pe tastatura de pe ecran. Poți și să
   faci clic pe tastatură și să apeși combinația reală.
2. Scrie textul pe care trebuie să-l trimită, de exemplu `show interfaces diagnostics optics et-0/0/0`. Poate avea
   mai multe linii.
3. Bifează „Apasă Enter la final" dacă vrei să se execute direct și apasă **Atribuie**.

Culorile tastaturii: albastru = atribuită; verde = scurtătura unui buton; dungă albastră = atribuită cu alți modificatori;
estompată = folosită de NetTerm. Dedesubt ai lista tastelor atribuite, pentru a le edita sau elimina.

## 7. Ecran împărțit

Apasă `▥` și alege:

| Aspect | Scurtătură |
|---|---|
| Un terminal | `Ctrl+Shift+1` |
| Două, unul lângă altul | `Ctrl+Shift+2` |
| Două, sus și jos | `Ctrl+Shift+3` |
| Patru | `Ctrl+Shift+4` |

- Panoul selectat are un **chenar albastru**. Fă clic pe un panou pentru a-l selecta.
- Fă clic pe o **filă** pentru a o afișa în panoul selectat (sau într-un spațiu liber).
- Fiecare panou arată sus numele și starea sesiunii.

## 8. Trimitere multiplă (scrierea în mai multe sesiuni simultan)

1. Deschide sesiunile (de exemplu, toate switch-urile de la un etaj).
2. Apasă `📡` (sau `Ctrl+Shift+M`). Apare o **bară portocalie** și toate sesiunile SSH/Telnet sunt marcate ☑.
3. Demarchează-le pe cele pe care nu le vrei cu ☑ de pe filă („Marchează toate" / „Niciuna" în bara portocalie).
4. Scrie în orice sesiune marcată: **ce tastezi ajunge la toate cele marcate**. Și butoanele.
5. Apasă **Dezactivează** (sau din nou `📡`) când termini.

> ⚠ Ai grijă la modificările de configurație: se aplică simultan tuturor sesiunilor marcate.
> Combină-l cu ecranul împărțit pentru a vedea ce răspunde fiecare echipament.

## 9. Evidențierea cuvintelor

Routerele și switch-urile nu trimit culori, așa că NetTerm le adaugă. Implicit:

| Ce | Culoare |
|---|---|
| `up`, `active`, `connected`, `established`… | Verde aldin |
| `down`, `err-disabled`, `failed`, `error`… | Roșu aldin |
| `administratively down`, `admin-down`, `%Warning`… | Portocaliu |
| Adrese IPv4 și IPv6 | Cyan |
| Adrese MAC (`0050.56c0.0001`, `aa:bb:cc:dd:ee:ff`) | Mov |
| Interfețe agregate / trunk (`ae3`, `BE3.9`, `Port-channel10`, `Eth-Trunk0`, `BAGG1`, `lag1`, `Trk1`…) | Auriu aldin |
| Interfețe de 100G și 400G (`et-0/0/0`, `Hu0/0/0/1`, `HundredGigE…`, `100GE…`, `HGE1/0/49`) | Roz |
| Interfețe de 10G (`xe-0/1/4`, `TenGigE…`, `Te1/1/1`, `XGigabitEthernet…`, `XGE1/0/1`) | Turcoaz |
| Restul interfețelor (`ge-0/0/1`, `Gi0/1`, `lo0`, `GE1/0/1`, `1/1/1`…) | Albastru |

**Evidențiază un cuvânt pe loc:** clic dreapta pe cuvânt în terminal (sau `Ctrl`+clic dreapta) →
**🎨 Evidențiază**. Alege un șablon sau creează unul nou. Se aplică la ceea ce sosește din acel moment.

**Preferințe → Evidențiere:**

- **Șabloane de stil:** culoarea textului, fundal (∅ = fără fundal), **B** aldin, *I* cursiv, U subliniat.
- **Reguli:** la ce se aplică fiecare șablon.
  - *Cuvinte:* cuvinte exacte separate prin virgule (`up, active, connected`). `UP` nu colorează `BACKUP`.
  - *Conține:* ca Cuvinte, dar și în interiorul altor cuvinte: `MPLS` colorează `MPLS_VPN_SLAES`.
  - *Model:* IPv4, IPv6, MAC sau un **tip de interfață**: trunk-uri/agregate, 100G-400G, 40G-25G, 10G, 1G,
    management/logice sau orice interfață. Astfel poți da fiecărui tip culoarea dorită.
  - *Regex:* expresie regulată (de exemplu `VLAN\d+`). Dacă este scrisă greșit, câmpul devine roșu.
  - `Aa` = ignoră majusculele. `▲▼` = prioritate: dacă două reguli se potrivesc, câștigă cea de sus.
- **Restaurează** revine la regulile implicite.

## 10. Preferințe (`⚙` sau `Ctrl+,`)

Modificările se salvează singure. **🌐 Limba** (Español, English, Română) se alege în partea de sus a acestei ferestre.

- **Terminal:** 13 teme, font și dimensiune, spațiere, grosime, cursor, culori proprii,
  istoric pe ecran, comportamentul clicului dreapta, avertisment la lipire, keepalive, reconectare automată și **întreabă înainte de a închide NetTerm**
  (implicit, dacă există sesiuni deschise; ca să nu se închidă din greșeală). Dacă sesiunea deschisă are temă
  proprie, alegi dacă tema se aplică la „Toate sesiunile" sau „Doar această sesiune".
- **Aspect:** butoane sus, jos, stânga sau dreapta; stil și dimensiune; panoul de sesiuni în stânga,
  în dreapta sau ascuns; listă, compactă sau carduri.
- **Jurnale:** activează sau dezactivează și alege dosarul.
- **Evidențiere:** vezi secțiunea 9.
- **Taste:** editorul de taste (secțiunea 6).
- **Actualizări:** caută actualizări la deschidere și „Caută actualizări acum".

### Istoric pe ecran

Câte linii poți derula înapoi cu rotița mouse-ului: de la 1.000 la 1.000.000. Fiecare linie ocupă memorie
(cu 1.000.000 de linii, până la ~1,5 GB **pe filă**). Pentru a păstra **totul fără limită**, folosește jurnalele.

## 11. Jurnalele sesiunilor

Cu jurnalele activate (implicit), fiecare conexiune se salvează într-un fișier text, cu **data și ora pe
fiecare linie**, de exemplu `raspi_2026-10-23_18-30-00.log`.

- Dosar implicit: `Documents\NetTerm Logs` (îl schimbi în Preferințe → Jurnale).
- Deschide jurnalul unei sesiuni: clic dreapta pe fila ei → **Deschide jurnalul**.

## 12. Import și export

Butonul `⋯` de lângă „Sesiune nouă".

### Importă sesiuni din alte programe

- **PuTTY** și **SecureCRT:** citește sesiunile salvate pe acest PC (dosarele SecureCRT devin grupuri).
  Aceste programe nu permit citirea parolelor: NetTerm le va cere la conectare.
- **Excel sau CSV:** un fișier cu un rând de antet. Coloane recunoscute: **Nume, Host (sau IP),
  Port, Protocol, Utilizator, Parolă, Grup**. Doar hostul este obligatoriu. „Descarcă șablonul Excel/CSV"
  îți oferă un exemplu.

Vei vedea o listă pentru a alege ce să imporți. Cele pe care le ai deja apar cu „există deja" și nu se dublează.

### Partajează configurația cu echipa

- **Exportă configurația:** creează un fișier `.netterm` cu sesiuni, butoane și/sau preferințe.
  Parolele **nu se includ** sau merg **criptate cu o parolă** aleasă de tine.
- **Importă configurația:** deschide un fișier `.netterm`. Dacă are parole criptate, scrie parola fișierului.
  Ce ai deja nu se dublează. Preferințele importate le înlocuiesc pe ale tale (doar dacă bifezi).

## 13. Actualizări

La deschidere, NetTerm verifică dacă există o versiune nouă. Dacă există, vei vedea noutățile și poți alege:

- **Actualizează acum:** se descarcă, se închide, se înlocuiește și se redeschide. Datele tale se păstrează.
- **Mai târziu** sau **Omite această versiune**.

Nu se instalează niciodată nimic fără acordul tău.

## 14. Scurtături de la tastatură

| Scurtătură | Acțiune |
|---|---|
| `Ctrl+Shift+N` | Sesiune nouă |
| `Ctrl+Shift+W` | Închide fila |
| `Ctrl+Tab` / `Ctrl+Shift+Tab` | Fila următoare / anterioară |
| `Ctrl+B` | Afișează sau ascunde panoul de sesiuni |
| `Ctrl+,` | Preferințe |
| `F1` | Acest manual |
| `Ctrl+Shift+F` | Caută și filtrează în terminal |
| `Ctrl+Shift+1` … `4` | Ecran împărțit |
| `Ctrl+Shift+M` | Trimitere multiplă |
| `Ctrl+Shift+C` / `Ctrl+Shift+V` | Copiază / lipește |
| Cele pe care le atribui | Butoanele tale și editorul de taste |

## 15. Datele tale și securitatea

- Sesiunile, parolele și butoanele se salvează **criptat** în `%USERPROFILE%\.netterm`, protejate cu
  utilizatorul tău de Windows: alt cont sau alt PC nu le poate citi.
- Preferințele sunt în `%USERPROFILE%\.netterm\settings.json`.
- NetTerm nu trimite datele tale către niciun server. Se conectează doar la echipamentele tale și, pentru
  a căuta actualizări, la GitHub.

## 16. Probleme frecvente

| Problemă | Soluție |
|---|---|
| „Windows a protejat computerul" | Mai multe informații → Executare oricum |
| „Utilizator sau parolă incorecte" | Scrie parola în terminal și salveaz-o dacă funcționează. Verifică tastatura folosită la crearea parolei pe echipament (`@` față de `2`) |
| „Serverul a închis conexiunea" | Blocare temporară din cauza încercărilor eșuate: așteaptă câteva minute |
| „Conexiune refuzată" | Portul nu este deschis sau serviciul (SSH/Telnet) nu este activ pe echipament |
| „Timp de așteptare expirat" | Echipamentul nu răspunde: verifică IP-ul, VPN-ul sau firewall-ul |
| Nu văd panoul de sesiuni | Apasă `☰` sau `Ctrl+B` |
| Cuvintele nu se colorează | Preferințe → Evidențiere: verifică dacă este activată. Afectează doar ce sosește după aceea |
| Un buton nu face nimic | Sesiunea trebuie să fie conectată (punct verde). Parolele se trimit doar către SSH/Telnet |
| Echipamentul taie comenzile cu `...` sau descolocă liniile | Începând cu versiunea 1.4, NetTerm comunică echipamentului lățimea reală a ferestrei (SSH și Telnet). Dacă se întâmplă cu o versiune mai veche, actualizează |
