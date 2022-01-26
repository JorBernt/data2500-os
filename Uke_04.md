# Uke 4

### **(Oblig) 1. Last ned filen latch2.dwm Hva slags logisk krets er dette(dvs. hva kan denne kretsen brukes til)? Hvilken funksjon har de to input'ene A og B? Forklar og test at forklaringen er riktig ved å velge de fire mulige kombinasjonene av input. (Noen ganger får man en "race condition" i simulatoren. Det er tilfeller hvor det har betydning hviklet signal som kommer først frem og dette bør generelt unngås. Men se bort fra dette i denne oppgaven)**

Det er en D-lås (data) krets. Verdien som kommer inn gjennom A kan lagres. Den lagres ved å skru på og av B.

---

<br>
<br>

### **(Oblig) 2. Last ned filen 4bitALUtest.dwm åpne den og bruk den til å teste ALU'en som er den samme som brukes i maksinen i senere oppgaver. Gå til Uke 10 i menyen til venstre på siden datamaskinarkitektur og se på den nederste tabellen. Den viser hva input må være for å kunne få ALU'en til å utføre bestemte operasjoner. Bruk denne informasjonen til å få ALU'en til å gjøre regnestykket 3 + 4 = 7 og til å øke verdien av A med en.**

<p align="center">
    <img src="images\4bitalu.png" style="width: auto;" alt="">
    <img src="images\4bitalu_a++.png" style="width: auto;" alt="">
</p>

---

<br>
<br>

### **(Oblig) 3. Last ned filen 4bit.dwm som inneholder et 4-bits register. Ta utgangspunkt i ALU-test filen over og delete de fire output-LED-lysene. Koble istedet output til et register ved å legge inn makroen 4bit.dwm du nettop lastet ned ved å bruke "embed macro" knappen fra menyen. Hva må de relevante input-bit'ene være satt til for å utføre 2+2=4 og lagre resultatet i registeret? Hvilken funksjon har klokken når denne operasjonen utføres?**

<p align="center">
    <img src="images\4bitalu_4bitreg.png" style="width: auto;" alt="">
</p>
<br>
Klokken sin funksjon er å synkronisere D-låsene i 4bit registeret. 

---

<br>
<br>

### **(Oblig) 4. Last ned filen machine.dwm som er en simulering av en 4-bits datamaskin og åpne den i Digital Works. Høyreklikk på boksene som utgjør denne maskinen, velg "Edit Macro" og prøv å lokalisere ALU. Hva er ALU og hva er dens funksjon?**

<p align="center">
    <img src="images\alu_in_machine.png" style="width: auto;" alt="">
</p>


ALU ligger inne i "Data path"-boksen. ALU står "Arithmetic Logic Unit", en enhet som kan gjøre følgende:

* Adder
* Subtraher
* Inkrement (++)
* Dekrement ($- -$)
* Multipliser
* Divider
* Shift (flytt alle bit i en retning)
* Sammenligne
* AND, OR, NOT, XOR

Den har forskjellige kontroll-bits som kan forandre hvilken operasjon som utføres.

---

<br>
<br>

### **(Oblig) 5. Maskinen som simuleres er en liten CPU som kan kjøre programmer som ligger i boksen merket ROM. Høyreklikk på boksen og velg "Edit Memory Contents". Dette er maskininstruksjonene i programmet fra forelesningen som er en liten for-løkke. Kjør programmet ved å klikke deg igjennom med Step-knappen eller ved å trykke på play. Følg med i ROM og se hvordan instruksjonene blir utført en for en. Hva blir resultatet av beregningen og hvor ligger dette resultatet når beregningen er ferdig?**

Resultatet lagres i R2, og er 3.

----

<br>
<br>


### **(Oblig) 6. I forelesningsnotatene står det at i den simulerte datamaskinen er det "gjort visse endringer i forhold til von Neumann arkitekturen". Les forelesningsnotater eller let på nettet og finn ut hva som er den viktigste forskjellen på von Neuman arkitekturen og Harvard arkitekturen. Hvilken arkitektur ligner den simulerte datamaskinen mest på?**





---
<br>
<br>

### **(Oblig) 7. Ta utgangspunkt i DigitalWorks simuleringen av en datamaskin fra forelsningen og endre maskinkoden i ROM slik at løkken gjennomløpes bare to ganger og hvor S økes med to og ikke i, det vil si utfører maskinkode som er den kompilerte versjonen av følgende høynivåkode:**

```

S = 0;
for(i=1;i < 3;i++)
{
   S = S + 2;
}
```

**(NB! Når du har endret på bit'ene i en maskininstruksjon i ROM, pass på å flytte deg med piltastene ned til neste instruksjon, ellers vil ikke endringen lagres.) Hva blir da resultatet og hvor er det lagret etter kjøringen? Hva er sluttverdien til de fire registerne R0, R1, R2 og R3 etter kjøringen?**
<br>
<br>

| Address | Instruksjon | Beskrivelse                                    |
|---------|-------------|------------------------------------------------|
| $0000   | 00100011    | Maks verdi for for-løkken (3), lagres i reg 0  |
| $0001   | 00100101    | Verdien i skal økes med (1), lagres i reg 1    |
| $0002   | 00101001    | i lagres i reg 2 med verdi 1                   |
| $0003   | 00101100    | variabel S lagres i reg 3, og settes til 0     |
| $0004   | 01001001    | Adderer reg 1 til reg 2 (øker i med 1)         |
| $0005   | 01001101    | Adderer reg 1 til reg 3 (øker S med 1)         |
| $0006   | 01001101    | Adderer reg 1 til reg 3 (øker S med 1)         |
| $0007   | 11001000    | Sjekker(cmp) om reg 0 == reg 2 (i == 3)        |
| $0008   | 11110100    | JNE (Jump not equal) om i < 3, hopp til steg 4 |

<p align="center">
    <img src="images\oppgave_04_07.png" style="width: auto;" alt="">
</p>

Sluttresultatet lagres i R3, og er 4. 
Verdiene for registerene er:

```
R0: 0011
R1: 0001
R3: 0011
R4: 0100
```
---

<br>
<br>

## **11. Skriv maskinkode som genererer Fibonacci-rekken 1, 1, 2, 3, 5, 8, 13, der tallene vises fortløpende i to registere, for eksempel R0 og R1. Hvorfor må rekken stoppe her?**

<p align="center">
    <img src="images\fibonacci.png" style="width: auto;" alt="">
</p>

Den må sluttes av der, fordi 13 + 8 > 15, som er maks verdi vi kan lagre i 4 bit.

---

<br>
<br>

## **(Oblig) 12. Logg inn som du tidligere har gjort til s-serveren hvor du har en s-bruker og hvor passordet ligger i s-gruppene i Canvas. Men bruk intel2 istedet for intel3 som du har brukt tidligere:**

```
$ ssh -p 635 s135@intel2.vlab.cs.oslomet.no
```
  
**Som før er portnummeret s-nummeret + 500, 635 er kun for s135. Da kommer du inn på en helt nylaget server, du har fortsatt tilgang til s-serveren på intel3 med alt du har laget der. Her er det en mengde mapper med forskjellige navn, 10 mapper som hver har 10 undermapper som igjen hver har 10 undermapper, altså totalt tusen mapper. Mappesystemet er forskjellig for hver eneste student, så det hjelper ikke å se på naboen sine mapper. Nede i en av disse mappene ligger det en fil som heter file.txt og ukens praktiske oppgave er å finne denne filen og det ordet på 10 tegn som filen inneholder. Finn dette ordet og skriv det inn i rapporten, ett ord for hvert medlem i gruppen. Skriv inn ordene sammen med s-nummeret det tilhører.**

```bash
find /home -name '*.txt'
```

Supercommand :D (hopper inn i mappen) :

```bash
cd "$(find -name '*.txt' -type f -printf '%h\n' -quit)"
```

* s354410 - h9jOTAgq7A
* s354378 - Q7IGly8a70

---

<br>
<br>

## **13. (Oblig) Gi en Linux-kommando som gir deg brukernavnet ditt.**

```bash
whoami
```

---

<br>
<br>

## **14. Gi en Linux-kommando som viser host-navnet på maskinen du sitter på.**
```bash
hostname
```

---

<br>
<br>

## **15. Gi en Linux-kommando som finner ut hvilket operativsystem maskinen din kjører og hvilken versjon det er.**

```bash
lsb_release -a
eller
uname -a (??)
```

---

<br>
<br>

## **16. Finn ut hvilke grupper du selv tilhører på din private s-server (med intel3-innlogging).**
```bash
groups <username>
Tilhører <username> og sudo
```
---

<br>
<br>

## **17. Bruk grep på data2500 til å finne alle grupper brukeren haugerud er med i.**
```
cat /etc/group | grep haugerud
- sudo
```

---

<br>
<br>

## **18. (Oblig)  Hva skjer med eierskapet om man kopierer en annens fil? Prøv ved å kopiere en fil fra en annen bruker, for eksempel /home/haugerud/haugerud.txt på serveren data2500.**

Den kopierte filen kommer under eierskap av brukeren som kopierte. Dette vil jeg tro skjer fordi vi har leserettighet, og derfor kan lese filen og skriver det i en egen ny fil.

---

<br>
<br>

## **19. Gir skriverettighet leserettighet? Har man automatisk leserettigheter hvis man har skriverettighet? Prøv!**

Nei, det gir ikke leserettigheter.

---

<br>
<br>


## **20. Kan man slette en fil man selv eier, men ikke har skriverettigheter til?**

Ja, men man får et spørsmål om man vil slette en skrivebeskyttet fil.

---

<br>
<br>

## **21. (Oblig) På din private s-server (med intel3-innlogging), utfør en Linux-kommando som bruker grep til å skrive ut den linjen i /etc/passwd som inneholder ditt brukernavn, uten å bruke ditt brukernavn eksplisitt.**

```bash
cat /usr/passwd | grep $USER
```
---

<br>
<br>


## **22. (Oblig) Tast inn inn ved shell-promptet de to linjene:**

```bash
minvar=hei
export DINVAR=HALLO
start et nytt bash-shell med
bash
og taster deretter inn i dette shellet
$ echo $minvar 
$ echo $DINVAR
```
<br>
<br>

minvar=hei lagrer hei i en variabel i shellet man er i, men når man åpner opp ett nytt, er det kun variabelen som ble eksportert som er tilgjengelig.
Output blir :

```bash
s194@os694:~$ echo $minvar

s194@os694:~$ echo $DINVAR
HALLO
```

---

<br>
<br>


## **23. (Oblig) Lag et script vari.sh:**

```bash
#! /bin/bash 
min=hei
export DIN=HALLO
som du kjører med
$ ./vari.sh 
og taster deretter
$ echo $min 
$ echo $DIN
```
<br>
<br>

Output blir :

```bash
s194@os694:~$ echo $min

s194@os694:~$ echo $DIN

```

Dette var ikke som forventet, vi forventet samme output som forrige oppgave.
Dette fungerer ikke på samme måte, fordi et bash-script kjøres i et eget subshell.
Om man skriver
```bash
s194@os694:~$ source <script>.sh
eller
s194@os694:~$ . <script>.sh
```
vil det fungere. Da kjøres scriptet i samme shell.

---

<br>
<br>

## **24. Start en editor på data2500. Anta at editoren henger av en eller annen grunn. Logg inn på data2500 i et annet vindu og drep editor-prosessen med kommandoen kill. Hint: Du må finne editorens PID med ps.**

Jeg fant prosessen med ps aux fra en annen terminal, og drepte den med kill. <PID> <br>
Da avsluttet editoren i det andre vinduet med en gang med følgende melding:

```bash
***Fatal Error: Killed by signal 15.

jed version: 0.99.19/Unix
 Compiled with GNU C 9.2
S-Lang version: 2.3.2

jed compile-time options:
 +LINE_ATTRIBUTES +BUFFER_LOCAL_VARS +SAVE_NARROW +TTY_MENUS
 +EMACS_LOCKING +MULTICLICK +SUBPROCESSES +DFA_SYNTAX +ABBREVS
 +COLOR_COLUMNS +LINE_MARKS +GPM_MOUSE +IMPORT
CBuf: 0x557f76e645b0, CLine: 0x557f76e162e0, Point 11
CLine: data: 0x557f76e64580, len = 11, next: (nil), prev (nil)
Max_LineNum: 1, LineNum: 1
JWindow: 0x557f76e5dbc0, top: 1, rows: 27, buffer: 0x557f76e645b0

```

---

<br>
<br>

## **25.Bruk uname slik at navnet på OS'et som kjøres legges i variabelen $OS (etterpå skal echo $OS gi Linux).**

```bash
s194@os694:~$ export OS="$(uname)"
s194@os694:~$ echo $OS
Linux
```
---

<br>
<br>

## **26.Legg til katalogen ~/bin i \$PATH. Legg endringen til i ~/.bashrc for at den skal være varig. Legger du senere scriptene du lager i ~/bin kan de da kjøres fra hvilken som helst katalog. Legg et script i ~/bin og sjekk at det kan kjøres fra hvorsomhelst. Sjekk om "." (katalogen du står i) er med i \$PATH. Hvis ikke må du skrive \$ ./mittscript for å få kjørt et script som heter mittscript. Legg i såfall til "." i PATH og lagre endringen i ~/.bashrc. Da kan du etterpå kjøre scriptet med $ mittscript.**

```bash
PATH=$PATH:~/bin
```
---

<br>
<br>

## **29.(Oblig) Hvis du leter etter filer med navn passwd på data2500 med følgende kommando**
```bash
data2500:~$ find /  -name "passwd"
```
## **får du en masse linjer med "Permission denied". Lag en kommando som gjør at bare linjer hvor "passwd" blir funnet vises.**

```bash
find / -name "passwd" 2>/dev/null
```
---

<br>
<br>

## **30. Ukens utfordring nr. 1: Lag et script err.sh som skriver strengen "hallo" til stdout og strengen "Error!" til stdout. Kjør deretter scriptet slik at "hallo" skrives ut mens "Error!" omdirigeres til filen err.txt.**

```bash
#! /bin/bash

echo "hallo"
echo "Error!" >err.txt
```
---

<br>
<br>

## **31.Lag en kommando på data2500 som teller antall ganger navnet haugerud forekommer i filen /etc/group og legger tallet i filen hgroup.txt.**

```bash
grep -c haugerud /etc/group>haugerud.txt
```

---
<br>
<br>

## **32.Splitt opp følgende eksempel, utfør ledd for ledd (først ps aux, så awk '{print $1}', så ps -eo user | sort, etc.) og forklar hva hver kommando gjør:**

```bash
ps aux | awk '{print $1}' | sort | uniq | wc -l**
```

## **(Forøvrig er ps -eo user et alternativ til ps aux | awk '{print $1}' ) Kommandoen skal gi antall brukere som kjører prosesser på maskinen, men gir en for mye fordi det står en linje med USER øverst i ps aux listingen. Prøv å fjerne linjen som inneholder USER med grep, les manualsiden for grep.**

```bash
ps aux
```
Lister opp alle prosesser
```bash
awk '{print $1}'
```
Viser kun rad 1 (alle brukere)
```bash
sort
```
Sorterer brukerene
```bash
uniq
```
Fjerner alle repeterende brukernavn
```bash
wc -l
```
Teller antall linjer, AKA alle unike brukere som har prosesser kjørende.

Om en skal bruke 
```bash
ps -eo user
```
kan en gjøre slik:
```bash
ps -ei user | grep -v USER
```
for å fjerne den øverte USER kolonnenavnet. (-v er NOT MATCHING i grep)

---
<br>
<br>

## **33. Ukens utfordring nr. 2: Lag en kommando som teller opp hvor mange ganger strengen "haugerud" finnes tilsammen i filene /etc/passwd og /etc/group på data2500.**

```bash
grep -c 'haugerud' /etc/passwd /etc/group | awk -F: '{s+=$2} END {print s}'
```
0 forekomster i passwd, 1 i group.
---
<br>
<br>


## **34.(Oblig) Lag et script usrbin.bash:**
```bash
#! /bin/bash 
cd /usr/bin 
echo "er i $(pwd)"
som du kjører med
$ ./usrbin.bash 
```
## **Hvor i filtreet er du etter at scriptet har kjørt? Forklar. Prøv å kjøre scriptet på en slik måte at du befinner deg i /usr/bin etter at det har kjørt.**

Vi er på samme sted. For å kunne havne /usr/bin må vi kjøre scriptet i samme shell, enten ved bruk av 'source' eller '.' slik:

```bash
. usrbin.bash
```

---

<br>
<br>

## **35. Lag script for å appende fra meminfo til fil**

```bash
#! /bin/bash

cat /proc/meminfo | grep $1 >>$1.dat
```
---

<br>
<br>

## **36.Ukens utfordring nr. 3:  I en tom katalog med navn ~/tmp utføres følgende Linux-kommandoer:**
```bash
$ mkdir dir1
$ mkdir dir2
$ mkdir dir3
$ for nr in * ;do touch $nr/fil$nr;done
$ mv dir1 dir2
$ mv dir3 dir2
```

## **Bruk kommandoen tree eller tegn en liten skisse som viser katalogstrukturen under ~/tmp med navn på alle kataloger og filer etter at disse kommandoene er utført.**

```bash
s354410@data2500:~/tmp2$ tree
.
└── dir2
    ├── dir1
    │   └── fildir1
    ├── dir3
    │   └── fildir3
    └── fildir2

3 directories, 3 files
```

---

<br>
<br>

## **37.Ukens utfordring nr. 4: Anta at du er i en katalog med en mengde filer med filendelse .HTM. Lag et script som endrer fil-endelse på alle disse filene til .html. Bruk basename fra oppgaven over til å løse dette problemet. Kommandoen $ basename dir/fil.txt gir fil.txt til resultatet. For å legge resultatet av en kommando inn i en variabel, bruker man apostrofer. Etter**
```bash
name=`basename dir/fil.txt`
```

## **har variabelen $name verdien fil.txt. Legg merke til at det er forskjell på apostrofene ' og `. Den siste som heller bakover brukes i det siste eksempelet. Alternativt kan man bruke følgende metode:**
```bash
name=$(basename dir/fil.txt)
```

Rename script:
```bash
#! /bin/bash

for fil in *.htm
do
        name="$(basename $fil .htm)"
        mv $fil $name.html
done
```