# Eksamen 2017 Høst

## Oppgave 1

    pwd

## Oppgave 2

    ps

## Oppgave 3

    Lag link - ln
    Skriv til
    stdout - cat
    Lag
    mappe - mkdir
    Kopier - cp
    Flytt - mv
    Endre
    rettigheter - chmod
    List
    innhold i
    mappe - ls
    Slett/fjern - rm

## Oppgave 2a

    ping -i 5 www.hin.no

## Oppgave 2b

    ping -c 1 www.hin.no

## Oppgave 2c

    ping -t 1 www.hin.no

## Oppgave 2d

    ping -t 1 -c 1 www.hin.no | head -2 | tail -1
    ping -t 1 -c 1 www.hin.no | grep "Time to live"

## Oppgave 2e

    ping -t 2 -c 1 www.hin.no | head -2 | tail -1
    ping -t 2 -c 1 www.hin.no | grep "Time to live"

## Oppgave 2f

```bash
#! /bin/bash
for (( i=1;; i++ ))
do
    response=$(ping -t $i -c 1 $1 | grep "Time to live")
    if [ "$response" ]
    then
        echo $i $response
    else
        echo "Det er $((($i-1))) rutere på vei til $1"
        break
    fi
done
```

```bash
#!/bin/bash

number=1
while [ True ]
do
        loc=$(ping -t $number -c 1 $1 | grep "Time to live")
        if [[ "$loc" != ""  ]]; then
                echo "$number $loc"
        fi
        if [[ "$loc" == "" ]]; then
                echo "Det er $((($number-1))) rutere på vei dit"
                break;
        fi
        ((number=number+1))
done

```

## Oppgave 3a

    $gcc add.c
    $./a.out

## Oppgave 3b

    "Resultat: 42"

## Oppgave 3c

    movl $13, -8(%rbp) | Legger til tallet 13 til register -8(%rbp)
    movl $29, -4(%rbp) | Legger til tallet 29 til register -4(%rbp)
    movl -4(%rbp), %eax | Flytter tallet fra register -4(%rpb) til %eax
    addl %eax, -8(%rbp) | Legger sammen registere %eax og -8(%rbp). Resultatet blir liggende i -8(%rbp)

    Resultatet blir 42

## Oppgave 3d

    movl -4(%rbp), %eax
    addl %eax, -8(%rbp)

    Det er ikke gitt at en C-instruksjon leder til bare en assembly instruksjon. Det blir ofte flere instruksjoner, slik som vist over.
    En assembly-instruksjon kan også bli til flere maskin-instruksjoner.

## Oppgave 3e

    Opsjonen -O er for å kjøre kompilatoren med optimalisering på. Den vil da analysere koden som skal kompileres, og prøve lage så kompakt og rask assembly som mulig. Den ser at det er to statiske verdier som skal legges sammen, og precomputer hele addisjonsleddet og skriver resultatet direkte til registeret.

## Oppgave 4a

    Kode som må fullføres uten at andre prosesser bruker samme felles ressurs

## Oppgave 4b

    At OS skifter prosess som bruker CPU'en

## Oppgave 4c

    I et multitasking operatisystem vil OS'et gjøre konstante context switcher, hvor den hopper mellom hvilken del av prosessen som kjører.
    Det vil da være mulig for deler av prosessen til å aksessere felles data, samtidig som en annen del prøver å f.eks skrive til denne dataen. Dette kan skape race conditions. Derfor er det viktig at prosessen er serialisert, så OS'et vet når det kan gjøre en switch, og når det ikke må gjøres. Det er opp til brukeren å serialisere sine prosesser.

## Oppgave 4d

    movl $13, -8(%rbp)
    movl $29, -4(%rbp)
    movl -4(%rbp), %eax
    addl %eax, -8(%rbp)

    Om vi ser på de to siste linjene i assembly koden fra "C og Assembly" oppgaven, så leses verdi fra variabelen tall på nest linje, før den legges til felles på siste. Om det da skjer en context switch etter at tall er lest, men før den legges til felles, og kodelinjen
    "felles = felles - tall;" kjøres, vil det bli feil verdi av felles som lagres.

    Anta at operativsystemet switcher fra T0 til T1 etter at T0 har lastet verdiene
    av felles og tall inn i hvert sitt register og T1 gjør sin oppdatering i timeslicen den har fått. Når T0
    så får lov til å fortsette vil den legge sammen de to tallene den opprinnelig hadde lastet inn i registerne og

legge resultatet ut i felles. Dermed vil T1 sin oppdatering være forsvunnet.

## Oppgave 4e

    Om prosessene har en lock som settes når den kritiske linjen kjøres,
    så kan ikke det ikke skje en context switch så lenge denne kodebiten kjøres. Da vil de ikke kunne aksessere den felles variabelen samtidig.

```C
Get_Mutex(lock);
felles = felles + tall;
Release_Mutex(lock);

Get_Mutex(lock);
felles = felles - tall;
Release_Mutex(lock);
```

## Oppgave 4f

    I følgende eksempelkode:
    Get_Mutex(tid)
    felles = felles + tall
    Release_Mutex(tid)

    vil tråd første gang tråd nummer 0 få tilgang til koden først, fordi tråd 1 vil bli låst fast i while loopen i Get_Mutex.

## Oppgave 5a

## Oppgave 5b

## Oppgave 5c

## Oppgave 5d

## Oppgave 6a

## Oppgave 6b

## Oppgave 6c

## Oppgave 6d
