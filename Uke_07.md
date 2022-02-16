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


### **Start så fem prosesser i en for-løkke slik at de alle samtidig kjører ./a.out &. Hvordan fordeles CPUene mellom de 5 regne-jobbene? Tast f som gir mulighet til å se flere kolonner, flytt så pekeren ned til kolonnen "Last used CPU" med piltatsten og tast space og deretter q for å komme tilbake til top. Prøv å se hvilke CPUer dine 5 prosesser jobber på og prøv å forklare hvordan OS fordeler jobbene på CPU'ene.**