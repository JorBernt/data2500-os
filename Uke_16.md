# Uke 16

### **1.**

    Programmet har havnet i en deadlock. Det virker ikke som at Java forsøker å løse det.

---

<br>
<br>

### **2.(Oblig) Hva er forskjellen på en fysisk adresse og en virtuell adresse?**

    En fysisk adresse er hvor dataen er lagret i det fysiske minnet. En virtuell addresse er addressen sånn programmet ser det selv. Når programmet skal be om en ressurs fra minnet må den virtuelle addressen oversettes av en MMU (Memory management unit).

---

<br>
<br>

### **4.Oblig) Bruk page-tabellen i avsnitt 13.14 i forelesningsnotatene. Gi den fysiske adressen som korresponderer til følgende virtuelle adresser: a) 500) 18010) 46512**

    a) 8500
    b) 1810
    c) 30512

---

<br>
<br>

### **5.CPU utfører en x86-instruksjon som henter en byte fra RAM og legger den i et register. Vil CPU-cache kunne involveres når denne instruksjonen utføres?**

    Cache kan involveres om dataen som skal hentes blir mye brukt. Data som ofte aksesseres vil lagres cache så det kan nås raskere.

---

<br>
<br>

### **6. CPU utfører en x86-instruksjon som sammenligner tallene i to registere. Vil CPU-cache kunne involveres når denne instruksjonen utføres?**

---

<br>
<br>

### **7. En liten CPU bruker 10-bits registere til å adressere en byte i internminnet. Hvor stort er da det virtuelle adresserommet som kan adresseres med disse 10-bit adressene?**

    Det virutelle adresserommet må være på 1024 (2^10) byte.

---

<br>
<br>

### **8.Det virtuelle adresserommet for alle prosesser på det samme systemet er delt inn i sider (pages) med en sidestørrelse på 128 bytes. Hvor mange sider utgjør det virtuelle adresserommet til en prosess?**

    Det blir 8 sider (1024 / 128)

---

<br>
<br>

### **14. Skriv et PowerShell-script som legger sammen PagedMemorySize og WorkingSet for alle Windows-prosessene som kjører og skriver ut den totale summen for begge verdiene.**

```powershell
$sumPM = 0
$sumWS = 0
foreach ($prosess in Get-Process){
 $sumPM += $prosess.PM
 $sumWS += $prosess.WS
}
"PM: $sumPM"
"WS: $sumWS"
```

<br>
<br>

### **15. Hva er Working Set? Denne Windowsmaskinen har ca 360 MByte internminne. Sammenlign de totale summene WS og PM med størrelsen på totalt minne. Er det et problem om WS eller PM er større enn totalt minne?**

Working set er den mengden med minne en prossess trenger i et gitt tidsrom. Det er dumt om en prosess trenger mer minne enn det som er tilgjengelig

<br>
<br>

### **16. Skriv et powershell-script som ved hjelp av en løkke skriver ut følgende:**

```powershell
for ($i = 2; $i -le 8; $i+=2){
    "Linje $i"
}
```

---

<br>
<br>

### 17.Skriv en powershell oneliner som dreper alle prosesser med navn notepad.\*\*

```powershell
ps | foreach { if(.name -eq notepad){kill .id}}
```

---

<br>
<br>

### 19.Lag en PowerShell one-liner som teller opp summen av antall bytes for filene med extension .ps1 i mappen du står i og legger verdien i variabelen $sum (som kan antas å være lik 0 før kommandoen kjøres). (Hint: lov å bruke semikolon slik at resultatet kan skrives ut til slutt)..\*\*

```powershell
ls | foreach { if($_.Extension -eq ".ps1") { $sum += $_.length; }};echo $sum
```

---

<br>
<br>

### 21. Skriv en PowerShell oneliner som finner alle filer i mapper og undermapper som har filendelse .ps1.\*\*

```powershell
ls -r | foreach { if($_.Extension -eq ".ps1") {echo $_.name}}
```

---

<br>
<br>

### 21. Skriv en PowerShell oneliner som finner alle filer i mapper og undermapper som har filendelse .ps1.\*\*

```powershell
ls -r | foreach { if($_.Extension -eq ".ps1") {echo $_.name}}
```

---

<br>
<br>
