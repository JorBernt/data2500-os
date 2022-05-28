## Oppgave 1a

    mv /tmp/fil.txt .

## Oppgave 1b

    Kun brukeren haugerud

## Oppgave 1c

    tail -n 5 index.html | grep name | cut -d\" -f 4

## Oppgave 1d

    sort -n -k 3 biler

## Oppgave 2

```bash
#! /bin/bash
teller=30
prev=0
while [[ $teller > 0 ]]
do
    i=0
    new=$(grep cpu /proc/stat | cut -d' ' -f $(($1+2))| head -n 1)
    echo $((new-prev))
    prev=$new
    ((teller--))
    sleep 1
done
```

## Oppgave 3a

## Oppgave 3b

## Oppgave 3c

    5 minutter

## Oppgave 3d

31

## Oppgave 3e

    2^31 - 1 = 2147483647

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

```powershell
$array = @()
foreach($fil in (ls -r).CreationTime 2>$null){
    $day=[int]$fil.DayOfWeek
    if(!($array.Contains($day))) {
        $array+=$day
    }
    $array[$day]++
}
echo $array
```

$array = @(0,0,0,0,0,0,0)
foreach($fil in (ls -r).CreationTime 2>$null){
    $day=[int]$fil.DayOfWeek
$array[$day]++
}
echo $array
