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

## **8. (Oblig) Lag et bash-script count.bash som skriver ut en oversikt over hvor mange linker, filer og kataloger det finnes i katalogen scriptet kjøres fra og i alle dens underkataloger. Bruker du doble parenteser rundt aritmetiske uttrykk (( x++ )) kan du bruke samme syntaks som i Java (og sløyfe $ foran variabelnavn). Hint: Test kommandoene ls -R, tree -if og find . og se om noen av dem kan brukes i scriptet.**

```bash
#! /bin/bash

filer=0
mapper=0
linker=0

for fil in $(tree $1 -i -f --noreport)
do
        if [ -d $fil ]
        then
                ((mapper++))
        elif [ -f $fil ]
        then
                ((filer++))
        elif [ -l $fil]
        then
                ((linker++))
        fi
        echo Leser fil $fil
done

echo Antall filer: $filer
echo Antall mapper: $mapper
echo Antall linker: $linker
```

---

<br>
<br>

## **9. Ukens utfordring nr. 2: Lag en versjon av scriptet i spørsmål 5.7 som antar at ~/www eksisterer og gir**
1. **alle rettigheter for eier, men kun lese- og kjørerettigheter for alle andre for ~/www og alle undermapper**
2. **lese og skriverettigheter for eier, men kun leserettigheter for alle andre for alle filer i ~/www og dens undermapper**

**Filer i ~/www og undermapper som allerede har kjørerettigheter skal beholde det. Hint: Se opsjonen X til chmod i manual-siden.**

```bash
#! /bin/bash

chmod chmod u=rwx,g+rw,o+rw ~/www
for fil in $(tree ~/www/ -i -f --noreport)
do
        if [ -d $fil ]
        then
                chmod u=rwx,g+rx,o+rx $fil
        elif [ -f $fil ]
        then
                chmod u+rw,g-w+r,o-w+r $fil
        fi
done
```
---
<br>
<br>

## **10. Ukens utfordring nr. 3: Lag en versjon av scriptet i forrige spørsmål som gir rettigheter som spesifisert der, uavhengig av hvilke rettigheter de hadde fra før.**

```bash
#! /bin/bash

chmod 755 ~/www
for fil in $(tree ~/www/ -i -f --noreport)
do
        if [ -d $fil ]
        then
                chmod 755 $fil
        elif [ -f $fil ]
        then
                chmod 644 $fil
        fi
done
```
---
<br>
<br>

## **11. (Oblig) Skriv et shell-script som tar en streng som argument og skriver ut en melding som avgjør om dette er en fil og om i såfall den er angitt med absolutt eller relativ path (om en relativ path er angitt til filen, skal scriptet sjekke om den finnes relativt til der scriptet kjøres fra. Merk: hvis man gjør en test på en fil i et script, utføres testen fra den mappen som scriptet starter i.). (hint: Testen if [ -f $fil ] ; then slår til om $fil er en fil. Bruk konstruksjonen \${variabel:offset:length} for å trekke ut ett tegn fra en streng. Eventuelt cut -c 1.)**


```bash
#! /bin/bash

if [ -f $1 ]
then
        echo Er en fil
else
        echo Er ikke en fil
fi
```

---
<br>
<br>

## **12. (Oblig) Utvid scriptet i forrige oppgave slik at brukeren kan angi flere enn en fil. Gjør det ved å gå igjennom argumentene ett for ett og utføre det samme for hvert argument.**

```bash
#! /bin/bash

for fil in "$@"
do
        if [ -f $fil ]
        then
                echo $fil er en fil
        else
                echo $fil er ikke en fil
        fi
done
```
```bash
s194@os694:~/uke5$ ./isFile2.sh sr.sh count.bash publiser.sh finnesikke!
sr.sh er en fil
count.bash er en fil
publiser.sh er en fil
finnesikke! er ikke en fil
```

---
<br>
<br>

## **13. Skriv et bash-script rename som endrer filendelse på filer i katalogen det kjøres. Brukeren angir en filendelse og hva den skal endres til med to argumenter. Hvis man bruker rename som følger:**

```
$ ./rename wav mp3
Endrer fil.wav til fil.mp3
Endrer fil2.wav til fil2.mp3
```

## **skal alle filer i katalogen som har filendelse wav endres til mp3. En opplysning om hver endring skal gis som i eksempelet. Hvis brukeren ikke angir to argumenter skal scriptet avslutte og oppgi riktig syntaks. Hvis det ikke finnes filer med den filendelsen brukeren angir som første argument, skal scriptet gi en melding om det.**


```bash
#! /bin/bash

if test "$#" -ne 2; then
        echo "Illegal number of parameters"
        echo "Syntax is rename <fromExt> <toExt>"
        exit 1
fi

for f in *; do
        ext=`sed 's/^\w\+.//' <<< "$f"`
        if [ "$ext" = "$1" ]; then
                echo "Renaming $f to "${f%."$1"}."$2"
                mv -- "$f" "${f%."$1"}."$2
        fi
done
```

---

<br>
<br>


## **15. (Oblig) Lag et bash-script "finnOrd" som tar ett ord som argument og går igjennom alle filer i katalogen scriptet blir utført fra og i alle underkataloger, og finner linjer i disse filene som inneholder dette ordet. For hver fil som inneholder ordet, skal scriptet gi meldingen:**
```
########### Fant "ord" i fil "filnavn" i følgende linje(r):
```
## **Og så skrive ut alle linjene (Hint: bruk find . og grep).**

```bash
#! /bin/bash

for fil in $(find .)
do
    if [ -f $fil ]
    then
        linje=$(grep $1 $fil)
        if [ $linje ]
        then
                echo "########## Fant $1 i fil $fil i følgende linjer:"
                echo $linje
        fi
    fi
done
```
```
s194@os694:~/uke5$ ./finnOrd.sh "Hei"
########## Fant Hei i fil ./fil2 i følgende linjer:
Hei
########## Fant Hei i fil ./fil5 i følgende linjer:
Hei
```

## **16. Lag et shellscript som når det kjøres på data2500 gir omtrent tilsvarende som output:**

```
Linux data2500 4.4.0-101-generic #124-Ubuntu SMP Fri Nov 10 18:29:59 UTC 2017 x86_64 x86_64 x86_64 GNU/Linux
cpu MHz		: 2294.248
MemTotal:        8175152 kB
model name	: Common KVM processor
/etc/lsb-release:DISTRIB_CODENAME=xenial
/etc/os-release:VERSION_CODENAME=xenial
/etc/os-release:UBUNTU_CODENAME=xenial
/etc/lsb-release:DISTRIB_DESCRIPTION="Ubuntu 16.04.3 LTS"
```
## **Hint: Test ut kommandoen uname og se på innholdet i /proc/meminfo, /proc/cpuinfo og /etc/\*release.**

```bash
#! /bin/bash

uname -a
cat /proc/cpuinfo | grep "cpu MHz" -m 1
cat /proc/meminfo | grep "MemTotal"
cat /proc/cpuinfo | grep "model name" -m 1

a=("DISTRIB_CODENAME" "VERSION_CODENAME" "UBUNTU_CODENAME" "DISTRIB_DESCRIPTION")

for f in /etc/*release; do
        for i in ${!a[@]}; do
                t=$(cat $f | grep ${a[$i]})
                if test $t; then
                        echo $f $t
                fi
        done
done
```
Output:
```
s354410@data2500:~/uke5$ ./info.sh
Linux data2500 5.10.0-11-amd64 #1 SMP Debian 5.10.92-1 (2022-01-18) x86_64 GNU/Linux
cpu MHz         : 3100.000
MemTotal:        3953464 kB
model name      : Common KVM processor
/etc/os-release VERSION_CODENAME=bullseye
```