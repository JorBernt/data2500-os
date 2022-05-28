# Prøveeksamen 2020

## Oppgave 1

    En transistor
    
## Oppgave 2

    100

## Oppgave 3

    En CPU har en regneenhet, kalt ALU, som kan gjøre en rekke forskjellige talloperasjon, som da f.eks addisjon.
    CPU'en leser tallenene fra minne, og legger de i sine register, som er små lynkjappe lagringsenheter på selve CPU'en.
    Videre så utfører den adderingen, ved å først lese av et av tallene og de legges i mellomlager, før den leser av det andre tallet, og adderer det oppå det andre ved bruk av binær addisjon. CPU'en klarer ikke å legge to tall sammen samtidig, og må derfor bruke mellomlagringen. ALU'en vet hva den skal gjøre, ved at den får forskjellige kontrollsignal. Selve beregningen skjer ved at det er en rekke "Full addere" som er koblet sammen, hvor hver av de kan lese inn to binære bits, og legge de sammen. Om begge to er 1, så blir den adderen sitt resultat 0, og den sender 1 i mente videre til neste full adder. Resultatet blir lagret i et register, og returnet til minne hvor det skal være.

## Oppgave 4

    Hovedforskjellen mellom java og c koden, er at java kompileres til java bytecode, som så leses av JVM (Java virtual machine) og da kompileres til maskininstrukser. C koden kompileres direkte til assembly. Det kan forekomme tidsforskjell siden c-koden kjøres direkte til maskinkode, mens java må gjennom JVM først.

## Oppgave 5

    Context switch er at CPU'ene bytter på hvilken prosess de jobber på.
    Når en context switch skjer, så settes prosessen som byttes fra på pause, og en annen tar over. Den nye prosessen får tildelt timeslices, dvs. tid som den skal få lov til kjøre. Dette er ticks, som telles nedover med 1 hver gang det kommer et hardware interrupt.
    Når den er på 0, så skjer det en ny context switch. De kan skje når som helst, mitt i kritiske kodeavsnitt, og det er opp til utvikleren og håndtere dette. Context switch er styrt av OS.

## Oppgave 6

    Hyperthreading er Intel sitt navn på SMT(Simultaneous mulithreading).
    Det vil si deler av CPUen er duplisert, som f.eks registerne, men ikke ALU'en. Det betyr at CPUen har to tråder, og kan kjøre to prosesser samtidig. Siden de ikke deler ALU, så har dette ikke mye å si for CPU-intensive prosesser, men om en tråd på gå til minne for hente data, så kan den andre bruke ALU'en i mellomtiden. Det vil gjøre minne-intensive prosesser går mye raskere. Denne context switchen blir derimot ikke gjort av OS, men av hardware, som er flere tusen ganger kjappere. OS og utvikleren av programmet kan ikke styre hvordan CPU'en fordeler prosessen.

    Multithreading er når en applikasjon velger å bruke flere ulike CPU'er samtidig. Dette styres av utvikleren, som må skrive paralellisert kode. Når en applikasjon bruker multithreading kan da flere deler av applikasjonen bruke en ALU hver, i motsetning til hyperthreading. Siden multithreading kan gjøre beregninger samtidig, og CPU'en ikke vet noe om hvordan koden er strukturert, så må utvikleren bruke verktøy som mutex for å låse tråder når leses og skrives til felles data, eller instrukser som er avhenginge av hverandre.

    Hver CPU som kjøres samtidig med mulithreading, kan utnytte hyperthreading hver for seg, det er ikke noe forskjell på de prosessene fra en ikke multithreaded prosess.


## Oppgave 7

    Alle prosessene vil bli tildelt så lik tid som mulig. De vil få tildelt jiffies, og kjøres til de er brukt. Så vil det bli tildelt nye jiffies. Når en prosess har brukt de opp, legges i de i ready-listen, hvor de venter på å få tildelt nye jiffies så snart som mulig.

    Når 6 prosesser kjører på 4 CPU'er vil det ta omtrent en og en halv gang tiden det tar å kjøre en til fire prosesser.

## Oppgave 8
    Tid for en tråd ganget med antall tråder delt på antall CPU'er.
    De trenger til sammen 30 * 6 minutter med CPU tid, og det kan fordeles over de 4 CPU'ene som er tilgjengelig.
    30*6 / 4 = 45 min

    

## Oppgave 9

    Det er nødvendig å serialisere prosesser om de kan aksessere en felles variables samtidig. OS kan gjøre en context-switch når som helst og da kan en prosess bli satt på vent mens en annen prosess får kjøre. Et sted i koden hvor det er nødvendig at en prosess kan utføre hele kodebiten før en annen prosess aksesserer koden kalles et kritisk avsnitt. Det kan gjøres med en MuteX lås der den ene prosessen blir låst ute fra den kodebiten når den andre prosessen bruker den.

    Et eksempel kan være en nettbutikk, hvor systemet holder oversikt på hvor mange eksemplarer det er igjen av et produkt. Om to brukere bestiller et produkt samtidig, men det bare er en igjen, og bestillingene håndteres gjennom 2 forskjellige tråder, kan dette skape en race condition. Det vil si at når bestillingen blir gjort, og systemet leser av at det finnes et eksemplar igjen, mens den andre prosessen holder på å skrive at det ikke finnes noe igjen, så vil begge bestillingene gå gjennom, men det finnes bare et eksemplar. 
    Om den ene bestillingen ikke fikk lov til å lese inventaret mens den andre brukte det, så kunne dette vært unngått. 



## Oppgave 10

    Kritisk avsnitt er del av koden som må få kjøre uten at det blir berørt av andre prosseser samtidig. Det kan være når det skal endres på en felles variabel.

## Oppgave 11

    Scriptet leser av en fil fra pathen ""/home/haugerud/teller", og legger innholdet i variabelen nr.
    Så inkrementeres nr, før vi venter i 3 sekund og overskriver inneholdet i filen med den nye nr verdien. 
    
    Når skriptet da kjøres flere ganger, vil det stige med en hver gang, siden resultatet blir oppdatert i filen vi først leser inn i skriptet.

## Oppgave 12

    Prosessene rekker ikke å skrive tilbake til filen før de leses av, så begge to vil først lese av en tom fil (0), også legge tilbake 1.

    Om man hadde kjørt enda en instans av scriptet etter disse er ferdig ville den fått 2 som svar.

## Oppgave 13

    Her brukes det en MuteX lock som gjør at prosessen låser CPUen, slik at den andre prosessen ikke får lov til å lese filen mens den selv kjører.
    Det skjer ved at det lages en skjult fil kalt ".lock" av første prosess, og når andre prosess starter, så vil den sitte fast i while løkken, som kjøres så lenge det finnes en fil kalt ".lock". 
    Når den første er ferdig, så avslutter den med å slette ".lock" filen, og da frigjør prosess nummer 2.

## Oppgave 14

    Her startes de helt likt, og derfor begge to forbi while løkken før en ".lock" fil er laget. Da vil ingen av de låses, og de vil gjennomføre prosessen samtidig.

    Det kan løses ved at while-løkken flyttes til en metode (eller flytte løkken til etter låsen er laget), som blir kallet på etter at filen er laget. Da kan vi garantere at den finnes for en prosessene, når det kalles på while-løkken.

    Da må låsen også ha en id, som f.eks PID til tråden som lager låsen.
    Da må while-løkken endres på til at den ikke kjøres med låsen på tråden som laget den, slik at den ikke stopper seg selv, men låser seg for de andre. 

## Oppgave 15

    Mappen over den du står i.

## Oppgave 16

    /usr/bin/diff

## Oppgave 17

    regn > res.txt

## Oppgave 18

    *

## Oppgave 19

    $ echo $prefixfase - Feiler fordi du prøver å hente variabelen "prefixfase", som ikke finnes.

    $ echo $(prefix)fase - Feiler fordi du prøver å kjøre en kommando kalt prefix, som ikke finnes
    
    $ echo $prefix fase - Mellomrommet gjør at det blir en variabel og et ord skrevet hver for seg
     
    $ echo $prefix\fase - Man kan bruke \ for skille mellom variabelnavnet og teksten, uten mellomrom.

## Oppgave 20

```bash
#! /bin/bash
for fil in $(ls); do
    filnavn=$(basename $fil)
    bokstav=$(echo ${filnavn:0:1} | '{print tolower($0)}')
    dir=$bokstav\dir
    mkdir $dir
    mv $fil $dir 
done
```

## Oppgave 21

    Remove-Item - rm
    Get-Process - ps
    Stop-Process - kill
    Set-Location - mv
    Copy-Item - cp
    Get-Location - pwd
    Move-Item - mv
    Get-Content - cat


## Oppgave 22

```powershell
foreach($fil in ls -r "C:\" 2>$null) {
    if (($fil.Extension -eq ".ps1")) {
        $totalBytes+=$fil.Length
    }
}
echo $totalBytes
```
 
## Oppgave 23

    Den  prinsippielle betydningen er at det skal like lang tid å aksessere hvilken som helst byte, hvor som helst i minnet.

    I en server er det ofte store mengder internminne, og da vil den fysiske avstanden til CPUen være forskjellige for ulike deler av RAM'en. Det vil derfor være noe data som vil ta lenger å hente ut enn andre, fordi dataen må fysisk reise lenger.

## Oppgave 24

    Pages

## Oppgave 25

    Paritets bit
