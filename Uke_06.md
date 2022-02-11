# Uke 6

### **1.(Oblig) Les 5.2 'En linje høynivåkode kan gi flere linjer maskininstruksjoner' i Forelesningsnotatene, kompiler programmene, C-koden main og assembly-koden enlinje.s (den som starter med .globl enlinje), vis at en kjøring gir svaret 42 og forklar så hvorfor svaret blir 42 utifra assembly-koden.**

---
<br>
<br>

### **2.(Oblig) Bruk så det C-programet som gjør det samme som assembly-koden i forrige oppgave(deklarer int-variabler svar og memvar), kompiler det sammen med main C-programmet på samme måte og sjekk at svaret blir det samme. Kompiler C-funksjonen alene med gcc -S og studer den resulterende assembly-koden.**

```bash
jorber@JBMain:~/uke6$ gcc main.c enlinje.c
jorber@JBMain:~/uke6$ ./a.out
Kaller enlinje()...
Svar = 42
```

Assembly:
```bash
enlinje:
.LFB0:
        .cfi_startproc
        endbr64
        pushq   %rbp
        .cfi_def_cfa_offset 16
        .cfi_offset 6, -16
        movq    %rsp, %rbp
        .cfi_def_cfa_register 6
        movl    $32, -8(%rbp) #Flytter verdi 32 til register A
        movl    $10, -4(%rbp) #Flytter verdi 10 til register B
        movl    -4(%rbp), %eax #Flytter register B til RAM A
        addl    %eax, -8(%rbp) #Adderer RAM A til register A (10 + 32)
        movl    -8(%rbp), %eax #Flytter register A til RAM A (42)
        popq    %rbp            #Popper svaret for å returnere?
        .cfi_def_cfa 7, 8
        ret
        .cfi_endproc
```

### **Hvor mange linjer leder den ene høynivå-koden til?**
Den leder til 5 linjer assembly :

```
movl    $32, -8(%rbp) #Flytter verdi 32 til register A
movl    $10, -4(%rbp) #Flytter verdi 10 til register B
movl    -4(%rbp), %eax #Flytter register B til RAM A
addl    %eax, -8(%rbp) #Adderer RAM A til register A (10 + 32)
movl    -8(%rbp), %eax #Flytter register A til RAM A (42)
```
### **Hvordan endrer den resulterende assembly-koden seg om du bruker "long long" istedet for "int" for variablene i C-funksjonen?**

```
jorber@JBMain:~/uke6/long$ diff enlinjeint.s enlinjelonglong.s
1c1
<       .file   "enlinjeint.c"
---
>       .file   "enlinjelonglong.c"
14,18c14,18
<       movl    $32, -8(%rbp)
<       movl    $10, -4(%rbp)
<       movl    -4(%rbp), %eax
<       addl    %eax, -8(%rbp)
<       movl    -8(%rbp), %eax
---
>       movq    $32, -16(%rbp)
>       movq    $10, -8(%rbp)
>       movq    -8(%rbp), %rax
>       addq    %rax, -16(%rbp)
>       movq    -16(%rbp), %ra
```
I long long versjonen ser det ut som størrelsen på registerene har doblet seg.
Det gir mening siden int er 32 bit, og long long er 64 bit.

---
<br>
<br>

### **3.Ukens utfordring nr. 1: Ta utgangspunkt i if-testen skrevet i Assembly fra forelesningen hvor variabelen svar er defintert og skriv et Assembly-program som**
- ### Returnerer 1 hvis svar > 0
- ### Returnerer -1 hvis svar < 0
- ### Returnerer ellers 0

iftest.s:
```bash
.globl iftest
iftest:

mov $42, %rbx

cmp %rbx, svar
jg greater

cmp %rbx, svar
jl less

mov $0, %rax
jmp return

greater:
mov $1, %rax
jmp return

less:
mov $-1, %rax

return:
ret

.data
svar: .quad 45
```
main.c:
```c
#include <stdio.h>

extern int iftest();

int main (void) {
        int svar = iftest();
        printf("Svar = %d\n", svar);
}
```

---
<br>
<br>

### **4.Ukens utfordring nr. 2: Lag en assemblymetode as.s som returnerer tall nr 46 i Fibonacci-rekken 1, 1, 2, 3, 5, 8, 13,... Lag en tilsvarende metode skrevet i C og test at resultatet stemmer. Hva skjer om du regner ut tall nr 47 i rekken? Hvorfor skjer dette? Prøv å endre type fra int til long long og om du da kan klare å regne ut tall nr 92 i rekken. Hva skjer om du regner ut tall nr 93? Hvorfor skjer dette?**

fibo.s
```bash
.globl fibo

fibo:

mov $1, %rbx #a
mov $1, %rdx #b
mov $2, %cx #i

loop:
mov %rbx, %rax
add %rdx, %rbx
mov %rax, %rdx
inc %cx

cmp %cx, max
jg loop

ret

.data

max: .quad 93

```

Resultat
```bash
jorber@JBMain:~/uke6/oppgave4$ ./fiboTest
Svar = 1836311903 #45

jorber@JBMain:~/uke6/oppgave4$ ./fiboTest
Svar = 7540113804746346429 #92

jorber@JBMain:~/uke6/oppgave4$ ./fiboTest
Svar = -6246583658587674878 #93
```

en int i C har bare 16 bits, og som signed er det høyeste tallet den kan lagre 32767. Denne vil overflowe som bare det for fibonaccitallet nr 46. Den vil også overflowe en signed long (32 bit)

Det samme gjelder nummer 94, den vil overflowen signed long long (64-bit)

## Ekstra ekstra oppgave:

```c
#include <stdio.h>
#include "BigInt/BigInt.h"

void fibo() {
	BigInt* a = BigInt_construct(1);
	BigInt* b = BigInt_construct(1);
	BigInt* temp = BigInt_construct(0);

	for(int i = 2; i < 1000; ++i) {
		BigInt_add(temp, b);
		BigInt_add(temp, a);
		BigInt_free(a);
		a = BigInt_construct(0);
		BigInt_add(a, b);
		BigInt_free(b);
		b = BigInt_construct(0);
		BigInt_add(b,temp);
		if(i < 999) {
			BigInt_free(temp);
			temp = BigInt_construct(0);
		}
	}
	BigInt_print(temp);
	printf("\n");
}
```
Tall 1000:
```
jorber@JBMain:~/uke6/oppgave4/bigFibo$ ./a.out
43466557686937456435688527675040625802564660517371780402481729089536555417949051890403879840079255169295922593080322634775209689623239873322471161642996440906533187938298969649928516003704476137795166849228875
```

---
<br>
<br>

### **5. Ta utgangspunkt i hash-strengen**
```
$6$AB.f/K06$IsV3oABaBO4UEBertVwViFgqFcuRvPfBDBVojDJkwg43AlPlgfD.y8nCpjnb01EgwwrVaxpYRzYjgT5G1g4lw.
```
### **som er hentet fra shadow-filen på en Linux-server. Passordet er laget med små bokstaver og er bare tre tegn langt. Lag et shell-script som bruker kommandoen mkpasswd til å regne ut hash-verdien for alle mulige kombinasjoner av ord med tre små bokstaver mellom a og z. Det vil si aaa, aab, aac, etc. Få scriptet til å sammenligne med hash-strengen over slik at du dermed cracker passordet!**

```bash
#! /bin/bash

pass=$(cat $1)
salt=$(cat $1 | awk '{split($0,a,"$"); print a[3]}')
i=0
for p in {a..z}{a..z}{a..z}; do
	((i++))
	gen=$(echo $(mkpasswd -m SHA-512 -s $p -S $salt))
	echo "Prøver $i av 17576 ($p)   $gen"
	if [[ "$pass" = "$gen" ]]; then
		echo "Passord funnet: $p"
		break
	fi
done
```

```
Prøver 13291 av 17576 (tre)   $6$AB.f/K06$IsV3oABaBO4UEBertVwViFgqFcuRvPfBDBVojDJkwg43AlPlgfD.y8nCpjnb01EgwwrVaxpYRzYjgT5G1g4lw.
Passord funnet: tre
```

## **6.Prøv å forklare resultatene av følgende kommandoene.**

```bash
echo dette er en test | sed s/test/fisk/ # Bytter ordet "test" med "fisk"
echo test og test | sed s/test/fisk/ #Bytter kun det første ordet "test" med "fisk"
echo test og test | sed s/test/fisk/g #Bytter alle forekomster av ordet "test" med "fisk"
echo test og test | sed s@test@fisk@g #@ er det samem som /
echo `pwd` | sed s///:/g      # (prøver å bytte ut / med : ) men får feil fordi det vi vil bytte inneholder en "/" og det forvirrer sed
echo `pwd` | sed s@/@:@g # så da må vi bruke @ i steden for
echo `pwd` | sed s/\[/\]/:/g  # gir det samme som forrige, fordi vi escaper "/"
find ~ -mtime +1 -print # Viser alle filer i home som er endret for minst 1 dag i siden
find ~ -mtime 0 -exec file {} \; #Viser file type av alle filer endret idag.

#Finner alle skjulte filer i home
for variable in $(find ~ -name '.*' -print)
do
echo Hidden file/directory $variable
file $variable
echo ------------------------------
done
```
---

<br>
<br>

### **8. Lag en fil med navn fil.txt som inneholder**

```
s802399@stud.hioa.no
s886878@stud.hioa.no
s886876@stud.hioa.no
s886885@stud.hioa.no
s886884@stud.hioa.no
s850806@stud.hioa.no
s886873@stud.hioa.no
s886888@stud.hioa.no
s808855@stud.hioa.no
s856627@stud.hioa.no
s886878@stud.hioa.no
s299507@stud.hioa.no
s850798@stud.hioa.no
s803434@stud.hioa.no
s886879@stud.hioa.no
s886877@stud.hioa.no
s959938@stud.hioa.no
s886880@stud.hioa.no
s826650@stud.hioa.no
s886882@stud.hioa.no
s886874@stud.hioa.no
s859987@stud.hioa.no
s803833@stud.hioa.no
s886885@stud.hioa.no
```

### **Lag så en kommando som fra denn filen lager en ny fil nyfil.txt hvor alle forekomster av stud.hioa.no er byttet ut med oslomet.no**

```bash
# /bin/bash
rm resultat.txt 2>/dev/null
while read LINE; do
	echo $LINE | sed s/stud.hioa.no/oslomet.no/ >> resultat.txt
done
cat resultat.txt
```

```
jorber@JBMain:~/uke6/oppgave8$ ./script.sh < fil.txt
s802399@oslomet.no
s886878@oslomet.no
s886876@oslomet.no
s886885@oslomet.no
s886884@oslomet.no
s850806@oslomet.no
s886873@oslomet.no
s886888@oslomet.no
s808855@oslomet.no
s856627@oslomet.no
s886878@oslomet.no
s299507@oslomet.no
s850798@oslomet.no
s803434@oslomet.no
s886879@oslomet.no
s886877@oslomet.no
s959938@oslomet.no
s886880@oslomet.no
s826650@oslomet.no
s886882@oslomet.no
s886874@oslomet.no
s859987@oslomet.no
s803833@oslomet.no
s886885@oslomet.no
```

---

<br>
<br>

### **9.Ta utgangspunkt i en fil med navn fil.txt som inneholder listen**

```bash
grep -o s[0-9]*@stud.hioa.no fil.txt | sed s/stud.hioa.no/oslomet.no/ >> nyfil.txt
```

---

<br>
<br>

### **10 Lag en enlinjes Linux-kommando som skriver ut en liste med de 10 største filene i /etc, omtrent slik (på data2500):**

```bash
jorber@JBMain:/etc$ ls -laS | head -11
total 816
-rw-r--r--  1 root root      31133 Feb 11 09:12 ld.so.cache
-rw-r--r--  1 root root      24546 Oct 19  2019 mime.types
-rw-r--r--  1 root root      14867 Feb  1  2019 ltrace.conf
-rw-r--r--  1 root root      14464 Feb 17  2020 services
-rw-r--r--  1 root root      10593 Nov  6  2019 sensors3.conf
-rw-r--r--  1 root root      10550 Feb  7  2020 login.defs
-rw-r--r--  1 root root      10037 Feb  7  2020 nanorc
-rw-r--r--  1 root root       9440 Apr 23  2020 locale.gen
-rw-r--r--  1 root root       6920 Feb 25  2020 overlayroot.conf
-rw-r--r--  1 root root       5713 Apr 23  2020 ca-certificates.conf
```

---
<br>
<br>

### **11.