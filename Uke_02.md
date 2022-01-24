<style>

table{
    color: white;
}

#main{
    color: white;
    margin-left: 30;
    margin-right: 30;
}

#body{
    background-color: #2e2d2d;
}

#oppgaveBoks{
    border:1px; border-style:solid; border-color:#FFFFFF; padding: 1em; margin: 2em; border-radius: 10px;
}

#oppgaveTittel{
    font-size: 30px;
    margin-bottom: 20px;
    text-align: center;
}

#sporsmal{
    border:1px; border-style:solid; border-color:#FFFFFF; padding: 1em; background-color:#4a4a4a; font-size:18px; border-radius: 10px;
    margin-top: 20px; margin-bottom: 20px;
}
#outerSvar{
    border:1px; border-style:solid; border-color:#FFFFFF; padding: 1em; margin-top:1em; background-color:#3b3b3b; margin-left: 20px; margin-right: 20px; border-radius: 10px;
}
#innerEnkelSvar{
    background-color:#212121; border-radius: 10px; padding: 1em; font-size:18px;
}
#image{
    width: auto; border-radius: 10px;
    margin-top: 20px;
    margin-bottom: 20px;
}
</style>

<div id="body">

<div id="main">


<h1 style="text-align: center; font-size: 42px;">Uke 1</h1>
<div id="oppgaveBoks">
<h2 id="oppgaveTittel">Oppgave 1</h2> 
<div id="sporsmal">
<h3 style="text-align: center"> Hva er de to viktigste oppgavene til et operativsystem?</h3>
</div>
<div id="outerSvar">

<div id="innerEnkelSvar">

1. Det gir applikasjoner og brukere tilgang til datamaskinens ressurser gjennom en enhetlig, enkelt og mer abstrakt lag.
2. Den administrere ressursene til maksinen, og sørger for at prosesser og brukere ikke ødelegger for hverandre når de skal aksessere samme ressurser.

</div>
</div>
</div>

----


<div id="oppgaveBoks">
<h2 id="oppgaveTittel">Oppgave 2</h2> 
<div id="sporsmal">
<h3 style="text-align: center;"> I figuren i forelesningsnotatene er det to feil i output på høyre side, hva er galt?</h3>
</div>
<div id="outerSvar">

<div id="innerEnkelSvar">

1. Or skal være 1, siden en av inputene er det.
2. Not skal være 1, siden input er 0;

</div>
</div>
</div>

----


<div id="oppgaveBoks">
<h2 id="oppgaveTittel">Oppgave 3</h2> 
<div id="sporsmal">
<h3 style="text-align: center;"> Forklar utifra sannhetsverditabellene til AND og OR-portene hvorfor resultatet i den nederste kretsen blir 0, når øverste input er 1(rødt) og nederste input er 0(hvitt). </h3>

<div style="text-align: center;" style="padding-top: 2em">
<img src="images\oppgave-02.png" id="image">
</div>
</div>

<div id="outerSvar">

<div id="innerEnkelSvar">

Det øverste signalet går inn i en AND-gate, hvor kun 1 av inputene er 1, så derfor blir outputen 0.
Begge input-signalene må være 1 for at output skal bli 1.

</div>

</div>

<div id="sporsmal">

<h3 style="text-align: center;"> Forklar utifra sannhetsverditabellene til AND og OR-portene hvorfor resultatet i den nederste kretsen blir 0, når øverste input er 1(rødt) og nederste input er 0(hvitt). </h3>

</div>
<div id="outerSvar">

<div id="innerEnkelSvar">


| A | B | A AND B | AND OR B |
|---|---|---------|----------|
| 1 | 1 | 1       | 1        |
| 0 | 1 | 0       | 1        |
| 1 | 0 | 0       | 0        |
| 0 | 0 | 0       | 0        |


</div>

</div>

</div>

----


<div id="oppgaveBoks">
<h2 id="oppgaveTittel">Oppgave 13</h2> 
<div id="sporsmal">
<h3 style="text-align: center;"> Bruk mkdir, cp og touch til å opprette en katalogstruktur som den på figuren, der passwd er en kopi av systemets passordfil mens fil1 og fil2 er tomme filer. Katalogen ~ er din hjemmekatalog.</h3>
</div>
<div id="outerSvar">

<div id="innerEnkelSvar">

* cp /etc/passwd .
* touch fil1
* mkdir etc
* cd etc
* mkdir bin
* touch fil2

</div>
</div>
</div>

----


<div id="oppgaveBoks">
<h2 id="oppgaveTittel">Oppgave 14</h2> 
<div id="sporsmal">
<h3 style="text-align: center;"> Gi en kommando som flytter deg to kataloger oppover i filtreet.</h3>
</div>
<div id="outerSvar">

<div id="innerEnkelSvar">

cd ../../

</div>
</div>
</div>

----


<div id="oppgaveBoks">
<h2 id="oppgaveTittel">Oppgave 15</h2> 
<div id="sporsmal">
<h3 style="text-align: center;"> Lag en mappe i din brukers hjemmekatalog. Gå inn i den mappen og lag noen tomme filer med kommandoen touch filnavn. Kopier alle filer i katalogen du står i som slutter på .java til katalogen over deg. Sørg for at du har laget noen slike filer først.</h3>
</div>
<div id="outerSvar">

<div id="innerEnkelSvar">

 find . -name \*.java -exec cp {} .. \\;

</div>
</div>
</div>

----


<div id="oppgaveBoks">
<h2 id="oppgaveTittel">Oppgave 16</h2> 
<div id="sporsmal">
<h3 style="text-align: center;"> List alle filer og kataloger under /usr/bin som har filnavn som begynner på "b".</h3>
</div>
<div id="outerSvar">

<div id="innerEnkelSvar">

 find b*

</div>
</div>
</div>

----


<div id="oppgaveBoks">
<h2 id="oppgaveTittel">Oppgave 18</h2> 
<div id="sporsmal">
<h3 style="text-align: center;"> I denne oppgaven skal du lage et lite shellscript. Start en editor med

$ jed info.sh
og skriv inn

<p style="background-color:#000000; margin: 0% 40% 0% 40%; border-radius: 10px; padding: 10px">
#! /bin/bash<br>
whoami<br>
hostname <br>
uname -a
</p>

og lagre filen. Dette er et lite shellscript med navn info.sh som utfører de tre kommandoene når du kjører det. For at det skal bli kjørbart, må du sette kjørerettigheter på scriptet med
\$ chmod 700 info.sh
og du skal kunne kjøre det ved å taste inn kommandoen
\$ info.sh
Hvis det ikke går, prøv
\$ ./info.sh
<br><br>Hva er forskjellen på de to måtene å kjøre scriptet på?</h3>
</div>
<div id="outerSvar">

<div id="innerEnkelSvar">

???

</div>
</div>
</div>

----


<div id="oppgaveBoks">
<h2 id="oppgaveTittel">Oppgave 19</h2> 
<div id="sporsmal">
<h3 style="text-align: center;"> Start top i kommandolinjen og forklar hva du ser. Beskriv hvordan top er delt opp i to visuelle deler. Beskriv hva de to forskjellige delene viser og nevn de to datafeltene du mener er mest interessant i den øverste delen. For en forklaring av alle feltene, se "man top". Prøv å taste "1" i top. Hva skjer og hvilken ekstra info får du nå? (tast "1" på nytt for å gå tilbake til slik det var)</h3>
</div>
<div id="outerSvar">
<div id="innerEnkelSvar">

<p>
Øverste del viser en totaloversikt over CPU, minnebruk, antall prosesser og deres tilstand. 
Andre del viser en oversikt over alle prosesser som er i live, og diverse info om de. 

Når en trykker på "1" så vises oversikt over ressursbruk per CPU-kjerne, i stedenfor hele samlet.
</p>
</div>
</div>
</div>

<div id="oppgaveBoks">
<h2 id="oppgaveTittel">Oppgave 20</h2> 
<div id="sporsmal">
<h3 style="text-align: center;">Top har flere "hotkeys" av typen "1" som man kan bruke til å forandre hva som vises. Prøv å taste "U" i top og så ditt eget brukernavn og se hva som skjer. Ser du noe gevinst med å bruke top på denne måten? Gi eksempel på situasjoner hvor dette kan være nyttig.</h3>
</div>
<div id="outerSvar">
<div id="innerEnkelSvar">

<p>

</p>

</div>
</div>
</div>






</div>
</div>