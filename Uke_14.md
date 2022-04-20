# Uke 14

### **1. Ta utgangspunkt i java-programmet NosynchThread.java fra avsnitt 11.12 i forelesningsnotatene. I java kan man sikre seg mot at en felles variabel ikke blir oppdatert av to threads samtidig ved å lage en kodeblok**

```java
synchronized(objekt)
   {
   // Her kan bare en thread av gangen kjøre kode; kritisk avsnitt 
   }
```

### **Endre java-programmet over ved å først lage**
```java
public static Object lock = new Object(); // Et lock-objekt 
```
### **Og deretter bruke synchronized rundt de kritiske avsnittene i koden til å serialisere NosynchThread.java slik at resultatet blir riktig. Tar programmet lengre tid å kjøre nå? Isåfall: hvorfor? Gjør det noen forskjell om du starter java med taskset -c 0?**

```java
public void updateSaldo()
    {
    int i;
    if(id == 1)
    {
        synchronized(lock) {
                for(i = 1;i < MAX;i++)
                {
                        saldo++;
                }
        }
    }
    else
    {
        synchronized(lock) {
                for(i = 1;i < MAX;i++)
                {
                        saldo--;
                }
        }
    }
    System.out.println("Thread nr. " + id + " ferdig. Saldo: " + saldo);
    }
```

    Begge programmene kjører like raskt, på omtrent 0.150 sekunder. Om de kjøres med taskset er de begge omtrent 0.050 sekunder tregere i snitt
---
<br>
<br>

### **10. Skriv et Windows bat-script som skriver ut Hello World! når det kjøres. Legg det på Deskotop slik at det enkelt kan brukes. Legg til kommandoen pause til slutt i scriptet, så forsvinner ikke cmd-vinduet med en gang.**

.bat
```bat
ECHO OFF
ECHO “Hello World”
PAUSE
```
---
<br>
<br>

### **11. Lag et VBScript i notepad som skriver ut Hello World! Pas på å lagre det som "hello.vbs" samtidig som du velger "Files of type: All files".**
.vbs
```vbs
MsgBox("Hello World")
```
---
<br>
<br>

### **12.Lag et VBScript som skriver ut "Ja" hvis tallet du sender med som argument når du kjører det med**

    C:\> arg.vbs 3
### **er større enn 5 og "nei" hvis det er mindre enn 5. Hint: Wscript.Arguments(0) er det første argumentet.**

.vbs med if-else
```vbs
IF Wscript.Arguments(0) > 5 Then
MsbBox “Ja, Større enn 5”
ELSE
MsgBox “Nei, Mindre enn 5”
END IF
```
---
<br>
<br>

### **13. Sørg for at "Hello world!" powershell-scriptet fra forelesningen virker. Pass på at du må (med Administrator-rettigheter) sette**
    PS C:\> set-executionPolicy remoteSigned
### **for å kunne kjøre PowerShell-script. Det kan du få til ved Windows-tast og så skrive p (for PowerShell) og så høyreklikke på ikonet som kommer opp og velge Run as administrator.**
<br>

<p align="center">
    <img src="images\vbs_helloWorld.png" style="width: auto;" alt="">
</p>
---
<br>
<br>

### **15. EKjør følgende bash-script i en mappe på en Linux maskin og forklar kort hva resultatet blir:**
```bash
mkdir dir
cd dir
echo hei > fil.txt
cp fil.txt lik.txt
mv fil.txt ..
cp lik.txt kopi.txt
rm lik.txt
ls
```
    Etter scriptet er kjørt ligger det en fil.txt som inneholder "hei" sammen med en mappe (dir). I mappen dir ligger det en fil kalt kopi.txt som også inneholder "hei
### **Lag et PowerShell-script som gjør det samme som bash-scriptet, kjør det i PowerShell og sjekk at resulatet blir likt. Hvilke Cmdlets og functions bruker scriptet?**
    PowerShell scriptet bruker flere cmdlets som New-Item, Copy-Item, Move-Item, Remove-Item osv.

### **16. Skriv ut verdien av systemvariabelen $PSVersionTable for å se hvilken versjon av powershell du kjorer.**
    PSVersion er 7.2.2

### **18. CreationTime er en property for et PowerShell filobjekt. Gi en PowerShell-kommando som gir hvilket tidspunkt filen fil.txt i mappen du står i ble laget.**
    Get-ChildItem -Path .\fil.txt | select name,creationTime


### **19. Gi en PowerShell-kommando som gir årstallet for når filen C:\Windows\system.ini ble laget.**
     Get-ChildItem -Path C:\Windows\system.ini | Select-Object -ExpandProperty CreationTime | Get-Date -f "yyyy"
### **21.  Gi en PowerShell-kommando som skriver ut prosess-IDen for prosessen med navn 'idle'. Bruk først Get-Member for å finne ut hvilke properties ps har.**
    ps | Get-Member
    Get-Process Idle | select Id

### **22. Start en notepad-prosess fra PowerShell. Bruk så en ps-metode som gjør at nodepad-prosessen stoppes . Bruk først Get-Member for å finne ut hvilke properties ps har. Lag en ny notepad-prosess og bruk aliaset kill til å drepe den. Hva skjer om du har to notepad-prosesser?**
    Om vi bruker kill -name notepad så avsluttes alle instanser.
    En må bruke PID om en skal avslutte individuelle.
### **24. Ville det gi mening å kjøre tilsvarende kommandoer som i forrige oppgave i bash? Forklar.**
    Kommandoer fra forrige oppgave
        (ls test.txt).Length
        (ls test.txt).get_Length();

### **25. Installer først installasjonsprogrammet Chocolatey ved å kjøre følgende kommando i et elvert (admin) PowerShell:**
    PS C:\> wget -OutFile install.ps1 http://chocolatey.org/install.ps1    

### **og kjør det så i et Admin-vindu:**
    PS C:\> .\install.ps1
    
### **NB! Du må ha satt ExecutionPolicy til RemoteSigned for å kunne kjøre dette ps1-installasjonsscriptet, se den tidligere oppgaven om dette. Hvis dette ikke fungerer (pga SSL/TSL problemer), prøv istedet følgende 'lille' oneliner:**

    Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))
### **Chocolatey (eller kortversjonen choko) fungerer omtrent som apt-get på Linux og kan brukes til å installere programvare fra Power-Shell kommandolinjen eller i PowerShell-script. Installer først ssh som administrator med**
    PS C:\> choco install openssh
### **Sjekk deretter at du fra et PowerShell kan logge inn på Linux-VM med ssh. Du må starte et nytt PowerShell for at ssh skal virke. Logg ut av Linux-VM og tilbake til PowerShell og bruk så kommandoen scp til å laste ned mappen /tmp/dir på data2500 til Windows 10; bruk samme syntaks som for scp i Linux.**
    Resultat...