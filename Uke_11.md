# Uke 11

### **1.Lag et script som tar en pid som argument og deretter går i en evig løkke og skriver ut antall ticks prosessen som har denne pid-en bruker i user-mode hvert sekund.**

```bash
#! /bin/bash

while :
do
        echo $(cat /proc/$1/stat | cut -d' ' -f 14)
done
~             
```
I guess?

---

<br>
<br>

### **11.2.(Oblig) Man kan installere kildekoden for linux med**

    sudo apt-get install linux-source

### **Dette er gjort på data2500 og kildekoden ligger der i**

    /usr/src/linux-source-5.10

### **Finn ut fra filen**

    /usr/src/linux-source-5.10/arch/x86/entry/syscalls/syscall_64.tbl

### **hvor mange systemkall det er i denne versjonen av Linux-kjernen. I mappen over er det en fil som heter entry_64.S . Hvilken funksjon har koden i denne filen og hvilket språk er den skrevet i?**

    350, eller så er det 385.
    Det er entry-point for 64-bit systemkall.

---
<br>
<br>

## **4.**

---
<br>
<br>

## **5.**

    Taskset setter hvilke CPU(er) som skal brukes på prosessen. Om en starter to prosesser på samme cpu deler de på CPU tiden på to.

    Om den ene prosessen kjører med en nice verdi på 19, vil den andre prosessen så og si ta hele CPU-tiden.

<p align="center">
    <img src="images\nice19.png" style="width: auto;" alt="">
</p>

---
<br>
<br>

## **8.(Oblig) Studer og kjør følgende kode:**

```C
#include <stdio.h>
#include <sys/types.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/types.h>
#include <sys/wait.h>

int main(){

int i,id,pid,mypid,ppid;
id = getpid();
printf ("Fork demo!\n Jeg er parent-prosess med pid = %d \n",id);
sleep(2);
pid = fork();     /* Prosessen lager nå en ny uavhengig prosess
                     I den nye barne-prosessen er $pid = 0
                     I foreldre prosessen er $pid = barnets PID */
if (pid == 0)
  {
    mypid = getpid();
    ppid  = getppid();
    printf("       Jeg er child (mypid = %d) av parent med pid = %d.\n",mypid,ppid);
    printf("       Here er variabelen pid = %d.\n",pid);
    for (i = 1;i < 10;i++)
      {
        printf("       %d \n",i);
        sleep(1);
      }
    printf("       Child prosess avslutter.\n");
    exit(0);
  } 
else
  {
    sleep(2);
    printf("Parent %d venter på child %d her...\n",id,pid);
    wait(&pid); 
    printf("Child har avsluttet, Parent avslutter!\n");
  }

}
```

Kanskje noe sånt?

```c
#include <stdio.h>
#include <sys/types.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/types.h>
#include <sys/wait.h>

int main(){
    printf ("Fork demo!\n Jeg er parent-prosess med pid = %d \n",getpid());
    sleep(2);
    forking(1);
}

void forking(int done) {
int i,id,pid,mypid,ppid;
id = getpid();
pid = fork();

if(pid == 0)
  {
    mypid = getpid();
    ppid  = getppid();
    printf("       Jeg er child (mypid = %d) av parent med pid = %d.\n",mypid,ppid);
    printf("       Here er variabelen pid = %d.\n",pid);
    sleep(5);
    printf("       Child prosess avslutter.\n");
    if(done == 1)
    forking(0);
    exit(0);
  }
else
  {
    sleep(2);
    printf("Parent %d venter på child %d her...\n",id,pid);
    wait(&pid);
    printf("Child har avsluttet, Parent avslutter!\n");
  }
}
```

---
<br>
<br>

### **10.**

Dockerfile
```
FROM ubuntu
RUN apt-get --fix-missing -y update
ENV TZ=Europe/Oslo
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone
RUN apt-get install --yes build-essential
RUN apt-get install --yes default-jdk
RUN apt-get install --yes python3
RUN apt-get install --yes git
RUN git clone https://github.com/haugerud/sum.git
```

---

<br>
<br>

### **11.**

Bash-scriptet brukte ca 5.1 sek

<table style="undefined;table-layout: fixed; width: 383px"><colgroup><col style="width: 58px"><col style="width: 240px"><col style="width: 85px"></colgroup><thead><tr><th>Språk</th><th>CPU-tid i sekunder på cube</th><th>TIMES</th></tr></thead><tbody><tr><td>bash</td><td>5.1</td><td>1</td></tr><tr><td>perl</td><td>5.1</td><td>28</td></tr><tr><td>php</td><td>5.1</td><td>215</td></tr><tr><td>Java</td><td>5.1</td><td>18200</td></tr><tr><td>C</td><td>5.1</td><td>36000</td></tr></tbody></table>




