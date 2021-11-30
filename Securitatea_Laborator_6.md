# Lucrarea de laborator Nr.6 la Securitatea SI

Tema: **Detectarea şi prevenirea intruziunilor în sistemele informatice. Sisteme anti-malware şi de jurnalizare.**

A elaborat: **Curmanschii Anton, IA1901**


- [Lucrarea de laborator Nr.6 la Securitatea SI](#lucrarea-de-laborator-nr6-la-securitatea-si)
  - [Scopurile lucrării](#scopurile-lucrării)
  - [Principiul funcționării sistemelor de detectare sau de prevenire a intruziunilor](#principiul-funcționării-sistemelor-de-detectare-sau-de-prevenire-a-intruziunilor)
  - [Suricata](#suricata)
    - [Regulile](#regulile)
    - [Opțiunile meta](#opțiunile-meta)
    - [Alte opțiuni](#alte-opțiuni)
    - [Aplicarea regulilor](#aplicarea-regulilor)
    - [Privirea mea la limbajul regulilor](#privirea-mea-la-limbajul-regulilor)
    - [Performanța](#performanța)
  - [Comparația între Snort și Suricata](#comparația-între-snort-și-suricata)
  - [Concluziile](#concluziile)



## Scopurile lucrării

1. Studierea caracteristicilor și a principiului de funcționare a sistemelor de detectare și de prevenire a intruziunilor. Analiza  arametrilor de funcționare a lor (IDS/IPS). 

2. Descrierea comparativă (după principiile de mai jos) a sistemelor de detectare sau de prevenire a intruziunilor IDS/IPS (unele din lista propusă, sau altele care nu sunt incluse în listă). 

3. Studierea funcționalității unor sisteme de detectare / prevenire a intruziunilor (2-3 sisteme din lista propusă). Verificarea și precizarea compatibilității cu anumite sisteme de operare (Windows, Linux, iOS), dacă pot fi gestionate de pe telefon sau tabletă. 
   
4. Descrierea principiului de funcționare a sistemelor de detectare / prevenire a intruziunilor. 
   
5. Stabilirea unei clasificări după gradul de popularitate în utilizare și eficacitate în funcționare.


**Principiile comparative:**

- Soft gratuit / licenţiat / termeni de utilizare etc., 
- Varietatea sistemelor de operare cu care sunt compatibile, 
- Descrierea serviciilor pe care le oferă/ principiul de funcționare, 
- Avantaje / dezavantaje, 
- Interfaţa de lucru / lucru prin comenzi / comoditate și simplitate, 
- Gradul de siguranţă / riscul de a genera mesaje/ alarme false, 
- Gradul de popularitate (ce categorii de persoane le utilizează), 
- Alte aspecte prin care se deosebesc, etc.


## Principiul funcționării sistemelor de detectare sau de prevenire a intruziunilor

După cunoașterea mea, IDS/IPS funcționează prin inspectarea pachetelor rețelei.

Ele interceptează pachetele care intră (sau iese) în (din) sistem, le inspectează, încercând să potrivească unele paterne prestabilite, după ce decid dacă pachetul dat este suspicios și trebuie să fie eliminat, sau dacă trecerea se permite.
Dacă un pachet este suspicios, el este eliminat și crează o alarmă, de exemplu, transmitând administratorului un mesaj, iar pachetele normale nu sunt afectate.

Sistemele ca Suricata, Snort folosească *Nmap Project's packet capture* (ncap) pe Windows, deci este imediat clar că ele funcționează în modul descris mai sus.

## Suricata

Suricata este un sistem IDS și IPS cu performanța ridicată, dezvoltat de Open Information Security Foundation (OISF).
Este cu sursa deschisă și este licențiată după GNU GPL-2.

### Regulile

[Documentarea Suricata, pagina despre reguli](https://suricata.readthedocs.io/en/suricata-6.0.4/rules/intro.html)

Regulile, sau semnaturile, sunt instumentul principal de configurare a sistemului Suricata. 
Regulile pot fi descărcate și utilizate direct, sau scrise manual.

O semnatură conține următoarele:

- **Acțiunea** care va fi aplicată în urma potrivirii semnaturii;
- **Antetul** care definește protocolul, adresele IP, porturile și direcțiile, după care regula va fi aplicată;
- **Opțiunile** care definesc detalii mai specifice.

**Acțiunea** este una din următoarele:

- `alert` - generează o alarmă.
- `pass` - permite propagarea a pachetului.
- `drop` - pică (șterge) pachetul și generează o alarmă.
- `reject` sau `rejectsrc` - transmite expeditorului eroarea că rețea a fost inaccesibilă, definit după protocolul [ICMP](https://www.wikiwand.com/en/Internet_Control_Message_Protocol).
- `rejectdst` - transmite un pachet de eroare a destinătarului.
- `rejectboth` - transmite un pachet de eroare a destinătarului și a expeditorului.

**Protocolul** se specifică ca prima parte a antetului și poate fi unul din multiple protocoale răspândite în rețea, de exemplu  `tcp`, `udp`, `http`, `ftp`, `smtp`. Se permite și wildcard-ul `ip` (orice protocol).

Pentru partea de **sursă și destinație** se poate folosi ori adresele IP specifice, ori variabile setate aparte pentru fiecare configurare după proprietățile sistemului. 
**Porturile** urmează sursa și destinația. Se poate folosi wildcard-ul `any` care semnifică orice port.

**Direcția** poate fi ori `->` (înainte) ori `<>` (în ambele direcții).

De exemplu următoarea semnătură, dacă am înțeles corect, va pica orice pachet HTTP de la calculatorul curent la calculatorul cu IP adresa 10.0.0.5, orice port:

```
drop http $HOME_NET any -> 10.0.0.5 any
```

### Opțiunile meta

Opțiunea `msg` specifică informația contextuală a semnăturii, și va fi inclus în notificare trimisă administratorului în caz de alarmă. Exemplul din documentare se va declanșa la fiecare pachet transmis cu ajutorul protocolului TCP (în documentare sunt mai multe opțiuni care limită conținutul mesajul care ar declanșa alarma).

```
drop tcp $HOME_NET any -> $EXTERNAL_NET any (msg:"ET TROJAN Likely Bot Nick in IRC (USA +..)"; mai_multe_opțiuni)
```

Opțiunea `sid` asociază un identificator unic fiecărei regule.

```
sid: 123
```

Opțiunea `rev` asociază numărul reviziei fiecărei regule.

```
rev: 2
```

Prin opțiunea `classtype` putem atribui semnaturile la tipuri de alarme personalizat definite, și putem să le dăm prioritate la fiecare. 
```
# Configurarea claselor.
config classification: web-application-attack,Web Application Attack,1
config classification: not-suspicious,Not Suspicious Traffic,3

# Utilizarea clasului web-application-attack în semnătură.
classtype:web-application-attack
```

Putem folosi opțiunea `reference` pentru a lega o pagină web la o semnătură. În exemplul de mai jos, tipul referinței este URL, iar info.com este linkul la informație.
```
reference: url, info.com
```

### Alte opțiuni

Alte opțiuni sunt specifice la protocoale concrete.
De exemplu, protocolul IP definește opțiunile pentru câmpurile diferite ale antetelor, ca `ttl` (tile-to-live, câte hop-uri rămân), `ipopts` care verifică unele opțiuni specifice, `ip_proto` care permite accesul la protocolul definit în cadrul pachetului, etc.
La protocolul TCP, de exemplu, sunt opțiunile `seq` - numărul secvențial al pachetului, câmpul `ack`, etc.


### Aplicarea regulilor

Regulile default vor fi sălvate în fișierul `/var/lib/suricata/rules/suricata.rules`.

Regulile pot fi configurate să fie incluse sau discluse prin modificarea fișierilor `/etc/suricata/enable.conf` și `/etc/suricata/disable.conf`.

```
2019401                   # sid
group:emerging-icmp.rules # un rulefile specific
re:trojan                 # o expresie regulară
```

Fișierul cu configurare este în `/etc/suricata/suricata.yaml` și poate fi modificat pentru a include reguli personalizate.
Un exemplu conținut:

```
default-rule-path: /usr/local/etc/suricata/rules

rule-files:
  - suricata.rules
  - /path/to/local.rules
```

### Privirea mea la limbajul regulilor

Este clar, chiar fără experiența de utilizare a regulilor Suricata, că limbajul regulilor nu este comod și regulile nu sunt susținabile:

- Sintaxa este urâtă;
- Regulile trebuie să fie scrise într-o singură linie, sau caracterele line feed trebuie să fie evadate;
- Includerea regulilor anevoioasă (nu poate fi inclusă o mapă de reguli);
- Nu putem defini variabile, face operații aritmetice, etc.

Suricata permite și utilizarea limbajului Lua pentru definirea regulilor.
Această variantă este mai bună, dar totuși nu-mi place Lua, deoarece nu are tipuri și este foarte anevoiosă pentru programarea unui sistem ne-super-trivial.

Eu aș implica un limbaj de programare real, cu un sistem sofisticat de tipuri, care permite sintaxa declarativă și este comod de utilizat. Deci ori limbajul D, ori un limbaj funcțional.
Un limbaj real ar permite o analiză mai profundă a pachetelor, implicarea algoritmilor mai eficienți, etc.


### Performanța

Suricata rulează pe mai multe thread-uri (worker-uri), procesând mai multe pachete deodată.
Acest număr de thread-uri poate fi setat la configurare.


## Comparația între Snort și Suricata

Mă orientez după [acest blog](https://resources.infosecinstitute.com/topic/open-source-ids-snort-suricata/).

| Categorie | Suricata | Snort |
| --------- | -------- | ----- |
| Activ? | Da, foarte ([Github](https://github.com/OISF/suricata/pulse/monthly)) | Da, dar mai puțin ([Github](https://github.com/james-martinez/snort3/pulse/monthly)) |
| Gratuit și Open Source? | Da | Da |
| Sistemele de operare? | Windows, Linux, MacOS | Oficial, [orice *nix sistem](https://www.snort.org/documents/snort-supported-oses). Windows pare că nu a fost testat atât de mult (însă am găsit bin-uri precompilate) |
| GUI? | CLI, GUI neoficiale Web | CLI, GUI neoficiale Web |
| Multithreading? | Da | Parțial |
| Suportul comunității? Plugin-uri? | Da | Da |


Punctele comune:

- Utilizează același format de reguli;
- Lua scripting;
- Același principiu de funcționare.


În general, după cum înțeleg, Suricata are mai multe capacități, de exemplu [file extraction](https://redmine.openinfosecfoundation.org/projects/suricata/wiki/File_Extraction). 
Snort3 este un release anticipat care aduce multe capacități utile, ca sistemul de plugin-uri inclus, multithreading, configurarea simplificată etc. Însă încă este în preview.


## Concluziile

Suricata este un sistem de detectare și prevenire a intruziunilor mai modern, dezvoltat activ în timpul recent.
Snort este un sistem mai vechi, dar versiunea nouă este așteptată să fie la același nivel cu Suricata.
Însă, ambele sisteme sunt ușor de instalat și de încercat, și în general acel sistem care se dovedește mai performant și mai ușor de configurat va fi ales. 
Adică, dacă aplicația deja primește trafic dens, și aceste caracteristici pot fi ușor verificate.

După opinia mea, însă, nu are mult sens să vorbesc despre aceste sisteme pe un nivel mai adânc, deoarece n-am acest trafic și nu le pot testa cum-se-cade.
În lucrarea această de fapt am prezentat o descriere după documentare, dar nu după experiență și teste, și am comparat cele două sisteme superficial.