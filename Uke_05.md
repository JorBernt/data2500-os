# Uke 5

## **1. Kompiler C-programmet Hello world fra forelesningen på data2500 med gcc hello.c og kjør det med**
```
$ ./a.out
```
## **Kompiler det så med gcc hello.c -o hello. Hvordan kan du nå også kjøre programmet? Hvis du ikke har programmert i C før, kan denne C-tutorial være nyttig.**

En kan kjøre den med å skrive 

```
$ ./hello
```
---

<br>
<br>

## **2. (Oblig) Kompiler sum.c fra forelesningen sjekk at du får riktig svar. Kompiler så sammen sumMain.c og as.s fra samme forelesning med**

```bash
$ gcc sumMain.c as.s
```
## **Endre så assembly-koden as.s slik at løkken gjennomløpes en gang til og sjekk at du får svaret 10. Hva er likheten mellom koden i as.s og maskinkoden i oppgave 31 i uke 3?**

????? HVAA ???

---

<br>
<br>

## **3.(Oblig) Kopier as.s til en ny fil as2.s og endre assembly-koden slik at den utfører**
```c
S = 0;
for(i=1;i < 3;i++)
{
   S = S + 2;
}
```
## **istedet. Lag gjerne en ny versjon av sum.c også slik at du er sikker på at as2.s virker som den skal.**

```s
sum:                 # Standard

mov   $3, %rcx       # 3 -> rcx, maks i løkke
mov   $1, %rdx       # 1 -> rdx, tallet i økes med for hver runde
mov   $1, %rbx       # 0 -> rbx, variabelen i lagres i rbx
mov   $0, %rax       # 0 -> rax, summen = S

# løkke
start: # label
add  %rdx, %rbx # rbx = rbx + rdx (i++)
add  %rdx, %rax # rax = rax + rbx (S = S + i)
add  %rdx, %rax
cmp  %rcx, %rbx # compare, er i = 3?
jne  start      # Jump Not Equal til start:

ret  # Verdien i rax returneres
```
```bash
$ gcc sumMain.c as2.s -o as2
$ ./as2
$ Sum = 4
```
---

<br>
<br>

## **3.Lag en fil esum.c som ser slik ut:**
```c
int sum()
{
int S=0,i;
for(i=1; i < 4; i++)
     {
	S = S + i;
     }
return(S);
}
```
## **Kompiler den deretter sammen med sumMain.c med.**
```bash
gcc sumMain.c esum.c
```

## **og kjør programmet. Hva er likheten mellom as.s og esum.c? Kompiler så esum.c med**
```bash
gcc -S esum.c
```
as.s
```
sum:                 # Standard

mov   $4, %rcx       # 3 -> rcx, maks i løkke
mov   $1, %rdx       # 1 -> rdx, tallet i økes med for hver runde
mov   $0, %rbx       # 0 -> rbx, variabelen i lagres i rbx
mov   $0, %rax       # 0 -> rax, summen = S

# løkke
start: # label
add  %rdx, %rbx # rbx = rbx + rdx (i++)
add  %rbx, %rax # rax = rax + rbx (S = S + i)
cmp  %rcx, %rbx # compare, er i = 3?
jne  start      # Jump Not Equal til start:

ret  # Verdien i rax returneres
```
esum.c
```c
int sum()
{
int S=0,i;
for(i=1; i < 4; i++)
     {
	S = S + i;
     }
return(S);
}

```

Likhet kan være at de er strukturert likt, de definerer og initialiserer variablene med verdier først, også går gjennom løkken.
<br>
<br>

## **Hva er likeheten mellom as.s og den resulterende filen esum.s med tanke på hva de totalt sett utfører? Klarer du å se noen likheter mellom koden i esum.s og as.s? Endre koden i esum.s slik at løkken går en gang til.**

```
.LFB0:
        .cfi_startproc
        endbr64
        pushq   %rbp
        .cfi_def_cfa_offset 16
        .cfi_offset 6, -16
        movq    %rsp, %rbp
        .cfi_def_cfa_register 6
        movl    $0, -8(%rbp)
        movl    $1, -4(%rbp)
        jmp     .L2
.L3:
        movl    -4(%rbp), %eax
        addl    %eax, -8(%rbp)
        addl    $1, -4(%rbp)
.L2:
        cmpl    $4, -4(%rbp)
        jle     .L3
        movl    -8(%rbp), %eax
        popq    %rbp
        .cfi_def_cfa 7, 8
        ret
        .cfi_endproc
```
Output:
```
$ Sum = 10
```
---
<br>
<br>

## **5. Ukens utfordring nr. 1: Programmer inn en linje maskinkode i sum-programmet som ligger i DigitalWorks slik at resultatet av summen som ligger i R3 skrives til adresse 3 i RAM. Sjekk etterpå at resultatet ble lagret rett sted ved å gå inn i RAM-modulen og se. Du kan finne rikgig instruksjon i avsnittet 3.10 Løkker og branch control. Ville det være mulig å skrive til adresse 2 og 12 bare ved hjelp av de eksistrende instruksjonene?**

For å lagre i ram bruker vi store opcode (1010). Store leser av en verdi fra DR, og bruker denne til å velge hvilken adresse i ram den skal skrive til.
For å skrive i adresse 3, kan vi lese av register 0 som er 3.
Linjen er slik: 10100011

---

<br>
<br>

## **6. (Oblig)Skriv et shell-script som skriver ut verdien av den globale variabelen SHELL hvis den er satt og gir melding om at den er udefinert hvis den ikke er satt.**

```bash
#! /bin/bash

if [ $SHELL ]
then
        echo $SHELL
else
        echo Variabelen er udefinert
fi
```

```bash
s194@os694:~/uke5$ . sr.sh
/bin/bash
s194@os694:~/uke5$ unset SHELL
s194@os694:~/uke5$ . sr.sh
Variabelen er udefinert
```

---

<br>
<br>

## **7. (Oblig) Lag et bash-script med navn publiser som setter rettighetene til alle filer i ~/www slik at eier kun kan lese og skrive, mens alle andre kun kan lese dem. I tillegg skal scriptet gi tilsvarende rettigheter for alle filer i ~/www/bilder. Hvis mappene ~/www og ~/www/bilder ikke eksisterer, skal de opprettes og gis alle rettigheter for eier, men kun lese- og kjørerettigheter for alle andre. Om det finnes andre kataloger i ~/www skal disse ikke endre rettigheter, heller ikke underkataloger og filer i disse.**

```bash
#! /bin/bash

perm() {
if [ ! -e $1 ]
then
        mkdir $1
fi

chmod 744 $1

for fil in $1/*
do
        if [ -f "$fil" ]
        then
        chmod =r $fil
        fi
done
}

perm ~/www
perm ~/www/bilder
```

---
<br>
<br>