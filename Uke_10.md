# Uke 10

### **10.1. Se på CPU-usage på en Linux-VM. Hvor mye av CPU'en brukes vanligvis? Her ser det ut til å være mye ressurser til overs. Hvordan kan de utnyttes bedre, eller gjør de allerede det?**

    Ved å se på TOP med et delay på 3 sekunder på intel3-serveren, kan vi se at CPU'en er ~100% idle i løpet av de tre sekundene. 

---
<br>
<br>

### **10.2 Hva er en trap-instruksjon? Forklar kort hva den brukes til i et operativsystem.**

    Det er en instruksjon for å skifte modusbiten fra bruker til kernel. Den brukes når et brukerprogram ønsker å gjøre en operasjon som krever aksess fra kernel. Den hopper til predefinerte steder i minnet hvor kode for systemkall ligger, utfører systemkallet og skifter tilbake igjen til brukermodus.

---
<br>
<br>

### **10.4 Linux-kjernen konfigurerer vanligvis hardware-timeren til å sende et interrupt hvert hundredels sekund. Forklar kort hvorfor dette timer-interruptet er nødvendig for at Linux-kjernen skal kunne fordele CPU-tid mellom alle prosessene uten at en av disse prosessene kan ta over styringen.**

    Hver prosess får tildelt et time-quantum som måles i helt antall jiffies.
    Får hver tick 


