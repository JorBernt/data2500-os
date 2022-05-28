## Oppgave 1a

    move: command not found

## Oppgave 1b

    ssh os3.vlab.cs.hioa.no hostname

## Oppgave 1c

    Output fra cat omdirigeres til /dev/null og forsvinner

## Oppgave 1d

    sort -k 2 biler

## Oppgave 1e

    grep name index.html | head -n 5 | cut -d\" -f 2

## Oppgave 2

```bash
#! /bin/bash

write_output () {
    echo "#### $1 ####"
}

while [ 1 ]
do
    echo -n dsh$
    read command
    if [[ $command == "exit" ]]
    then
        exit
    fi
    write_output $(hostname)
    eval $command
    for ssh in $(cat ./hosts)
    do
        write_output $ssh
        ssh $ssh $command
    done
done
```

```bash
#!/bin/bash

while[ 1 ]
do
    command=$(read)
    if [[ $command == "exit" ]];then
        echo Avslutter dsh
        exit 1
    fi
    for dest in $(cat ./hosts)
    do
        echo "#### $dest ####"
        ssh $dest $command
    done
done
```

## Oppgave 3a

    bash
    Java bytecode
    PowerShell
    C
    Assembly

## Oppgave 3b

    Maskinkode

## Oppgave 3c

    Assembly

## Oppgave 3d

    $gcc svar.c
    $./a.out

    Output blir:
    "Svar = 41"
    "Kaller enlinje()..."
    "Svar = 42"

## Oppgave 3e

    $gcc -c svar.c -o svar
    Kompilerer svar.c til en kjørbar fil som heter svar, uten å linke programmet.
    $gcc -c en.c -o en
    Kompilerer en.c til en kjørbar fil som heter en.out, uten å linke programmet.
    $gcc svar en -o run
    Linker svar og en, og lager en ny kompilert fil, slik at svar.c kan kalle på funksjonen i en.c, og variabelen svar er linket.

    Enlinje.c henter den externe variabelen svar, som vil si at den leser fra den samme adressen til svar som svar.c gjør.
    Når den da øker denne verdien, vil da svar.c også lese denne nye oppdaterte verdien.

## Oppgave 3f

    Dette er assembly koden for dette C-programemt.

    movl svar(%rip), %eax - leser variabelen svar fra minne til ax registeret
    addl $1, %eax - Øker verdien i registeret $eax med 1
    movl %eax, svar(%rip) - Flytter verdien i $eax tilbake til variabelen svar i internminnet.

## Oppgave 3g

    void enlinje()
    {
    extern int svar;
    svar++;
    }

    Det finnes en egen assemblyinstruksjon, incl, som utfører inkrementering av variabelen.

## Oppgave 4a

    Det opprettes 2 tråder, som begge to skal kjøre metoden inc(). De startes og utfører inc() metoden, også joines tilbake igjen.
    Siden de ikke er synkronisert, vil dette kune skape race-conditions.

## Oppgave 4b

    Siden trådene ikke er synkronisert, så vil en tråd kunne lese av svar variabelen, mens den andre prøver å skrive til den.
    Dette er en race-condition, og vil føre til at endringer vil gå tapt.

## Oppgave 4c

    Begge trådene vil få delt kjøretid om hverandre, som byttes på.
    Når en tråd har lest verdien fra minne, så kan den da bli stoppet og det gjøres en context switch til den andre tråden, før den er ferdig med å skrive. Dvs. det samme problemet som i forrige oppgave. Men siden gjøres færre context-switcher på samme cpu, så er det mindre sannsynlig at det vil skje, og derfor blir resultatet av og til riktig.

    Siden de to trådene her må dele på en cpu, så vil de kun kjøre en om gangen. Da er det mindre sannsynlighet for at en tråd blir stoppet mens den leser/skriver til minne, og det gjøres en context switch, og det blir en race condition.
    I forrige oppgave vil kjøre parallellt, og derfor vil dette problemet oppstå mye oftere.

## Oppgave 4d

    Dette er fordi det nå er bare en instruks som både leser, øker og skriver tilbake igjen, i steden for 3 som i forrige oppgave. Derfor er det ikke mulig for at det skjer en context-switch før variabelen er økt og skrevet tilbake igjen til minne når det kjøres på en cpu.

## Oppgave 4e

    Det er fordi det nå kjøres i parallell mellom flere CPUer, og derfor kan instruksjonen utføres helt samtidig. Da vil begge to lese samme verdi, øke de med en, og overskrive hverandre. Det skulle ha blitt økt med 2 til sammen, og vi mister den ene økningen. Som resultatet viser, så skjer det ca. hver gang instruksjonen utføres, siden resultatet er ca. halvparten av det det skal være.

## Oppgave 4f

    Instruksjonene er de samme, bare at det nå er introdusert en lock instruksjon før den kritiske linjen incl utføres.
    Lock låser minnebussen, slik at instruksjoner ikke kan hente eller lagre noe i ram samtidig. Da vil den ene tråden kunne utføre inkrementeringen, uten at den andre tråden kan gjøre.
    Det vil da føre til at de ikke vil overskrive hverande, og resultatet blir korrekt.

## Oppgave 4g

    Denne metoden sørger for serialisering ved at det lages en "lås", som er en while løkke som kjører så lenge låsen er true.
    Når første tråd kaller på låsen, går den forbi løkken, men setter låsen til true. Når da tråd 2 kommer til låsen, vil den da sitte fast i denne while løkken (busy-waiting).
    Den sitter da fast der, til tråd 1 er ferdig med det kritiske avsnittet, og setter låsen til false igjen. Da kan tråd 2 fortsette til det kritiske avsnittet.


    Om tråd 1 blir stoppet etter while-løkken, men før den setter lock til true, og det blir gjort en switch til tråd 2, slik at tråd 2 kommer til while-løkken, som da ikke er satt til true og den vil gå rett forbi, så vil da begge trådene ha kommet forbi låsen, uten å ha blitt låst. Da vil begge to gå inn i det kritiske avsnittet samtidig, og skape race-conditions.

## Oppgave 5a

    ls | Get-Member

## Oppgave 5b

    $(Get-Date) - (ls)[0].CreationTime | select TotalDays
    ($(Get-Date) - (ls)[0].CreationTime).TotalDays
    ($(Get-Date) - (ls fil.txt).CreationTime).TotalDays

## Oppgave 5c

```powershell
foreach($fil in ls) {
    $alder=(Get-Date) - $fil.CreationTime
    $total+=$alder.TotalDays
    $antallFiler++
}
echo "Snitt-alder $($total/$antallFiler) dager for $antallFiler filer og mapper"
```
