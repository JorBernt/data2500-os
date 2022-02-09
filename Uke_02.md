# Uke 2

## **2.1. Hva er de to viktigste oppgavene til et operativsystem?**

1. Det gir applikasjoner og brukere tilgang til datamaskinens ressurser gjennom en enhetlig, enkelt og mer abstrakt lag.
2. Den administrere ressursene til maskinen, og sørger for at prosesser og brukere ikke ødelegger for hverandre når de skal aksessere samme ressurser.

---

<br>
<br>

## **2.2. I figuren i forelesningsnotatene er det to feil i output på høyre side, hva er galt?**

1. Or skal være 1, siden en av inputene er det.
2. Not skal være 1, siden input er 0;

---

<br>
<br>

## **2.3.Forklar utifra sannhetsverditabellene til AND og OR-portene hvorfor resultatet i den nederste kretsen blir 0, når øverste input er 1(rødt) og nederste input er 0(hvitt).**

Det øverste signalet går inn i en AND-gate, hvor kun 1 av inputene er 1, så derfor blir outputen 0.
Begge input-signalene må være 1 for at output skal bli 1.

## **Forklar utifra sannhetsverditabellene til AND og OR-portene hvorfor resultatet i den nederste kretsen blir 0, når øverste input er 1(rødt) og nederste input er 0(hvitt).**


| A | B | A AND B | AND OR B |
|---|---|---------|----------|
| 1 | 1 | 1       | 1        |
| 0 | 1 | 0       | 1        |
| 1 | 0 | 0       | 0        |
| 0 | 0 | 0       | 0        |

---
<br>
<br>

## **2.13. Bruk mkdir, cp og touch til å opprette en katalogstruktur som den på figuren, der passwd er en kopi av systemets passordfil mens fil1 og fil2 er tomme filer. Katalogen ~ er din hjemmekatalog.**

* cp /etc/passwd .
* touch fil1
* mkdir etc
* cd etc
* mkdir bin
* touch fil2

---
<br>
<br>

## **2.14.Gi en kommando som flytter deg to kataloger oppover i filtreet.**

```
cd ../../
```

## **2.15.Lag en mappe i din brukers hjemmekatalog. Gå inn i den mappen og lag noen tomme filer med kommandoen touch filnavn. Kopier alle filer i katalogen du står i som slutter på .java til katalogen over deg. Sørg for at du har laget noen slike filer først.**

```bash
mkdir temp
cd temp
touch fil1.java fil2.java fil3.java
find . -name \*.java -exec cp {} .. \\;
```

---
<br>
<br>

## **2.16.List alle filer og kataloger under /usr/bin som har filnavn som begynner på "b".**

```
$ ls /usr/bin/b*
```

---
<br>
<br>

## **2.18.I denne oppgaven skal du lage et lite shellscript. Start en editor med**
```
$ jed info.sh
```
## **og skriv inn**
```bash
#! /bin/bash<br>
whoami<br>
hostname <br>
uname -a
```
## **og lagre filen. Dette er et lite shellscript med navn info.sh som utfører de tre kommandoene når du kjører det. For at det skal bli kjørbart, må du sette kjørerettigheter på scriptet med**
```
$ chmod 700 info.sh
```
## **og du skal kunne kjøre det ved å taste inn kommandoen**
```
$ chmod 700 info.sh
```
## **Hvis det ikke går, prøv**
```
$ chmod 700 info.sh
```
## **Hva er forskjellen på de to måtene å kjøre scriptet på?**

Den første fungerer ikke fordi den ser etter scriptet i $PATH, og den andre fungerer fordi vi spesifiserer at scriptet ligger i mappen vi er i.

---

<br>
<br>

## **2.19.Start top i kommandolinjen og forklar hva du ser. Beskriv hvordan top er delt opp i to visuelle deler. Beskriv hva de to forskjellige delene viser og nevn de to datafeltene du mener er mest interessant i den øverste delen. For en forklaring av alle feltene, se "man top". Prøv å taste "1" i top. Hva skjer og hvilken ekstra info får du nå? (tast "1" på nytt for å gå tilbake til slik det var)**

Øverste del viser en totaloversikt over CPU, minnebruk, antall prosesser og deres tilstand. 
Andre del viser en oversikt over alle prosesser som er i live, og diverse info om de. 

Når en trykker på "1" så vises oversikt over ressursbruk per CPU-kjerne, i stedenfor hele samlet.

---

<br>
<br>

## **2.20.Top har flere "hotkeys" av typen "1" som man kan bruke til å forandre hva som vises. Prøv å taste "U" i top og så ditt eget brukernavn og se hva som skjer. Ser du noe gevinst med å bruke top på denne måten? Gi eksempel på situasjoner hvor dette kan være nyttig.**

Kan være greit å kunne se hvor mange ressurser en user bruker. Hvor lenge en prosess har kjørt f eks hos en bruker. Hvor mye cpu og memory eventuelt de bruker.

## **2.21. I de neste oppgavene skal du lage ditt eget alternativ til hva du fikk til i forrige oppgave. Du skal lage et shell-script som lister opp alle prosessene til en bruker.Prøv kommandoen "ps aux". Forklar kort utskriften til den kommandoen.**

Kommandoen «ps aux» lister alle prosesser som kjører uavhengig av hvilken bruker de hører til og hvordan de ble startet.

---

<br>
<br>

## **2.22.grep er en kommando som kan plukke ut linjer som matcher en spesiell tekst. For at grep skal kunne plukke ut enkelte linjer fra ps aux, må vi lime dem sammen på et vis. Dette gjør vi med en pipe (engelsk for rør, pipe-tegnet er til venstre for 1-tasten):
```
ps aux | grep  tekst
```
## **Prøv ut den kommandoen selv og bytt ut "tekst" med noe mer fornuftig, f.eks et brukernavn. Forklar utskriften du får nå. Lag et shellscript som heter "psuser" som utfører denne kommandoen.**

```bash
#! /bin/bash
ps aux | grep <user>
```

## **2.23.Det kan være praktisk å ikke måtte endre selve koden når man vil endre litt på hvordan et script kjører. Utvid shellscriptet "psuser", slik at det kan kjøres på denne måten: ./psuser root og det da skriver ut alle linjer som inneholder teksten root. Hint: inne i scriptet vil argumentet root legges i variabelen $1. Dermed kan du erstatte teksten du vil lete etter med $1.**

```bash
#! /bin/bash
ps aux | grep $1
```

```
$ ./psuser.sh <username>
```

---

<br>
<br>