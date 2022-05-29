# Eksamen - Vår -2017

1a) Forklar hva som menes med PID

    PID er Process ID, som er en unik id som hver prosess i et OS får når den lages.

1b) Forklar kort hva et systemkall er.

    Når en prosess som kjører i brukermodus trenger tilgang til priviligert minne, så har OS flere systemkall, som er et API mellom kernel og userspace, som kan hjelpe til med dette. Dette kan f.eks være å få tilgang til filsystemet. Systemkall ligger i predefinerte områder i minnet, hvor det ikke er mulig for userspace å kjøre kode.

1c) Du utfører Linux-kommandoen ls /etc/passwd. Forklar kort om dette vil medføre at det utføres systemkall og
isåfall hvorfor dette er nødvendig.

    Dette vil medføre systemkallet readdir. Dette er nødvendig for å lese innholdet i mappen/directory.

1d) Om man kopierer et C-program kompilert på en x86-basert Linux maskin til en x86-basert Mac OS X, vil da
programmet kunne kjøre? Forklar kort.

    Nei, dette vil ikke fungere da maskininstruksjonene vil være forskjellig.

1e) Anta at man kompilerer et Java-program på en x86-basert Linux maskin slik at man får en Java class-fil. Om man
kopierer class-filen til en x86-basert Windows 10 PC, vil da programmet kunne kjøre? Er det noen forutsetninger
utover det som operativsystemet bidrar med som må være på plass for at programmet skal kunne kjøre? Forklar
kort.

    JVM = Java Virtuell Machine. Siden Java kompieres i java byte code og kjøres igjennom JVM så vil dette fungere. OBS: Hvis java koden blir kompilert i en nyere java versjon og flyttes til en maskin med eldre java så vil ikke dette fungere da jvm ikke er bakoverkompatibelt. Forutsetning er at java er installert på maskinene.

1f) En prosess bruker ca 8 minutter på å beregne et CPU-intensivt regnestykke. Hvis to slike prosesser kjører
samtidig på et multitasking OS med én CPU, hvor lang tid vil det omtrent ta? Forklar kort.

    16 min. I et multitaskin OS så er det fremdeles en ALU per core og hvis da dette OS`et har en CPU/core så vil det kun være en ALU tilgjengelig og begge prosessene må dele på denne. Dermed vil det ta dobbelt så lang tid hvis man kjører 2 prosesser. Dette er fordi dette programmet er CPU intensivt og må bruke ALU hele tiden.

1g) Hvorfor kan ikke et OS generelt sett utnytte en dual core CPU ved å la en vanlig sekvensiell prosess kjøre på to
CPUer? Forklar kort.

    Fordi i en sekvensiell prosess, så er neste operasjon avhenging av forrige, og derfor må begge kjernene vente på forrige operasjon. Da er det ikke mulig for kjernene å regne andre deler av sekvensen.
    Det måtte eventuelt vert opp til programmeren til å skrive parallellisert kode, om mulig.

1h) En sekvensiell 100% CPU-intensiv regnejobb bruker 6 minutter på en dual core CPU. Hvor lang tid tar det hvis 7
slike program startes samtidig på samme maskin? Forklar kort.

    6 * 7 / 2 = 21. En prosess trenger 6 minutter cpu tid. Hvis 7 kjøres vil de fordeles likt på 2 cores. Defor regnestykket over.

# Linux kommandolinje

2a) I de følgende deloppgavene skal vi først studere noen Linux-kommandoer som til slutt skal settes sammen til en
lang Linux-kommando som viser hvilke fem ord Shakespeare brukte oftest i sine samlede verker.
Forklar utifra følgende eksempel hva kommandoen head -n 2 gjør:

```bash $ cat num.txt
30 to
20 en
200 tre
$ head -n 2 num.txt
30 to
20 en
```

    Head betyr fra start, og opsjon -n 2 betyr at det skal vises de 2 første linjene fra start i tekstfilen.

2b)Vi bruker så kommandoen sort på den samme filen num.txt. Forklar utifra følgende eksempel hva opsjonene
n og r betyr for kommandoen sort:

```bash
$ sort num.txt
200 tre
20 en
30 to
$ sort -n num.txt
20 en
30 to
200 tre
$ sort -nr num.txt
200 tre
30 to
20 en
```

    sort er alfabetisk
    sort -n er nummerisk
    sort -nr er nummerisk reversert.

2c) Studer manualsiden for kommandoen uniq:

```bash
NAME
uniq - remove duplicate lines from a sorted file
SYNOPSIS
uniq [OPTION]... [INPUT [OUTPUT]]
DESCRIPTION
Discard all but one of successive identical lines from INPUT (or
standard input), writing to OUTPUT (or standard output).
-c, --count
prefix lines by the number of occurrences
-d, --repeated
only print duplicate lines
-D, --all-repeated
only print all duplicate lines
-f, --skip-fields=N
avoid comparing the first N fields
-t, --separator=SEP
use SEParator to delimit fields
-u, --unique
only print unique lines
-W, --check-fields=N
compare no more than N fields in lines
```

Gitt at du har følgende fil med navn test.txt
to
en
en
to
to
Angi hvordan du kan bruke uniq med opsjoner på filen test.txt slik at output blir
1 to
2 en
2 to

    uniq -c test.txt

2d)Lag så en sammensatt kommando med sort og uniq og opsjoner, slik at du får en numerisk sortert liste over
antall ganger ord forekommer i filen test.txt:

    $ cat test.txt | DIN KOMMANDO
    3 to
    2 en

Angi hva som må stå istedet for DIN KOMMANDO.

    cat test.txt | sort -r | uniq -c

2e)Anta du står i en katalog med fire underkataloger som inneholder tekstversjonen av alle Shakespeares verker og
som ser slik ut når du lister dem:

    $ ls -l
    totalt 4
    drwx------ 2 haugerud drift 512 2016-11-21 15:32 comedies
    drwx------ 2 haugerud drift 512 2016-11-21 15:32 histories
    drwx------ 2 haugerud drift 512 2016-11-21 15:32 poetry
    drwx------ 2 haugerud drift 512 2016-11-21 15:32 tragedies
    $ ls -l poetry/
    totalt 265
    -rw------- 1 haugerud drift 14366 2016-08-29 07:45 loverscomplaint
    -rw------- 1 haugerud drift 84700 2016-08-29 07:46 rapeoflucrece
    -rw------- 1 haugerud drift 95662 2016-08-29 07:43 sonnets
    -rw------- 1 haugerud drift 18954 2016-08-29 07:46 various
    -rw------- 1 haugerud drift 54390 2016-08-29 07:46 venusandadonis

Tilsvarende inneholder de tre andre underkatalogene tekstfiler med de andre verkene. Gi en Linux-kommando
som legger alle disse tekstfilene etter hverandre i samme tekstfil med navn /tmp/alle.txt.

    cat */* >> /tmp/alle.txt

    find . -type f -exec cat {} \; > /tmp/alle.txt

2f) Linux-kommandoen tr leser fra standard input og kan brukes til å skifte ut tegn i tekster. Følgende
kommando bytter ut alle sekvenser av tegn som ikke er bokstaver med ett linjeskift:

    $ echo "Hei, ja og Hallo dere..." | tr -cs A-Za-z '\n'
    Hei
    ja
    og
    Hallo
    dere

Dermed overføres en setning til ord fordelt linje for linje. Kommandoen tr kan også brukes til å bytte store bokstaver med små

    $ echo "HEisaNN" | tr A-Z a-z
    heisann

Lag en sammensatt kommando som gjør begge deler ved å fylle inn det som mangler i kommandoen nedenfor,
slik at resultatet blir som angitt:

    $ echo "Hei, ja og Hallo dere..." | DIN KOMMANDO
    hei
    ja
    og
    hallo
    dere

<br>

    $ echo "Hei, ja og Hallo dere..." | tr -cs A-Za-z '\n' | tr A-Z a-z

2g) Bruk det du har lært fra de tidligere deloppgavene og filen /tmp/alle.txt fra deloppgaven 2(e) til å lage en enlinjers
Linux-kommando som lager en liste over de 5 ordene som Shakespeare brukte mest når han skrev sine verker.
Output fra kommandoen skal være på formen
29854 the
27554 and
23357 i
21075 to
18520 of
eller ihvertfall inneholde samme informasjon. Resultatet betyr at Shakespeare brukte ordet "the" 29854 ganger og
"and" 27554 ganger.

```bash
cat /tmp/alle.txt | tr -cs a-zA-z '\n' | tr A-Z a-z | sort | uniq -c | sort -nr
```

# Bash-Scripting

3 Skriv et bash-script rename.sh som endrer filendelse på filer i katalogen det kjøres. Brukeren angir en filendelse
og hva den skal endres til med to argumenter. Hvis man bruker rename.sh som følger:

    $ rename.sh wav mp3
    Endrer fil.wav til fil.mp3
    Endrer fil2.wav til fil2.mp3

skal alle filer i katalogen som har filendelse wav endres til mp3. En opplysning om hver endring skal gis som i
eksempelet. Du trenger ikke å sjekke at brukeren virkelig kjører scriptet med to argumenter.
Man kan bruke kommandoen basename i scriptet om man ønsker det; to relevante eksempler er vist her:

    $ basename fil.wav .wav
    fil
    $ basename fil.12.wav .wav
    fil.12

```bash
#! /bin/bash
for fil in *.$1; do
    mv $fil $(basename $fil $1)$2;
done;
```

## Oppgave 1a

## Oppgave 1b

## Oppgave 1c

## Oppgave 1d

## Oppgave 2

## Oppgave 3a

## Oppgave 3b

## Oppgave 3c

## Oppgave 3d

## Oppgave 3e

## Oppgave 3f

## Oppgave 3g

## Oppgave 3h

## Oppgave 3i

## Oppgave 3j

## Oppgave 4a

## Oppgave 4b

## Oppgave 4c

## Oppgave 4d

## Oppgave 4e

## Oppgave 4f

## Oppgave 5a

## Oppgave 5b
