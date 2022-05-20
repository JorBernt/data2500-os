# Eksamen 2019 Vår

## Oppgave 1

    AND

## Oppgave 2

    OR-port

## Oppgave 3

    A*B+!A*B

## Oppgave 4

    B

## Oppgave 5

    Forklar kort hvorfor det er viktig og nødvendig å ha en klokke i en CPU, spesielt når resultatet fra beregninger
    skal mellomlagres. Bruk gjerne eksempelet fra forelesning der studenter simulerte D-låser i forklaringen.

---

    Det er viktig å ha en klokke så man unngår at verdier leses fra en D-Lås samtidig som det skrives til den.

## Oppgave 6

    Forklar kort hvordan maskinkoden for assembly-instruksjonen
    add %rax, %rbx
    vil føre til at to tall legges sammen. Beskriv spesielt hvilken rolle instruksjonsdekoderen, registerne og ALU har
    når denne opperasjonen gjennomføres.

---

    add - assembly kode/instruksjon for addisjon

    instruksjonsdekoderen konverterer assembly til maskinkode/instruksjoner. Disse kontrolbittene sendes da til ALU som utfører operasjonene.

    Her sendes det to tall inn som skal adderes til ALU, ALU utfører addisjon og sender resultat tilbake til %rbx

## Oppgave 7

    Hvilken Linux-kommando lager en ny katalog?

---

    mkdir

## Oppgave 8

    Hvilken katalog referer .. (to punktum) til i et bash-shell?

---

    Mappen over den du står i

## Oppgave 9

    Hva blir output av bash-kommandoen
    echo "hei du der" | sort | grep du

---

    hei du der

## Oppgave 10

    Den 21 april 2019 kl 22.00 om kvelden utfører du på en Linux-server følgende kommando:
    $ find /home/hh/div -type d -newermt "21 Apr 2019 00:00" -ls
    2623843 4 drwx------ 74 hh hh 4096 april 21 16:05 /home/hh/div
    2687210 4 drwx------ 2 hh hh 4096 april 21 21:25 /home/hh/div/parkering
    Forklar kort hva kommandoen gjør og hvilken informasjon output gir deg. For å finne ut av hva opsjonene
    betyr, kan du se i manual-siden for kommandoen find:
    man find
    Denne manualsiden kan du også få bruk for i oppgaven om bash-scripting.

---

    find /home/hh/div -type d -newermt "21 Apr 2019 00:00" -ls

    Find : kommando for å søke etter filer og mapper
    neste er path
    -type d  for å spesifisere at det er mappe vi skal finne (directory)
    -newermt "21 Apr 2019 00:00" spesifisere fra tid. Altså filer endret og lagret etter denne tiden
    -ls liste opp alle

## Oppgave 11

    Denne oppgaven er basert på en sann historie.... En IT-forsker bruker en Linux-server med host-navn
    research3 til å kjøre maskinlæring-proggrammer i python ved å kjøre følgende kommando i et bash-shell:
    research3:~$ python runML.py p3600-100.cnf
    Dette programmet tar omtrent en time på å kjøre ferdig og skriver resultatet til en fil i samme mappe. Forskeren
    har i samme mappe totalt 30 forskjellige input-filer, alle med filendelse .cnf, og ønsker å utnytte alle CPUene
    på serveren til å kjøre alle de 30 jobbene i parallell. Serveren research3 har 32 uavhengige CPUer. Forskeren
    ber deg derfor om hjelp til å skrive et bash-script som hun kan kjøre på serveren i mappen der de 30 inputfilene ligger, slik at hun ikke må kjøre en jobb av gangen fra kommandolinjen. Skriv et slikt bash-script:

```bash
#! /bin/bash
for fil in *.cnf; do
    python runML.py $fil&;
done
```

---

## Oppgave 12

    Forskeren spør deg om omtrent hvor lang tid du tror det vil ta for scriptet å fullføre alle beregningene. Gi henne
    et begrunnet svar.

---

    dette programmet bruker 1 time på en cpu.
    Maskinen til professoren har 32 cpu`er

    Scriptet vårt starter 30 jobber samtidig så disse vil da kjøre på hver sin cpu og dermed kun bruke 1 time totalt på alle

## Oppgave 13

    Forskeren skal hente barn i barnehagen om en halv time og ønsker derfor å sette igang scriptet på en slik måte
    at hun kan logge ut fra serveren research3 når hun går for dagen, men slik at scriptet fortsetter å kjøre. Hun vil
    også gjerne kunne logge inn via ssh hjemmefra senere på kvelden og se resultatfilene. Og hun vil også gjerne
    kunne se output som python-programmet gir direkte til konsollet, inkludert eventulle feilmeldinger. Forklar kort
    hvordan hun kan oppnå dette, og skriv ned hvilke kommandoer hun må kjøre på research3 før hun går og
    hvilke hun må kjøre hjemmefra.

---

    Hun kan starte en screen session i linux før hun går, som lager et shell hun kan koble seg på hjemmefra.
    En screen session startes ved å skrive `screen -S <session navn>`
    Og hun logge seg på med å skrive `screen -r <session navn>` etter hun har ssh'et seg inn hjemmefra.

```bash
#! /bin/bash
for fil in *.cnf; do
    python runML.py $fil&;
done
```

    research3:~$ run.sh > run.log 2>&1 &

## Oppgave 14

    Lag et bash-script som skriver ut en oversikt over hvor mange linker, filer og
    kataloger(mapper) det finnes i katalogen scriptet kjøres fra og i alle dens underkataloger. Output fra scriptet
    skal se tilsvarende ut som dette:

    Filer: 129
    Kataloger: 4
    Linker: 0

---

```bash
#! /bin/bash

fil=0
kat=0
link=0

for f in $(find . );
do
    if [[ -d $f ]]
    then
        ((kat++))
    fi
    if [[ -f $f ]];
    then
        ((fil++))
    fi
    if [[ -L $f ]];
    then
        ((link++))
    fi
done

echo "Antall filer: $fil"
echo "Antall mapper: $kat"
echo "Antall linker: $link"

```

## Oppgave 15

    Forklar hvordan et operativsystem kan kjøre flere titalls samtidige prosesser på samme CPU og gi prosessene
    rask responstid til tross for at de må dele på ressursene. Er OS avhengig av spesiell hjelp fra hardware for å
    ordne dette på en god og effektiv måte? Forklar kort.

---

    Multitasking. Prosesser settes i en Round Robin kø og tildeles timeslices/tics. OS scheduleren fordeler ticks rettferdig til alle prosessene. En prosess får cpu tid og fullfører sine ticks før neste prosess får lov til å få cpu tid. En hardware timer slås inn hvert 100 dels sekund som utfører en context switch. Det går en løkke som minsker ticks på hver prosess som kjører. Alt fra prosessen som kjøres lagres PCB til neste gang denne prosessen får cpu tid.

## Oppgave 16

    Forklar kort hva et systemkall er og spesielt om OS-kjernen er involvert når det gjøres et systemkall. Kan en
    kjørende prosess bli satt på vent på grunn av et systemkall? Forklar svaret, bruk gjerne (men ikke
    nødvendigvis) eksempelet fra vaffel-prosessen under forelesningen.

---

    Systemkall er når en prosess trenger hjelp fra kjernen.

    Systemkall er en rekke med metoder (API-er) som OS-user/prosesser kan kalle på for å utføre operasjoner i priviligiert minne.
    Dette kan f.eks å lese filer, få prosessID, vise mappeinnehold osv.

    Prosesser kan bli satt på vent når systemkall kjøres, bl.a ved lesing av tastaturinput.

## Oppgave 17

    Kan en kjørenede prosess flyttes fra CPUen den kjører på til en annen CPU mens den kjører? Hvis det er
    mulig å flytte den, må da også alle pages den har i RAM flyttes? Hvordan utføres isåfall det? Forklar svarene kort

---

    Når en prosess får tildelt cputid

## Oppgave 18

    Forklar kort hva det vil si at en prosess kan ha flere tråder.

---

    Programmmeren kan velge å kode programmet til å bruke flere threads, dette vil føre til at en prosess får flere tråder og dermed kunne kjøre på flere cpu`er samtidig. Dette kalles å parallellisere koden.0B

## Oppgave 19

    Forklar kort hva følgende PowerShell-kommandoer gjør og spesielt resultatet av den siste kommandoen:
    PS C:\Users\os> $now = Get-Date
    PS C:\Users\os> $then = Get-Date "20 Januar 2019"
    PS C:\Users\os> $then
    søndag 20. januar 2019 00.00.00
    PS C:\Users\os> $then -lt $now
    True

---

    $now = Get-Date - Dagens dato lagres i now variabel
    $then = Get-Date "20 Januar 2019" - 20 jan 2019 lagres i then variabelen
    $then - then variabelen skrives ut til shell
    søndag 20. januar 2019 00.00.00

    $then -lt $now - Sjekker om datoen i variabelen $then er mindre enn $now
     True

## Oppgave 20

    Følgende viser deler av output fra en PowerShell-kommando:
    PS C:\Users\os> ls fil.txt | Get-Member
    TypeName: System.IO.FileInfo
    Name MemberType Definition
    ---- ---------- ----------
    Delete Method void Delete()
    Encrypt Method void Encrypt()
    ToString Method string ToString()
    PSDrive NoteProperty PSDriveInfo PSDrive=C
    PSIsContainer NoteProperty bool PSIsContainer=False
    CreationTime Property datetime CreationTime {get;set;}
    Extension Poperty string Extension {get;}
    FullName Property string FullName {get;}
    LastAccessTime Property datetime LastAccessTime {get;set;}
    LastWriteTime Property datetime LastWriteTime {get;set;}
    Length Property long Length {get;}
    Name Property string Name {get;}
    Bruk dette til å lage en PowerShell-kommando som gir hvilket årstall filen fil.txt ble laget.

---

    (ls fil.txt).CreationTime.Year

## Oppgave 21

    Lag på grunnlag av det du har sett i de to foregående deloppgavene, en PowerShell kommando som viser alle
    filer og mapper under C:\User\os som sist gang ble skrevet til i løpet av 20 januar 2019.

```powershell
ls -r C:\User\os | where {$_.LastWriteTime -le (Get-Date "20 January 2022")}
```

## Oppgave 22

    Utifra Linux-kommandoen
    rex:~/undervisning/OSogUNIX/eksamen/hh$ ls -l fil.txt
    -rw------- 1 haugerud haugerud 4 april 29 13:48 fil.txt
    og PowerShell-kommandoen
    PS C:\Users\os> ls fil.txt
    Directory: C:\Users\os
    Mode LastWriteTime Length Name
    ---- ------------- ------ ----
    -a---- 19.03.2018 00.12 188 fil.txt
    kan man se ved hvilket tidspunkt de to filene med samme navn sist ble endret. Hvilken av de to kommandoene
    kan også gi tidspunktet for når filen sist ble aksessert(ikke endret, men lest)? Forklar kort hva som gjør at det er mulig å hente ut denne informasjonen og skriv ned kommandoen som gjør det.

---

(ls fil.txt).LastAccessTime
ls fil.txt | select LastAccessTime

Siden alt er objekter i powershell, så kan den lagre når vi åpner filen i variabelen LastAccessTime.

## Oppgave 23

FreeBSD med Intel-prosessor
Mac OS X 10.6 med Intel-prosessor

## Oppgave 24

## Oppgave 25

## Oppgave 26
