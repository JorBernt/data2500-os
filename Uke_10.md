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

    Hver prosess får tildelt et time-quantum som måles i helt antall jiffies, og lagres i en counter.
    Får hver tick minker counter med 1, og når en prosess ikke har flere igjen, kalles schedule() og en ny prosess velges. 
    Ticksene styres av hardware-timeren, siden det ville blitt for mye systemoverhaed om OS skulle styrt dette selv.

### **10.6.Problem 1.15 i Tanenbaum: Hva er den viktigste forskjellen mellom en trap og et interrupt? (I videoen som demonstrerer multitasking av forelesning og vaffelrørelaging : forskjellen på når vaffelprosessen ønsket å knuse et egg og på avbruddene fra timeren og fra melkemannen når melken leveres)**