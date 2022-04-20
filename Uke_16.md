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
