# Uke 2

## Introduksjon til Operativsystemer

Definisjon på et OS:

- A: Gi applikasjonsprogrammer og brukere enhetlig, enklere og mer abstrakt adgang til maskinens ressurser
- B: Administrere ressursene slik at prosesser og brukere ikke ødelegger for hverandre når de skal aksessere samme ressurser.

<p align="center">
    <img src="images\prinsippSkisseLinux.png" style="width: auto;" alt="">
    Prinsippskisse av Linux
</p>

Definisjon av prosess:
Alternative definisjoner:

1. Et program som kjører
2. Arbeidsoppgavene en prosessor gjør på et program
3. 1. Et kjørbart program
   2. Programmets data (variabler, filer, etc.)
   3. OS-kontekst (tilstand, prioritet, prosessor-registre, etc.)
4. Et programs ånd/sjel

   I en analogi hvor programmet som kjører er et menneskes DNA, vil prosessen være hele livet et menneske lever:

   **Program = DNA**<br>
   **Prosess = livet**<br>
   **Hardware = Organer/Universet/hus/mat/bygninger**<br>
   **OS = staten/lovverket**<br>
   **kill, Ctrl-C = drap**<br>
   **root/Administrator = Gud**
   **CPU = Hjerne**<br>
   **kriminalitet = Black hat hacking**

---

<br><br>

## Datamaskinarkitektur

### Logiske porter og Binær logikk

**AND:** Om begge signalene er 1, vil resultatet bli 1.<br>
**OR:** Om en eller begge signalene er 1, vil resultatet bli 1<br>
**NOT:** Signalet blir det motsatte.

<br>

AND:

| A   | B   | A $\cdot$ B |
| --- | --- | ----------- |
| 0   | 0   | 0           |
| 0   | 1   | 0           |
| 1   | 0   | 0           |
| 1   | 1   | 1           |

<p >
    <img src="images\AndGate.png" style="width: auto;" alt="">
    <br>And Gate
</p>

<br>

OR:

| A   | B   | A + B |
| --- | --- | ----- |
| 0   | 0   | 0     |
| 0   | 1   | 1     |
| 1   | 0   | 1     |
| 1   | 1   | 1     |

<p>
    <img src="images\OrGate.png" style="width: auto;" alt="">
    <br>OR Gate
</p>

<br>

NOT:

| A   | A not |
| --- | ----- |
| 0   | 1     |
| 1   | 0     |

<p>
    <img src="images\NOT.png" style="width: auto;" alt="">
    <br>NOT Gate
</p>

# Uke 3

## Transistorer, porter og krets som adderer tall

## Moore's Law

Moore's Lov sier at antall transistorer i integrerte kretser dobler seg annenhvert år.

## CMOS

**En teknologi for å lage kretser. Satt sammen av NMOS og PMOS**

## NMOS

**NMOS er en transistor. Ingen spenning inn, øvre og nedre del er isolert(bryter av)**

<p >
    <img src="images\nmos.svg" style="width: auto;" alt="">
    <br>And Gate
</p>

## PMOS

**PMOS er en transistor. Virker motsatt av NMOS. Når det er spenning inn, er øvre og nedre del isolert(bryter er av)**

<p >
    <img src="images\pmos.svg" style="width: auto;" alt="">
    <br>And Gate
</p>

**Man kan lage alle mulige logiske operasjoner bygget på transistorer ved å sette sammen systemer av NOT, AND og OR-porter.**

## Boolsk algebra

## I boolsk algebra uttrykkes AND, OR og NOT på følgende måte

- AND: A $\cdot$ B (A $\land$ B )<br>
- OR: A + B (A $\lor$ B)<br>
- NOT: $\overline{A}$ ($\lnot $ A )

### Eksempel på en logisk krets.

En krets hvor resultatet skal bli 1 når A og B er like.

$F(A,B) = A \cdot B + \overline {A}\cdot \overline {B} $. <br>

<p align="center">
    <img src="images\logiskKrets.png" style="width: auto;" alt="">
    <br>Tegning av den logiske kretsen.
</p>

Sannhetstabell av den logiske kretsen over<br>
| A | B | A $\cdot$ B |
|---|---|-------|
| 0 | 0 | 1 |
| 1 | 0 | 0 |
| 0 | 1 | 0 |
| 1 | 1 | 1 |

## Forenkling av logiske uttrykk.

$\displaystyle F(A,B) = \overline{A}\cdot B + A \cdot B = ( \overline{A} + A) \cdot B = 1 \cdot B = B
$

Her har vi brukt at at $\overline{A} + A = 1$ som gjelder kun for Boolsk algebre.

| A   | B   | F (A,B) |
| --- | --- | ------- |
| 0   | 0   | 0       |
| 0   | 1   | 1       |
| 1   | 0   | 0       |
| 1   | 1   | 1       |

## Hvordan kan man få en logisk krets til å addere?

<p align="center">
    <img src="images/fulladder.png" style="width: auto;" alt="">
    <br>Full Adder.
</p>

<p align="center">
    <img src="images\full_adder_krets.png" style="width: auto;" alt="">
    <br>Full Adder krets.
</p>

//TODO

---

# Uke 4

## Vipper og registre, CPU-arkitektur.

## ALU: Arithmetic Logic Unit

ALU er den delen av en CPU som utfører artimetiske operasjoner:

- Adder
- Inkrement (++)
- Dekrement ($- -$)
- Multipliser
- Divider
- Shift (flytt alle bit i en retning)
- Sammenligne
- AND, OR, NOT, XOR

### Kontrollbits

Hvilken operasjon ALU'en skal utføre kontrolleres ved bruk av kontroll-bits som gis forskjellige verdier.

## Vipper og registre

Vipper er den grunnleggende lagringsenheten i CPU og bruker til lagring i CPU'en sin cache samt cache mellom CPU og RAM.

For å lage en lagerplass som hurtig kan leses å endres må vi bruke logiske porter. Av slike porter kan man lage en lagerenhet som kan lagre nuller og enere og disse kalles vipper.

## D-lås (D-latch)

En D-lås er en lagringskrets som brukes for å lagre én bit. I bildet under er det verdien D sender inn i kretsen som er verdien som lagres, og C brukes som en lås/kontroll-signal. Når C = 1 vil den nye verdien lagres. Om C = 0 vil verdien i kretsen forbli som den er.

<p align="center">
    <img src="images\dlatch.svg" style="width: auto;" alt="">
    <br>En D-lås som lagrer én bit.
</p>

## Shift-register

For å kunne kontrollere flyten av data, og forsikre seg om at alle d-låsene leser og sender til riktig tid, kan man bruke en klokke som går på ca 1-3GHz. Denne klokken sender signaler med et kort mellomrom, og verdiene vil kun oppdatere seg når de mottar et slikt signal.

<p align="center">
    <img src="images\d-vippe.svg" style="width: auto;" alt="">
    <br>D-vippe av 4 D-låser.
</p>

# CPU-arkitektur

<p align="center">
    <img src="images\cpu_arkitektur.jpg" style="width: auto;" alt="">
    <br>CPU Arkitektur
</p>

# Von Neumann -arkitekturen

Den vanligste CPU-arkitekturen som brukes i dag er von Neumann arkitekturen. En negativ ting med denne arkitekturen, kjent som "the von Neumann bottleneck", er at både instruksjoner og data deler samme data-buss.

# Harvard arkitekturen

Harvard-arkitekturen har løst dette problemet med å ha to fysisk separerte data-busser. De som bruker Harvard-arkitekturen bruker også ofte en modifisert hardvard-arkitektur.

- Et arbeidsminne (internminnet/RAM) som inneholder både instruksjoner og kode.
- En aritmetisk/logisk enhet (ALU - Arithmetic Logic Unit) som kan utføre matematiske og logiske operasjoner.
- En kontrollenhet som henter inn instruksjoner fra RAM, dekoder dem og sender signaler som gjør at instruksjonen blir utført.
- Registre, internlager for både instruksjoner og data inne i CPU-en.
- Enheter for input og output som gjør at CPU kan kommunisere med harddisk, tastatur, nettverk, etc.

## Beregningsenheter

- ALU (Arithmetic Logic Unit) CPU-ens hjerne
- CPU (Central Processing Unit)
- FPU (Floating-Point Unit) vanligvis integrert i CPU
- GPU (Graphics Processing Unit) tusenvis av cores
- FPGA (Field-programmable Gate Array) programmerbar logikk
- ASIC (Application-Specific Integrated Circuit)

## Fra høynivåkode til CPU-beregning

All høynivå-kode oversettes til maskinkode av en kompilator eller liknende.

## Branch control

Branch control tillater en CPU å utføre instruksjoner som if, for og while.

# Uke5

## C, maskinkode og assembly

https://www.eecg.utoronto.ca/~amza/www.mindsec.com/files/x86regs.html

// TODO

# Uke 6

## Pipelining

Det er vanlig å dele opp instruksjoner i flere steg (stages), der en instruksjon kan begynne på sitt første steg så snart den forrige instruksjonen er ferdig med det steget. De kan altså kjøre samtidig, med bare ett stegs mellomrom.

# Uke 7

## Branch prediction, Multitasking

## Branch prediction

Med branch prediction er målet å gjette hva som er neste branch. Om man gjetter riktig kan man spare tid, men det må også gjøres om hvis man gjettet feil.

Branch prediction er et stort problem for piplining, må vente på resultat fra forrige instruksjon.

## Meltdown

Sikkerhetshull i hardware funnet i 2018. Meltdown utnytter at både koden som sjekker om prosessen kan lese fra RAM og lesingen fra RAM delvis utføres. Meltdown kan da lese data fra andre prosesser som er cachet med enda ikke fjernet pga feil branch.

### Interrupts

Et interrupt er et signal fra hardware. Når CPU'en får en interrupt vil den avbryte det den gjør for å håndtere signalet. Adressen til neste instruksjon blir lagret på stack så den kan fortsette etter interrupt-signalet er behandlet. Det finnes flere forskjellige interrupt-signaler med sine egne rutiner. De har forskjellige interrupt-nr (IRQ).

## Singletasking OS

Basis for flerprosess-systemer.

<p align="center">
    <img src="images\internminnekart.png" style="width: auto;" alt="">
    <br>Internminnekart for singeltasking
</p>

## Multitasking OS

**_For å lage et system som kan kjøre n programmer samtidig, må vi få en enprosess maskin til å se ut som n maskiner._**

**_Bruker software til å fordele tid mellom n programmer og å dele ressurser; minne, disk, skjerm etc. OS-kjernen utfører denne oppgaven._**

Samtidige prosesser må tildeles hver sin del av minne:

<p align="center">
    <img src="images\internminnekartMulti.png" style="width: auto;" alt="">
    <br>Internminnekart for multitasking
</p>

## Multitasking

Får det til å se ut som at flere prosesser kjøres samtidig men i prinsippet er det en og en prosess som får litt cpu tid hver. Alle prosessene legges i et køsystem kalt Round Robin. En hardware timer slås inn hvert hundre dels sekund og lagrer alt fra prosessen som kjøres og bytter til neste prosess i listen. Dette bytte kalles context switch.

## PCB - Process control block

- CPU registre
- pekere til stack
- prosesstilstand (sleep, run, ready, wait, new, stopped)
- navn (PID)
- eier (bruker)
- prioritet (styrer hvor mye CPU-tid den får)
- parent prosess
- ressurser (åpne filer, etc.)

## Timesharing og Context Switch

CPU-scheduling = å fordele CPU-tid mellom prosessene = Time Sharing

OS sender interrupt = CPU lagrer alt fra prosessen som kjører = OS lar neste prosess i Round Robin få CPU tid = Context Switch

# Uke 8

## Multitasking, cahce, hyperthreading
