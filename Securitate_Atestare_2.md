# Atestarea nr.2 la Securitatea SI

A elaborat: **Curmanschii Anton, IA1901**

**1. Formulaţi Regulile generale privind evidenţa, păstrarea, procesarea, multiplica-rea, manipularea, transmiterea şi distrugerea informaţiilor clasificate.**

Datele clasificate trebuie să fie protejate, fiind accesibile numai de către persone autorizate, iar numărul de persoane autoritative trebuie să fie cât mai mic.
Dacă un adversar obține acces la aceste date, le pot șterge.
Dacă mai multe persoane au acces la aceste date, crește posibilitatea că unul dintre ele le va împărți accidental (data leak).

Datele clasificate necesită un backup regular pentru a previne distrugerea lor accidentală.
Backup-ul poate fi realizat pe mai multe medii ca Tape pentru backup, simplu un Hard Disk Drive, RAID, etc.
Există mai multe abordări la backup, fiecare abordare permite compromisuri între costul (hardware), timpul (frecvența) și siguranța.

Dacă datele sunt secrete, acestea pot fi recuperate după ștergerea.
Această posibilitate trebuie să fie considerată și eliminată aparte.
Principiul se aplică și la fișiere cu date, și la buferi pentru parole în programare.
De exemplu, bibliotecile care furnizează servicii cripto, șterg informația din buferi cu parole după ce au utilizat-o.

Trebuie să se acorde atenție când ștergeți sau mutați fișierile, deoarece un `rm -rf *` pe Linux poate dauna sistemul ireversibil.

**2.Descrieţi ce reprezintă PATA şi SATA, la ce se foloseşte şi care este principiul de funcţionare. Prin ce se deosebesc ele?**

Pata = Parallel ATA; SATA = Serial ATA; ATA = AT Attachment; AT = Advanced Technology.

PATA este interfața standartă pentru conexiunea unui calculator la device-uri pentru păstrarea datelor, ca Hard Disk Drive, Drive-uri CD și DVD.

SATA este asemănător un standard pentru același scop, succesorul ui PATA. 
Furnizează accesul la date mai rapid, este mai puțin scump și mai compact.

PATA este învechit.


**3. Explicaţi ce reprezintă şi la ce se utilizează Tape backup care sunt avantajele şi dezavantajele de utilizare.**

Tape Drive este un mediu pentru păstrarea datelor, băzat pe o bandă magnetică liniară. 

Disavantajul este că accesul la date este doar secvențial.

Avantajele sunt costul redus în comparația cu discuri hard pentru același spațiu, rezistența la daune fizice (în comparația cu discuri hard), stabilitatea de funcționare (pot fi utilizate pe o durată lungă, 20+ de ani).
Tape-uri sunt mai rapide pentru accesul secvențial la date, de aceea sunt utile pentru backup-uri.


**4. Formulaţi care sunt principalele elemente de securitate ale SO Windows Longhorn şi Mac OS X. Faceţi o comparaţie.**

Windows Longhorn = Windows Vista.

Windows Vista este acea versiune Windows care a adus capacitățile noi din punct de vedere a securității sistemului.

- *User Account Control*. Aceasta înseamnă că utilizatorului i se cere confirmare când el încearcă o acțiune care necesită drepturi ridicate, chiar dacă este admin. Aceasta previne atacuri din partea aplicațiilor neprevăzute, asigură că utilizatorul știe ce el face, etc.
- *Windows Firewall*. Este de fapt un sistem de prevenire a intruziunilor: filtrează pachetele care vin la calculator pe rețea. Windows Vista a adăugat capacități noi în acest sistem, a sporit nivelul de securitate.
- *Windows Defender*. Este un sistem antimalware, introdus în Windows Vista, care a prevenit viruși și acțiuni malițioase cunoscuți.
- Criptarea datelor.
- Alte facilități de securitate.

Eu nu am studiat sistemul MAC, deci voi interpreta informația de pe internet:
- **FileVault** furnizează criptarea datelor (lucrează ca cu criptarea parolelor, previne furul datelor dacă computer-ul se obține de un adversar).
- Actualizări dese de securitate.
- **System Integrity Protection (SIP)** previne executarea aplicațiilor neautorizate, previne modificarea fișierilor de sistem.
- **Gatekeeper** previne instalarea aplicațiilor neautorizate.
- **XProtect** un program antimalware.
- Alte capacități, multe din care Windows nu are după default (după cum știu).

http://edtechchris.com/2018/04/03/9-macos-security-features/


După experiența mea, Windows previne doar atacuri primitive și rar este util practic. 
Utilizatorii Windows de obicei utilizează softul de terță parte pentru protejarea sistemului.
Nu știu cum sunt lucrurile cu Mac, dar îmi pare că are aplicații mai sigure după default.


**5. Enumeraţi care sunt procedurile sigure de administrare şi întreţinere a servere-lor.**

Am studiat această temă după documentul de la NIST care conține recomandări concrete.

Servere sunt atacate de entități malițioase pentru a obține acces la informații sensitive. 
Scopurile pot fi diferite, de la furul de bani, beneficii proprii, până la vandalism.

Administrarea unui server trebuie să asigure lipsa, sau eliminarea rapidă a vulnerabilităților, în scopul protejării datelor securizate.
Tehniciile sunt următoarele:

- Polițe de securitate standardizate în companie.
- Configurarea și reconfigurarea efectivă, care să respecte polițele stabilite.
- Răspândirea opiniei, sau a ideii că securitatea sistemului este importantă.
- Un plan backup.

Însă, este important de realizat, că aceste lucruri au și costuri asociate cu ele.
Unele serveri nu necesită măsuri de securități ridicate, deoarece nu conțin date clasificate.
Riscul pierderii datelor pentru unele companii poate fi mai puțin decât costul asigurării integrității lor.

Configurarea și reconfigurarea includ:
- Instalarea unui soft sigur.
- Instalarea actualizărilor de securitate.
- Configurarea accesului la date (autorizării utilizatorilor).
- Eliminarea vulnerabilităților.
- Testarea.
- Utilizarea aplicațiilor pentru prevenire a intruziunilor.


**6. Formulaţi care sunt mijloacele de securitate a Bazelor de Date multinivel.**

Stabilirea grupelor de acces. Acces la o resursă particulară se permite numai utilizatorilor autorizați, care fac parte dintr-un anumit grup căruia se permite accesul la această resursă.

Permiterea acțiunilor particulare la un grup de utilizatori.

Validarea autorizării utilizatorului (pe backend, nu doar în aplicația clientului).

Validarea interogărilor SQL (adversarul poate să găsească o vulnerabilitate de injectare a codului SQL pentru a obține unele date nesolicitate, ceea ce poate fi prevenit prin blocare interogărilor suspicioase, cu toate că așa vulnerabilitate este una gravă).

Conceptul de row-level security, care previne accesul la date nerelevante pentru un utilzator dat, adică datele despre care utilizatorul dat în principiu nu trebuie să cunoască.


**7. Explicaţi care sunt avantajele şi dezavantajele Ingineriei inverse din punct de vedere a asigurării securităţii sistemelor informatice.**

Ingeneria inversă înseamnă studierea codului sau a modului de funcționare a unui sistem pentru a-l modifica, a extrage informații referitor la design, a interacționa într-un fel cu el.

Ingeneria inversă are ca atare două cazuri de utilizare.

Primul caz de utilizare este unui beneficător ca de exemplu:
- Studierea modului de funcționare a unei sisteme proprietare pentru interacționarea externă cu ea, ca interacționarea cu softul proprietar.
- Studierea mai bună a produsului fără documentare deschisă pentru a putea crea un produs asemănător de o calitate mai mare (50-50, bun-rău, depinde de intenție).

Al doilea caz este unul malițios:
- Performarea analizei unui sistem informatic, pentru a determina puncte vulnerabile care pot fi exploatate (pot fi raportate, dacă hacker-ul are intenții bune).
- Cracking-ul sistemelor informaice proprietare pentru a le utiliza fără a plăti bani (este rău pentru dezvoltatorii, dar binefăcător pentru copii care nu pot să-și permită a cumpara un joc).


**8. Daţi  o  clasificare  a  sistemelor  SDI  şi  caracterizaţi  fiecare  dintre  tipurile enumerate.  Descrieţi  care  sunt  Metodele  de  Evaziune  a  SDI  aplicate  de atacatori.**


SDI (IDS) = Sistem de detectare a intruziunilor. 
Este un sistem informatic care analizează trafic din rețea, anume pachetele care vin la calculator, pentru a încerca să identifice aceste pachete și să da alarma. Sistemele ca Snot și Suricata lucrează după acest principiu. Ele sunt și sisteme de previziune a intruziunilor, adică pot face acțiuni suplimentare, ca de exemplu blocarea, acestor pachete nedorite. Aceste sisteme care realizează analiza traficului din rețea se numesc NIDS (N = network).

Mai există HIDS (H = host based) care detectează accesul la fișierele importante pentru funcționarea sistemei de operare.

NIDS pot fi clasificate la cele băzate pe semnaturi (reguli prestabilite, după care se decide dacă conținutul pachetului este malițios), și cele băzate pe anomalii, unde de obicei se folosesc Machine Learning, adică rețele NN destinate potrivirii unui pattern.
Cele prime rar recunosc amenințări noi, de obicei doar prevenind amenințări cunoscute, iar cele băzate pe anomalii dau mai multe false-positive, dar pot și a bloca amenințări necunoscute, prin generalizare.
