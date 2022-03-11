# OS OBLIG 2

* ### Jørgen Berntsen - s354410
* ### Atif Aziz - s354542
* ### Adrian August Grøtter - s354378
* ### Tony Strømsnæs - s354366

---
<br>
<br>

# Uke 6

### **6.1.(Oblig) Les 5.2 'En linje høynivåkode kan gi flere linjer maskininstruksjoner' i Forelesningsnotatene, kompiler programmene, C-koden main og assembly-koden enlinje.s (den som starter med .globl enlinje), vis at en kjøring gir svaret 42 og forklar så hvorfor svaret blir 42 utifra assembly-koden.**

    gcc -no-pie enlinje.s main.c / commando som kompilerer Assembly koden enlinje og c koden main

    Vi har to variabler i assembly koden, svar(32) og memvar(10) under datafeltet som legger variablene i ram

    Først legger memvar i rbx
    Også legges rbx til svar som ligger i ram = svar = memvar + svar
    Også flyttes svar til rax som igjen returneres. 

---
<br>
<br>

### **2.(Oblig) Bruk så det C-programet som gjør det samme som assembly-koden i forrige oppgave(deklarer int-variabler svar og memvar), kompiler det sammen med main C-programmet på samme måte og sjekk at svaret blir det samme. Kompiler C-funksjonen alene med gcc -S og studer den resulterende assembly-koden.**

```bash
jorber@JBMain:~/uke6$ gcc main.c enlinje.c
jorber@JBMain:~/uke6$ ./a.out
Kaller enlinje()...
Svar = 42
```

Assembly:
```bash
enlinje:
.LFB0:
        .cfi_startproc
        endbr64
        pushq   %rbp
        .cfi_def_cfa_offset 16
        .cfi_offset 6, -16
        movq    %rsp, %rbp
        .cfi_def_cfa_register 6
        movl    $32, -8(%rbp) #Flytter verdi 32 til register A
        movl    $10, -4(%rbp) #Flytter verdi 10 til register B
        movl    -4(%rbp), %eax #Flytter register B til RAM A
        addl    %eax, -8(%rbp) #Adderer RAM A til register A (10 + 32)
        movl    -8(%rbp), %eax #Flytter register A til RAM A (42)
        popq    %rbp            #Popper svaret for å returnere?
        .cfi_def_cfa 7, 8
        ret
        .cfi_endproc
```

### **Hvor mange linjer leder den ene høynivå-koden til?**
Den leder til 5 linjer assembly :

```
movl    $32, -8(%rbp) #Flytter verdi 32 til register A
movl    $10, -4(%rbp) #Flytter verdi 10 til register B
movl    -4(%rbp), %eax #Flytter register B til RAM A
addl    %eax, -8(%rbp) #Adderer RAM A til register A (10 + 32)
movl    -8(%rbp), %eax #Flytter register A til RAM A (42)
```
### **Hvordan endrer den resulterende assembly-koden seg om du bruker "long long" istedet for "int" for variablene i C-funksjonen?**

```
jorber@JBMain:~/uke6/long$ diff enlinjeint.s enlinjelonglong.s
1c1
<       .file   "enlinjeint.c"
---
>       .file   "enlinjelonglong.c"
14,18c14,18
<       movl    $32, -8(%rbp)
<       movl    $10, -4(%rbp)
<       movl    -4(%rbp), %eax
<       addl    %eax, -8(%rbp)
<       movl    -8(%rbp), %eax
---
>       movq    $32, -16(%rbp)
>       movq    $10, -8(%rbp)
>       movq    -8(%rbp), %rax
>       addq    %rax, -16(%rbp)
>       movq    -16(%rbp), %ra
```
I long long versjonen ser det ut som størrelsen på registerene har doblet seg.
Det gir mening siden int er 32 bit, og long long er 64 bit.
---

<br>
<br>

### **6.7.(Oblig) Lag en find-kommando på data2500 som lister alle filene i hjemmemappen din som ble endret i løpet av 30 januar 2022. (velg en annen dato å teste med hvis du ikke har endret noen filer denne dagen)**

    find ./ -newermt "2022-01-30" ! -newermt '2022-01-31'
<br>
<br>

### **6.8(Oblig) Lag en fil med navn fil.txt som inneholder**

    s802399@stud.hioa.no
    s886878@stud.hioa.no
    s886876@stud.hioa.no
    s886885@stud.hioa.no
    s886884@stud.hioa.no
    s850806@stud.hioa.no
    s886873@stud.hioa.no
    s886888@stud.hioa.no
    s808855@stud.hioa.no
    s856627@stud.hioa.no
    s886878@stud.hioa.no
    s299507@stud.hioa.no
    s850798@stud.hioa.no
    s803434@stud.hioa.no
    s886879@stud.hioa.no
    s886877@stud.hioa.no
    s959938@stud.hioa.no
    s886880@stud.hioa.no
    s826650@stud.hioa.no
    s886882@stud.hioa.no
    s886874@stud.hioa.no
    s859987@stud.hioa.no
    s803833@stud.hioa.no
    s886885@stud.hioa.no
  
### **Lag så en kommando som fra denn filen lager en ny fil nyfil.txt hvor alle forekomster av stud.hioa.no er byttet ut med oslomet.no**

### MED SCRIPT

```bash
# /bin/bash
rm resultat.txt 2>/dev/null
while read LINE; do
	echo $LINE | sed s/stud.hioa.no/oslomet.no/ >> resultat.txt
done
cat resultat.txt


```

### MED COMMAND
    cat fil.txt | sed s/stud.hioa/oslomet/ >> nyfil.txt

    jorber@JBMain:~/uke6/oppgave8$ ./script.sh < fil.txt
    s802399@oslomet.no
    s886878@oslomet.no
    s886876@oslomet.no
    s886885@oslomet.no
    s886884@oslomet.no
    s850806@oslomet.no
    s886873@oslomet.no
    s886888@oslomet.no
    s808855@oslomet.no
    s856627@oslomet.no
    s886878@oslomet.no
    s299507@oslomet.no
    s850798@oslomet.no
    s803434@oslomet.no
    s886879@oslomet.no
    s886877@oslomet.no
    s959938@oslomet.no
    s886880@oslomet.no
    s826650@oslomet.no
    s886882@oslomet.no
    s886874@oslomet.no
    s859987@oslomet.no
    s803833@oslomet.no
    s886885@oslomet.no
---
<br>
<br>

### **6.10.(Oblig) Lag en enlinjes Linux-kommando som skriver ut en liste med de 10 største filene i /etc, omtrent slik (på data2500):***

    -rw-r--r-- 1 root root   70481 Jan 15  2021 mime.types
    -rw-r--r-- 1 root root   26599 Jan 25 06:44 ld.so.cache
    -rw-r--r-- 1 root root   12813 Mar 27  2021 services
    -rw-r--r-- 1 root root   10593 Jan 30  2021 sensors3.conf
    -rw-r--r-- 1 root root   10477 Feb  7  2020 login.defs
    -rw-r--r-- 1 root root   10056 Dec  2  2020 nanorc
    -rw-r--r-- 1 root root    9443 Jan  2 23:35 locale.gen
    -rw-r--r-- 1 root root    6169 Feb 27  2021 sudo_logsrvd.conf
    -rw-r--r-- 1 root root    5662 Dec 31 21:14 ca-certificates.conf
    -rw-r--r-- 1 root root    5215 Feb 19  2021 manpath.config

    ls -laS /etc | head -11
<br>
<br>

### **6.12. (Oblig) Lag et bash-script som skriver ut en oversikt tilsvarende den som er gitt nedenfor. All informasjon skal genereres dynamisk av scriptet og vil dermed avhenge av hvem som kjører det, hva scriptet heter, hvor det kjøres etc. Bruk scriptet fra forrige uke som teller filer og linker i dette scriptet (Hint: finn ut hva shell-variablene $0 og $$ er).**
    haugerud@data2500:~$ ./info.sh 
    Du har brukernavn haugerud og kjører scriptet ./info.sh med PID = 816133 
    på maskinen data2500 som kjører operativsystemet Linux
    Oversikt over din hjemmekatalog /home/haugerud:
    Filer: 95
    Kataloger: 14
    Linker: 0
    Ditt default shell er /bin/bash og du befinner deg i 
    katalogen /home/haugerud
    Totalt 32 brukere er oppført i passordfilen og det er definert 58 grupper
    Oversikt over dine grupper:
    haugerud : groups: cannot find name for group ID 101964
    101964 sudo

```bash
#! /bin/bash

user=$(whoami)
script=$(basename $0)
os=$(uname)
pid=$(ps aux | grep $script | head -1 | awk '{print $2}')
directories=$(find ~/ -type d -not -path '*/.*' | wc -l)
files=$(find ~/ -type f -not -path '*/.*' | wc -l)
links=$(find ~/ -type l -not -path '*/.*' | wc -l)
currentDir=$(pwd)
usersInPasswd=$(cat /etc/passwd | wc -l)
groups=$(cat /etc/group | wc -l)

echo Du har brukernavn $user og kjører scriptet ./$script med PID = $pid 
echo på maskinen $(hostname) som kjører operativsystemet $os
echo oversikt over din hjemmekatalog $HOME:
echo Filer: $files
echo Kataloger: $directories
echo Linker: $links
echo Ditt default shell er $SHELL og du befinner deg i 
echo katalogen $currentDir
echo Totalt $usersInPasswd brukere er oppført i passordfilen og det er definert $groups grupper
echo Oversikt over dine grupper:
echo $(groups $user)
```

<br>
<br>

### **6.16(Oblig) Dette er ukens s-server oppgave. Logg inn på din private intel2 s-server som du har brukt tidligere med noe slikt som**

    $ ssh -p 635 s135@intel2.vlab.cs.oslomet.no
  
### **Som før er portnummeret s-nummeret + 500, 635 er kun for s135. Finn din s-gruppe på Canvas, der ligger også passordet du trenger for å logge inn. På s-serveren er det fra før 1000 mapper hvor du skulle lete etter en fil i forrige uke. Nå er det lagt inn en fil en fil med navn dfil.txt i hver eneste av de 1000 mappene. Alle er like store og alle unntatt en inneholder teksten "Ikke denne". Filen du skal lete deg frem til skiller seg ut fra de andre ved at den sist ble endret 11. februar 2013 (2013-02-11 02:26:11). Å kunne finne en fil som ble endret på et gitt tidspunkt på en Linux-server kan i mange tilfeller være veldig nyttig og her må du prøve å få til det. Les ukens forelesningsnotater hvis du står fast. Innholdet i denne filen er som vanlig en 10-tegns kode som viser at du har løst oppgaven. For å sjekke at du har funnet rette streng, skriv den inn på siden https://nexus.cs.hioa.no/~haugerud/os6.php og du får beskjed om du har skrevet riktig. I tilegg blir du da med på konkurransen om å finne denne koden fortest mulig!**

    ls -ld */*/*/* */*/* */* * | grep dfil.txt | find -newermt 2013-2-11 ! -newermt 2013-2-12

    s108 - LKFSK8HBkd
    s15 - BIbFirWI9o
    s253 - Nk5XPbjkq6
    s194 - qZnRmBljcy

---
<br>
<br>

# Uke 7

### **7.2.(Oblig) Logg inn på data2500 og last ned programmet regn med wget https://www.cs.hioa.no/~haugerud/regn til din egen hjemmekatalog (Bruk eventuelt wget http://data2500.ddns.net/regn hvis det ikke lastes ned). Programmet gir en feilmelding om ehco og det er meningen at det skal gjøre det, slik at error kan omdirigeres. Programmet regner på et problem i noen minutter (ca. et halvt på data2500 og Linux VM, ett minutt på s-server) og skriver tilslutt resultatet til skjermen. Start programmet slik at det blir en bakgrunnsprosess som skriver resultatet til filen res.txt når den er ferdig og som skriver feilmeldinger til err.txt. Hva skjer om du logger ut før regn er ferdig?**

```
 ./regn >res.txt 2>err.txt &
```

Jobben kjøres fortsatt selv om jeg logger ut.

---
<br>
<br>

### **7.3(Oblig) Finn ut hvor mye CPU-tid regn-programmet bruker og hvor stor andel av den totale CPU-tiden det bruker ved å bruke kommandoen time foran selve kommandoen du kjører med $ time ./regn. For å få med prosentandel CPU, må man formatere output fra time, f. eks slik:**
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

### **7.5(Oblig).Se igjen på top. Tast 1 mens top kjører. Hvor mange CPU'er har data2500? Hvor mange prosent CPU får hver prosess? Hvordan fordeles de to regne-jobbene på CPUer?**

Begge får 100%, og de fordeles over begge to.

### **Start så fem prosesser i en for-løkke slik at de alle samtidig kjører ./a.out &. Hvordan fordeles CPUene mellom de 5 regne-jobbene? Tast f som gir mulighet til å se flere kolonner, flytt så pekeren ned til kolonnen "Last used CPU" med piltatsten og tast space og deretter q for å komme tilbake til top. Prøv å se hvilke CPUer dine 5 prosesser jobber på og prøv å forklare hvordan OS fordeler jobbene på CPU'ene.**

De fordeles over alle CPU'ene. Det ser ut til at prosessene blir delt opp i veldig små deler, og CPU'en som er først tilgjengelig tar seg av neste bit. 
---
<br>
<br>

### **7.9. På gruppens Linux-VM: lag en bruker for hvert medlem av gruppen, bruk samme brukernavn som dere har på data2500(s123456 eller lignende). Pass NØYE på å ha et ordentlig passord, minst 8 tegn og gjerne tall og spesialtegn, ellers vil dere kunne bli hacket. Prøv å logge deg på som en av brukerene du laget.**

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
 

## **12.(Oblig) Installer en Apache webserver på gruppens Linux-VM med kommandoene**

  sudo apt update -y
  sudo apt install -y apache2
  
### **Deretter må du starte webserveren med**
    sudo service apache2 start

### **Test at Web-serveren virker ved å skrive inn http://os??.vlab.cs.hioa.no men der du bytter ut ?? med ditt gruppenummer. Alt du legger inn i katalogen /var/www/html kommer opp her. Altså har du nå din egen private webserver som kan nås fra overalt. Endre /var/www/html/index.html slik at man kan se hvilken gruppe som styrer denne webserveren.**

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
    
<p align="center">
    <img src="images\unknown.png" style="width: auto;" alt="">
</p>



## **7.14.(Oblig) Start fra data2500 og bruk ssh-copy-id til å sørge for at du kan logge inn til group-brukeren din på Linux-VM uten å taste passord (start fra s-server om du ikke kommer inn med ssh fra data2500 til Linux-VM). Se forelesningsnotater. Lag deretter et script som skal kjøres fra data2500. Scriptet skal først pakke ned mappen /tmp/dir på data2500 med tar cfz og lage en tgz-fil(pakket med tar og zippet med gzip, se notater). Deretter skal det flytte pakken til din bruker på Linux-VM med scp og pakke ut pakken i ~/tmp på Linux VM. Om denne mappen ikke finnes på Linux-VM, skal den lages først. Alle mellomlagrede filer (.tgz) på både data2500 og Linux VM skal slettes etterpå av scriptet. Når scriptet kjøres på data2500**

    s123456@data2500:~$ ./s.sh
    dir.tgz
    100%   43KB  12.0MB/s   00:00    
  
skal det se omtrent slik ut på Linux-VM:
    group100@os100:~$ ls -l tmp/dir/
    total 684
    -rw-r--r-- 1 group100 group100 694186 Feb 16 18:08 auth.log
    -rw-r--r-- 1 group100 group100      4 Feb 16 18:08 enFil.txt**

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

### **7.15(Oblig) (Bruk en s-server om du ikke kommer inn med ssh fra data2500 til Linux-VM) Installer først rsync på Linux-VM om den ikke er installert:**

  sudo apt update -y
  sudo apt install -y rsync
  
### **Lag et script som bruker rsync til å ta backup av av mappen /home/group?? med undermapper og filer på os??, hvor ?? er ditt gruppe-nummer og group?? er gruppens bruker på Linux-VM. La scriptet ta backup til en mappe ~/home for din bruker på data2500. Scriptet skal kjøres fra data2500, slik at du ikke gir andre med tilgang til Linux-VM tilgang til ditt område på data2500. NB! rsync må være installert på begge sider, så du må først installere rsync på Linux-VM. Hva skjer om du sletter en fil på Linux-VM og du etterpå gjør rsync? Bruk en rsync-kommandoen som gjør slik at filen da slettes der du lagrer backup(på data2500 i dette tilfellet). Bruk cron til å sørge for at det tas backup hver natt (kjør crontab -e på data2500) og få scriptet til å skrive en linje med dato og klokkeslett for når backup ble tatt til en loggfil i din hjemme-mappe. Test ut med en hurtigere backup-frekvens (f.eks. ett minutt) for å sjekke at alt virker og sett så til nattlig backup. Pass på å bruke full path i crontab!**

<p align="center">
    <img src="images\unknown1.png" style="width: auto;" alt="">
</p>

---    
<br>
<br>

### **7.16 (Oblig) Dette er ukens s-server oppgave. Logg inn på din private intel2 s-server som du har brukt tidligere med noe slikt som**

    $ ssh -p 635 s135@intel2.vlab.cs.oslomet.no
  
### **Som før er portnummeret s-nummeret + 500, 635 er kun for s135. Finn din s-gruppe på Canvas, der ligger også passordet du trenger for å logge inn. På s-serveren er det fra før 1000 mapper hvor du skulle lete etter en fil i forrige uke. Nå er det lagt inn en tekst-fil i alle mapper. Du skal finne den av disse tekstfilene som er størst, inneholder flest antall bytes. Innholdet i denne filen (første linje) er som vanlig en 10-tegns kode som viser at du har løst oppgaven. For å sjekke at du har funnet rette streng, skriv den inn på siden https://nexus.cs.hioa.no/~haugerud/os7.php og du får beskjed om du har funnet riktig fil og streng. I tilegg blir du da med på konkurransen om å finne denne koden fortest mulig!**