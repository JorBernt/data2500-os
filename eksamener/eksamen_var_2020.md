# Eksamen vår 2020

## Oppgave 1

    OR

## Oppgave 2

    A * B + B

## Oppgave 3

    A B RES
    0 0  0
    1 0  0
    0 1  1
    1 1  1

    Svar: B

## Oppgave 4

    En felles variabel y og en variabel x i hver thread

## Oppgave 5

    Hyperthreading

## Oppgave 6

    linux1$ gcc -O sum.c | Kompilerer C-programmet med optimalisering på.
    linux1$ time ./a.out | Kjører programmet og timer det.

    Real:1.809 User:1.804 System:0.004 99.95%
    Real: Hvor mye tid som gikk
    User: Hvor mye tid den kjørte i usermode
    System: hvor mye tid den i kjørte i kernel mode
    Prosessen gjorde 99.95% av instruksjonene på CPU i det gitte tidsrommet

## Oppgave 7

    I den første vil den kjøre programmet 4 ganger på rad, en etter en.
    I den andre vil den starte alle samtidig som bakgrunnsprosesser.

    Når du legger på en & på slutten av kommandoen, vil prosessenen starte som en bakgrunnprosess, og shellet vi er i kan fortsette videre.

    Det vil en stor forskjelli tid, om det er mer en 1 cpu. Om det er minst 4, vil det går fire ganger så raskt med den andre kommandoen.

## Oppgave 8

        Om en prosess får kjøre 100% på en CPU bruker den 1,8 sekunder. Ut ifra dette kan vi anta at serveren har fire kjerner, fordi de fire prosessen sammen også bruker 1,8 sekunder, og så tar det 1,5 ganger så lang tid med 6 prosesser, og dobbelt så lang tid med 8 prosesser. Når det kjøres fler prosesser enn det er prosessorer vil hver prosess få mindre CPU tid, fordi den deler med de andre prosessene. Med 8 kjøringer får de halvparten så mye CPU tid, samtidig som det er dobbelt så mange prosesser.

        Siden 4 kjøringer tar like lang tid som en, er det i det minste 4 cores. Når det kjøres dobbelt så mange kjøringer, blir CPU tiden ca 50% på hver, som vil tilsi at det ikke er to tråder per cpu. Derfor vil jeg konkludere med at det ikke er hyperthreading på denne serveren.


        tid*prosesser/CPU'er

        Antall CPU'er:
            (1,8 * 8) / x = 3,6
            14,4 / x = 3,6
            (14,4 / x) * x = 3,6 * x
            14,4 = 3.6x
            14,4 / 3,6 = 3,6*x / 3,6
            x = 4

        Tidsbruk
        (1,8*6)/4 = 2.7
        (1,8*8)/4 = 3.6

## Oppgave 9

    Kan konkludere med at det er 4 kjerner fordi det tar like lang tid med 1-4 prosesser, og dobbelt så mye tid med 8 prosesser, og 1,5 ganger tiden med 6 prosesser. Denne serveren bruker hyperthreading. Kan anta dette fordi 8 kjøringer bruker dobbelt så lang tid, men viser 100% CPU tid. Prosessene har alle en tråd hver, men hver tråd har ikke en ALU.

    Det er forskjeller i tidene med 6 kjøringer fordi alle prossene får 1 tråd hver, og 4 av dem får sine tråder på 2 av prosessorene. Derfor blir det 2 ledige CPU'er igjen til de 2 gjenværende prosessene og da bruker de vanlig kjøretid.

## Oppgave 10

    Denne serveren har åtte eller flere kjerner. Det tar like lang tid å kjøre 8 prosesser som 1. Det er vanskelig å si ut ifra denne dataen om CPUen bruker hyperthreading.

## Oppgave 11

```Dockerfile
FROM ubuntu/apache2
COPY ./index.html /var/www/html
RUN service apache2 start
```

## Oppgave 12

    Docker build -t ubuntuA .

    Kommandoen kan kjøres fra hvor som helst, hvis man legger path til dockerfilen i kommandoen.

## Oppgave 13

    docker run -d -p 5555:80 ubuntuA

    Det blir inkludert når imaget bygges.

## Oppgave 14

    L1 cache

## Oppgave 15

    8200

## Oppgave 16

    Mappen du står i

## Oppgave 17

    touch fil.txt

## Oppgave 18

    Dette er ikke en vanlig filendelse i Linux

## Oppgave 19

```bash
#! /bin/bash

start=$(date -d $1 +%s)
end=$(date -d $2 +%s)
echo $((end-start))
```

## Oppgave 20

```bash
#! /bin/bash

start=$(date -d $1 +%s)
end=$(date -d $2 +%s)
res=$((end-start))
echo $(date -d@$res -u +%H:%M:%S)
```

## Oppgave 21

```bash
#! /bin/bash

args=$#
if [[ "${$1##*.}" != "mp4" ]]
then
    echo "Du må angi en mp4 fil som input"
    exit
fi
if [[ ((args%2)) == 0 ]]
then
    echo "Antall tidskoder på være et partall"
    exit
fi
inputFile=$1
fileName=$(basename -s .mp4 $inputfile)
shift
((args--))
for ((i=0;i<args/2;i++))
then
    start=$(date -d@$(date -d $1 +%s) -u +%H:%M:%S)
    shift
    end=$(date -d@$(date -d $1 +%s) -u +%H:%M:%S)
    shift
    ./fromTo.sh $inputFile "$fileName$i".mp4 $start $end
done
```

## Oppgave 22

    I powershell er alt objekter :^)

## Oppgave 23

```powershell

$start = Get-Date 00:03:45
$stop = Get-Date 00:04:55

$dif=$stop - $start

$timer = '{0:d2}' -f $dif.Hours
$min = '{0:d2}' -f $dif.Minutes
$sek = '{0:d2}' -f $dif.Seconds
echo "${timer}:${min}:$sek"
echo $timer":"$min":"$sek
```

```powershell
$start = Get-Date $args[0]
$stop = Get-Date $args[1]
$dif=$stop - $start
'{0:d2}:{1:d2}:{2:d2}' -f $dif.Hours, $dif.Minutes, $dif.Seconds
```
