# Atestarea nr.1 la Securitatea SO

A elaborat: **Curmanschii Anton, IA1901**


**1. Dați definirea spațiului cibernetic din punct de vedere social și economic.**

Spațiul cibernetic este mediul unde are loc comunicarea pe internet, sau, în general, rețelele de comunicare.

Din punct de vedere social, este o platformă de comunicare pentru oameni.

Din punct de vedere economic, deschide posibilități noi pentru business-uri, ca de exemplu online banking, online shopping, valutele cryto.

De aceea prezintă și oportunități noi de împărțirea informației, dar și expune riscuri de securitate.


**2. Descrieţi ce rol are Parlamentului Republicii Moldova în vederea asigurării securităţii informaţionale în RM şi care sunt atribuţiile/realizările recente în privinţa securităţii informaţionale.**

Parlamentul Republicii Moldova asigură securitatea informațională națională, protectând datele naționale secrete, care, dacă ar fi expuse, pot prezenta un risc internațional. 
El asigură ca toate întreprinderile ce din punct de vedere național necesită un nivel de securitate sporit să-l obțină.
Se realizează informarea publică de riscuri legate la securitate.


**3. Daţi noţiunea (explicaţi ce este): Ameninţare cibernetică, Spionaj cibernetic, Cross-site scripting (XSS).**

Ameninţare cibernetică — daune potențiale ce poate aduce un eveniment sau un adversar la securitatea unei sisteme informatice.

Sponaj cibernetic — practicarea unor atacuri cibernetici pentru a obține anumite informații secrete de la adversar, sau pentru a obține control asupra sistemului informatic al lui.

Cross-site scripting — vulnerabilitatea prezentă în unele aplicații, unde adversarul poate executa codul său arbitrar pe server, astfel el poate obține informații secrete de pe server, sau a ia control asupra lui, etc.


**4. Daţi noţiunea de Copyleft. Explicaţi ce reprezintă simbolul CC.**

Copyleft înseamnă licența open source, unde utilizatorul nu este impus careva restricții referitor la ce el poate face cu codul.
Exemplu: MIT license.

Simbolul CC înseamnă Creative Commons license. 
Semnifică că autorul dorește ca codul sau lucrarea lui să fie accesibilă de alte persoane și să fie modificată, utilizată pentru a fi perfectată.
Deci autorul inițial nu dorește să primească profituri, vânzând acest produs.


**5. Explicaţi ce reprezintă soft open source şi ce prevede Protecţia drepturilor de  autor  pentru  soft  open  source.  Daţi  exemple  de  soft  open  source.**

Soft open source înseamnă programele codul cărora este accesibil pe internet de către orice persoană.
Orice persoană poate contribui la acest cod, de exemplu fixând unele bug-uri.

Autorul are dreptate de a asocia o licență la codul său, care să nu admită utilizarea codului dat de către alții (proprietary license), să restricționeze utilizarea codului (de exemplu, se stabilește că codul poate fi reutilizat numai dacă este atribuit autorul inițial, ori doar cu folosirea de aceeași licență), ori să dea voie de a folosi codul în orice mod (de exemplu MIT). 
După default, adică dacă codul nu este asociat nici o licența, ea este considerată să fie proprietară.

GTK, Windows Terminal, Visual Studio Code, Chromium, Vue JS, DMD etc.


**6. Explicaţi ce reprezintă Identificarea şi Autorizarea. Explicaţi ce reprezintă Protocolul Kerberos.**

Identificarea înseamnă că utilizatorul își dă numele (identitatea) la sistem.
Autorizarea semnifică confirmarea identității prin parolă, sau unei alte modalități de autentificare (amprenta digitală, one-time password).

Protocolul Kerberos asigură autenticarea mutuală între server și client, folosind algoritmele criptografice cu cheia publică-privată.
Utilizând protocolul dat, ambele părți își pot confirma identitatea.


**7. Faceţi o analiză comparativă pentru două dintre managerele de parole: KeePass,  1Password,  RoboForm,  eWallet,  LastPass,  Kaspersky  (pe  care le-aţi  utilizat  la  lucrarea  de  laborator).**

Se folosește o parolă master, care criptează o bază de date cu parolele. 
Fără parola master baza de date n-are semnificație, deoarece este criptată. 
Cu parola master, puteți obține toate parole la toate serviciile utilizatorului.

KeePass este cel mai flexibil, dar este și mai complicat de setat pentru un utilizator obișnuit.
Nu are sincronizare pe cloud, totul trebuie să fie setat manual, sau să copiați baza de date pe google drive de exemplu.
Se poate asocia linkuri, conturi și descrieri la parole individuale, se poate grupa parolele.
Ce mai des utilizăm parolele pe Web, însă KeePass nu furnizează o integrare automată pe Web, trebuie să faceți șmecherii individual pentru fiecare site. 
De exemplu, se poate seta o secvență de apăsări a cheilor, care ar fi reluată, când încercați să vă logați pe site-ul dat.
Se poate introduce parolele ca parametrile la request-ul (?name=value în URL), însă totul trebuie să fie făcut manual.
KeePass este open source, rulează pe desktop, și 100% gratuit, are port-uri pe Android și iOS etc. open source.
Are un nivel de securitate mare din punct de vedere standartelor moderne.

LastPass este o soluție web gratuită (versiunea cu capacități limitate, însă de ajuns pentru majoritatea utilizatorilor).
Nu este open source.
Rulează în browser, provizionează o integrație bună cu serviciile web (password autocompletion etc.), doar trebuie să introduceți la start parola master.
Are sincronizarea automată și centralizată.
Este foarte user friendly, complexitatea este minimă, în comparație cu KeePass, deoarece problemele de sincronizare a bazei de date și a integrării în browser sunt rezolvate automat.
Are aplicații pentru Android și iOS.
Are un nivel de securitate egal cu KeePass.


**8. Explicaţi principiul de gestionare a drepturilor de acces la fişiere şi dosare în dependenţă de tipurile de conturi de utilizator (Windows/ Linux - cel utilizat la LLab).**

În primul rând, menționăm, că sistemul NTFS permite asocierea datelor de securitate la fișiere și foldere.
O unitate ce posedă așa valoare de securitate se numește un obiect în Windows.
O identitate ce accesează obiectele se numește un security principal și are un SID (security identifier) asociat.
Windows păstrează datele de securitate la fiecare obiect într-un tabel ACL (access control table) care conține mai multe linii (access control entry, ACE).
Fiecare ACE conține principalul la ce se vor aplica regulile, și un set de reguli, ce restricționează sau garantează accesul la date.
Regulile pot fi *delete, list contents, write, read* și altele.
Un principal nu poate să acceseze obiectul dat dacă nu are drepturile la aceasta.

Principal poate fi un singur utilizator, sau un grup de utilizatori, care conține unul sau mai multe utilizatori, sau un thread, proces sau alte lucruri mai exotice.
Windows predefinește un set de grupuri, ca Everyone, Administrators, Users, etc.

La logare, utilizatorul primește un token, care cașează de ce grupuri el face parte.
Când utilizatorul încearcă să acceseze un obiect, OS-ul verifică acest token pentru a decide dacă utilizatorul poate fi dat acces la acest obiect.

Un cont de tip administrator are acces la toate obiectele și poate schimba regulile la oricare obiect.
Administratorii încă pot schimba la ce grup un alt utilizator specific se aparține, pot crea noi grupuri, atribuindu-le oricare utilizatori.
Astfel pentru administrare accesului la unele obiect în sistem administratorul doar trebuie să mute utilizatorii din și în grupuri, și să restricționeze sau să dea accesul la unele obiecte pentru acele grupuri.

Încă menționez că toate obiectele-fii unui folder moștenesc setările de securitate acelui fișier, ceea ce simplifică lucrul pentru administrator.

**9. Explicaţi ce reprezintă soluţia Two-way authentication.**

Two-way authentication semnifică că ambii serverul și clientul își demonstrează identitatea unul la altul.
Se face prin folosirea criptografiei cu cheia publică. 
Clientul își demonstrează identitatea, transmitând parola criptată cu cheia publică a serverului la server.
Serverul demonstrează că posedă cheia privată, criptând mesajul clientului cu cheia publică a lui, și transmitându-l la client.
Clientul verifică identitatea serverului, decriptând mesajul cu cheia sa privată.