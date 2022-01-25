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

```
find /home -name '*.txt'
```

Supercommand :D (hopper inn i mappen) :

```
cd "$(find -name '*.txt' -type f -printf '%h\n' -quit)"
```

* s354410 - h9jOTAgq7A
* s354378 - Q7IGly8a70

---

<br>
<br>

## **13. (Oblig) Gi en Linux-kommando som gir deg brukernavnet ditt.**

```
whoami
```

---

<br>
<br>

## **14. Gi en Linux-kommando som viser host-navnet på maskinen du sitter på.**
```
hostname
```

---

<br>
<br>

## **15. Gi en Linux-kommando som finner ut hvilket operativsystem maskinen din kjører og hvilken versjon det er.**

```
lsb_release -a
```

---

<br>
<br>

## **16. Finn ut hvilke grupper du selv tilhører på din private s-server (med intel3-innlogging).**
```
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
