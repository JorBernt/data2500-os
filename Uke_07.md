# Uke 7

### **7.1. Studer følgende C++ program, lag en kopi og kall det b.cpp og kompiler det med \$ g++ b.cpp Kjør deretter programmet på data2500 eller på en annen server og mål hvor lang tid det bruker med kommandoen $ time ./a.out**

```bash
jorber@JBMain:~/uke7/oppgave1$ time ./a.out
103
198
105
115
81
255
74
236
41
205
sum = 157465800000

real    0m10.577s
user    0m10.567s
sys     0m0.010s
```

### **Fjern så kommentartegnene foran linjen som sorterer arrayet, kompiler på nytt og ta tiden på nytt med time. Hvorfor går programmet nå fortere? Hva i ukens forelesninger kan dette relateres til?**
Dette kan relateres til branch prediction. Når listen er sortert, så kan vi garanterer at alle verdiene etter første verdi som er >= 127 er over 127, og alle før er < 127.

---

<br>
<br>

### **7.2. Logg inn på data2500 og last ned programmet regn med wget https://www.cs.hioa.no/~haugerud/regn til din egen hjemmekatalog (Bruk eventuelt wget http://data2500.ddns.net/regn hvis det ikke lastes ned). Programmet gir en feilmelding om ehco og det er meningen at det skal gjøre det, slik at error kan omdirigeres. Programmet regner på et problem i noen minutter (ca. et halvt på data2500 og Linux VM, ett minutt på s-server) og skriver tilslutt resultatet til skjermen. Start programmet slik at det blir en bakgrunnsprosess som skriver resultatet til filen res.txt når den er ferdig og som skriver feilmeldinger til err.txt. Hva skjer om du logger ut før regn er ferdig?**

```
 ./regn >res.txt 2>err.txt &
```

Jobben kjøres fortsatt selv om jeg logger ut.

---
<br>
<br>

### **7.3Finn ut hvor mye CPU-tid regn-programmet bruker og hvor stor andel av den totale CPU-tiden det bruker ved å bruke kommandoen time foran selve kommandoen du kjører med $ time ./regn. For å få med prosentandel CPU, må man formatere output fra time, f. eks slik:**
```
$ TIMEFORMAT="Real:%R User:%U System:%S %P%%"
```
### **der Real viser reell tid, User viser CPU-tid brukt i user-mode (prosessen selv som regner), System viser CPU-tid brukt i kernel-mode (av OS-kjernene) og %P gir prosentandel CPU denne prosessen har brukt. Hvis man legger denne kommandoen inn i ~/.bashrc vil dette formatet alltid brukes.**

```
s354410@data2500:~/uke7/oppgave2$ time ./regn
./regn: line 6: ehco: command not found
./regn : regner....
./regn, resultat: 14045002650000
Real:25,364 User:23,999 System:1,359 99,97%
```
### **Prøv å kjøre programmet slik at også tidsbruken lagres i err.txt. Det siste er det ikke så enkelt å få til......**
```
s354410@data2500:~/uke7/oppgave2$ (time ./regn > res.txt) 2>err.txt
s354410@data2500:~/uke7/oppgave2$ cat err.txt
./regn: line 6: ehco: command not found
Real:24,457 User:23,189 System:1,264 99,98%
```

---

<br>
<br>

### **4.Logg inn på data2500 og last ned programmet regn med wget https://www.cs.hioa.no/~haugerud/regn til din egen hjemmekatalog. Programmet vil stå og regne og bruke så mye CPU det klarer. Start programmet med**
```
$ ./regn&
```
### **og det vil starte å regne. Se at programmet kjører med**
```
top
```
### **Hvor mange prosent CPU får prosessen? (husk at også andre kan teste ut det samme samtidig).Start så en ny prosess mens den forrige kjører med**
```
$ ./regn&
```
### **Se igjen på top. Hvor mange prosent CPU får hver prosess? Tast 1 mens top kjører. Hvor mange CPU'er har data2500?**

Bare de 4 første får ~100% cpu, siden serveren har kun 4 cpuer.

---

<br>
<br>

### **5.Se igjen på top. Tast 1 mens top kjører. Hvor mange CPU'er har data2500? Hvor mange prosent CPU får hver prosess? Hvordan fordeles de to regne-jobbene på CPUer?**

Begge får 100%, og de fordeles over begge to.

### **Start så fem prosesser i en for-løkke slik at de alle samtidig kjører ./a.out &. Hvordan fordeles CPUene mellom de 5 regne-jobbene? Tast f som gir mulighet til å se flere kolonner, flytt så pekeren ned til kolonnen "Last used CPU" med piltatsten og tast space og deretter q for å komme tilbake til top. Prøv å se hvilke CPUer dine 5 prosesser jobber på og prøv å forklare hvordan OS fordeler jobbene på CPU'ene.**

De fordeles over alle CPU'ene. Det ser ut til at prosessene blir delt opp i veldig små deler, og CPU'en som er først tilgjengelig tar seg av neste bit. 
---
<br>
<br>

### **9. På gruppens Linux-VM: lag en bruker for hvert medlem av gruppen, bruk samme brukernavn som dere har på data2500(s123456 eller lignende). Pass NØYE på å ha et ordentlig passord, minst 8 tegn og gjerne tall og spesialtegn, ellers vil dere kunne bli hacket. Prøv å logge deg på som en av brukerene du laget.**

### **Hvilken kommando kan man bruke for å se hvilke grupper man tilhører?**

```
groups
```

### **Prøv om din nye bruker kan bli root ved å kjøre kommandoen "sudo su". Forklar hvorfor det ikke går (HINT: se hvilke grupper din nye bruker er medlem av i forhold til den brukeren du fikk tildelt.)**

    Funker ikke fordi brukeren ikke er lagt til i "sudoers"-listen.

## **Se om du kan legge den nye brukeren din til riktig gruppe slik at den også kan bli root. Hva er det som gjør at medlemmene i denne gruppen får sudo-rettigheter?**

I filen /etc/sudoers står det følgende:

``` 
# User privilege specification
root    ALL=(ALL:ALL) ALL

# Members of the admin group may gain root privileges
%admin ALL=(ALL) ALL

# Allow members of group sudo to execute any command
%sudo   ALL=(ALL:ALL) ALL
```

Som sier at brukere som er medlev av sudo får alle rettigheter.

---

<br>
<br>
 
### **10Lag som brukeren groupXX (på Linux-VM der XX er ditt gruppenummer) en katalog ~/felles og lag en fil info.txt i denne katalogen. Lag så en ny gruppe med navn os med kommandoen**

    sudo addgroup os

### **Sørg så for at groupXX blir medlem av denne gruppen. og deretter for at de andre brukerne dere tidligere lagde på Linux-VM (s123456 eller lignende) også blir medlemmer av denne gruppen. Bruk så kommandoene chgrp og chmod til å sørge for at alle medlemmer av gruppen os for lov til å editere og lagre filen ~/felles/info.txt. Logg inn som en av de andre brukerne og sjekk at de virkelig får editere filen. Endres hvem som eier filen når du editerer og lagrer den? (hvis du bruker chgrp som brukeren groupXX, må du logge ut og inn igjen først. Som du ser med groups blir brukeren først da oppfattet som medlem av os)**

    Eieren endres ikke. 


---

<br>
<br>

## **Ukens utfordring Som brukeren groupXX på Linux-VM: Sett filrettighetene til filen ~/felles/info.txt slik at brukeren selv og alle i gruppen ikke har noen rettigheter, mens alle andre har alle rettigheter (såkalte James Bond rettigheter). Prøv å se på innholdet med**
    $ cat ~/fil.txt
### **Logg inn som en annen bruker (s123456) og se på innholdet med**

    $ cat ~groupXX/fil.txt

### **Forklar.**

    Brukeren får leste filen fordi den ikke er eier, og heller ikke medlem av OS gruppen. Derfor går under brukeren under "andre" som har alle rettigheter.

---

<br>
<br>


## **12.**
<p align="center">
    <img src="images\apache.png" style="width: auto;" alt="">
</p>

---
<br>
<br>

### **7.13 (Oblig) Installer først screen på Linux-VM om det ikke er installert:

    sudo apt update -y
    sudo apt install -y screen
    
### **Anta at du er på os-gruppe osXX hvor XX er ditt gruppenummer. Følg forelesningsnotatene, logg inn som brukeren groupXX og lag en screen session som kan deles av andre. Få så alle de andre på gruppen til å logge seg på med samme bruker, groupXX, og få deretter alle på gruppen til å koble seg til samme screen. Om du er alene på en gruppe, test med to forskjellige innloggingsvinduer. Dette kan være veldig praktisk om dere sitter rundt et bord og samarbeider om Linux-oppgaver og for eksempel skriver et script. Et av medlemmene kan da vise hvordan et problem løses, eventuelt kan alle prøve forskjellige kommandoer. Det gjelder bare å sørge for å være en av gangen, for alle kan taste samtidig.Det er også mulig å få til en delt screen mellom forskjellige brukere om man nøye følger punkt 4 på siden http://www.pc-freak.net/blog/share-screen-terminal-session-in-linux-screen-share-between-two-or-more-users-howto/.**


## **14.**

```bash
#! /bin/bash

tar cfz dir.tgz /tmp/dir
scp dir.tgz group20@os20.vlab.cs.hioa.no:~/
rm dir.tgz
ssh group20@os20.vlab.cs.hioa.no 'tar xfz dir.tgz'
ssh group20@os20.vlab.cs.hioa.no 'rm dir.tgz'
```

---

<br>
<br>

