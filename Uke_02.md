# Uke 2

### **1. Utfør addisjonen 5 + 5 = 10 med binære tall for hånd ved å bruke den samme addisjonsmetoden som man bruker når man legger sammen desimaltall med penn og papir.**

<p align="center">
    <img src="images\uke2_oppgave1.png" style="width: auto;" alt="">
</p>

---

### **2. Se på hva som skjer når man legger sammen to siffer X og Y som står under hverandre i denne algoritmen. Anta at z er mente fra forrige operasjon til høyre for sifferene vi behandler, sifferet under streken blir S og c blir mente til neste operasjon, slik det er vist i figuren under:**
<p align="center">
    <img src="images\add.png" style="width: auto;" alt="">
</p>


<table align="center"><thead><tr><th>X</th><th>Y</th><th>Z</th><th>S</th><th>C</th></tr></thead><tbody><tr><td>1</td><td>1</td><td>1</td><td>1</td><td>1</td></tr><tr><td>1</td><td>1</td><td>0</td><td>0</td><td>1</td></tr><tr><td>0</td><td>1</td><td>1</td><td>0</td><td>1</td></tr><tr><td>0</td><td>1</td><td>0</td><td>1</td><td>0</td></tr><tr><td>1</td><td>0</td><td>1</td><td>0</td><td>1</td></tr><tr><td>1</td><td>0</td><td>0</td><td>1</td><td>0</td></tr><tr><td>0</td><td>0</td><td>1</td><td>1</td><td>0</td></tr><tr><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td></tr></tbody></table>

---

### **3. Hva blir den boolske funksjonen F som funksjon av A og B i figuren under? Skriv ned det boolske uttrykket.**

<p align="center">
    <img src="images\ab.png" style="width: auto;" alt="">
</p>

F(A,B) = A ⋅ B + A

---

### **4. Forenkle det boolske uttrykket for F i forrige oppgave så mye som mulig.**

F(A,B) = A

---

### **5.**

<p align="center">
    <img src="images\fulladder.png" style="width: auto;" alt="">
</p>

---

### **8. Let deg frem til den eneste filen som ligger i en mappe på ditt hjemmeoråde. Innholdet er et ord med 10 tegn. Finn dette ordet og skriv det inn i rapporten, ett ord for hvert medlem i gruppen. Skriv inn ordene sammen med s-nummeret det tilhører.**

* s354410 - 5cHVO5ZMUV
* s354542 - klZ1phWjUI
* s354378 - p071Zou8tV
* s354366 - ddZB8HXqkx

---

### **6. Sett sammen tre slike FullAdder-makroer til en krets som du kan bruke til å utføre summen 3+7=10.**

<p align="center">
    <img src="images\uke2_oppgave6.png" style="width: auto;" alt="">
</p>
---

### **10. Gå til katalogen /usr/bin ved å bruke absolutt path.**

 cd /usr/bin

---

### **11.  Gå til hjemmekatlogen din. Gå deretter til katalogen /usr/bin ved å bruke relativ path.**

* cd ../../usr/bin
---

### **12. Lag to filer med følgende innhold og kjør kommandoen diff**

```
haugerud@data2500:~$ cat fa.txt 
1a
2a
3a
4a
5a
haugerud@data2500:~$ cat fb.txt 
1a
2a
3a
4b
5a
```

```
s194@os694:~/tmp$ diff fa.txt fb.txt
4c4
< 4a
---
> 4b
```
4c4 betyr linje 4 fa, c for change, og linje 4 i fb, det er der forskjellen er.
< 4a betyr at venstre fil(fa.txt) innholder dette, og omvendt.

---

### **14. Utfør følgende Linux-kommandoer i en tom mappe:**

```
mkdir tex
mkdir oblig
mv oblig tex
mkdir oblig
mv tex oblig
```

```
s194@os694:~/tmp$ tree
.
└── oblig
    └── tex
        └── oblig
```

---

### **15.  Gå til roten (/) av systemet. Finn minst tre forskjellige måter å gå tilbake til hjemmektalogen din på.**

1. cd ~
2. cd home/s194/
3. cd
4. cd $HOME

---

### **16. Skriv kommandoen echo bla bla bla > newfile, og bruk more for å se på filens innhold. Kan du forklare hva som har skjedd? Dette kalles redirection.**

echo skriver ut meldingen i terminalen igjen, med med redirection sendes de til den spesifiserte filen i steden for terminalen.

---

### **25.  Lag først en fil hemmelig.txt. Utfør en Linux-kommando som setter filrettighetene for filen hemmelig.txt slik at eieren av filen (du) kun kan lese den, mens alle andre ikke har noen rettigheter.**

* chmod 400 hemmelig.txt

---

### **26. Lag først en fil fil.txt. Utfør en Linux-kommando som setter filrettighetene for filen fil.txt slik at eieren av filen (du) har alle rettigheter, medlemmer av filens gruppe har alle rettigheter untatt å skrive til filen, og alle andre kun kan lese den.**

chmod 754 fil.txt

---

### **28. Hva blir rettighetene til en ny fil du lager med touch? Blir rettighetene de samme om du bruker en editor til å lage en ny fil? Bruk kommandoen umask til å sørge for at nye filer som lages kun kan leses og skrives til av eieren, mens alle andre ikke får noen rettigheter.**

Med touch har filen har 664 rettigheter. Det samme med VIM og jed.
umask 100 gir skrive-/leserettigheter til eier, og ingen til resten.

---
# Ukens skrekk!

### **29.**

Man kommer seg ut ved å bruke sudo chmod 755
Man mister rettigheten til å execute noen form for kommando som eier av mappen. For å komme seg ut må man kjøre kommandoer som root.

---

### **30. Start jed og lagre en fil med navn #fil.txt. Gå ut av jed og prøv å fjerne filen. Hva tror du problemet skyldes? Hvordan kan du fjerne den fra kommandolinjen?**

Det går jo helt fint?

---


