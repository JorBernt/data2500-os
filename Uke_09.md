# Uke 9

### **1.På forelesning ble output fra et par kommandoer brukt til å vise at kjernene på desktop'en rex var hyperthreading og til å vise hvilke to CPU'er mellom 0 og 7 (OS sin nummerering) som var thread-siblings, dvs deler ALU. Gjør det samme på Linux-VM. Er det thread-siblings på Linux-VM?**

Ja, det er veldig mange.

```bash
group20@os20:~$ grep "" /sys/devices/system/cpu/cpu*/topology/thread_siblings_list
/sys/devices/system/cpu/cpu0/topology/thread_siblings_list:0,48
/sys/devices/system/cpu/cpu1/topology/thread_siblings_list:1,49
/sys/devices/system/cpu/cpu10/topology/thread_siblings_list:10,58
/sys/devices/system/cpu/cpu11/topology/thread_siblings_list:11,59
/sys/devices/system/cpu/cpu12/topology/thread_siblings_list:12,60
/sys/devices/system/cpu/cpu13/topology/thread_siblings_list:13,61
/sys/devices/system/cpu/cpu14/topology/thread_siblings_list:14,62
/sys/devices/system/cpu/cpu15/topology/thread_siblings_list:15,63
/sys/devices/system/cpu/cpu16/topology/thread_siblings_list:16,64
/sys/devices/system/cpu/cpu17/topology/thread_siblings_list:17,65
/sys/devices/system/cpu/cpu18/topology/thread_siblings_list:18,66
/sys/devices/system/cpu/cpu19/topology/thread_siblings_list:19,67
/sys/devices/system/cpu/cpu2/topology/thread_siblings_list:2,50
/sys/devices/system/cpu/cpu20/topology/thread_siblings_list:20,68
/sys/devices/system/cpu/cpu21/topology/thread_siblings_list:21,69
/sys/devices/system/cpu/cpu22/topology/thread_siblings_list:22,70
/sys/devices/system/cpu/cpu23/topology/thread_siblings_list:23,71
/sys/devices/system/cpu/cpu24/topology/thread_siblings_list:24,72
/sys/devices/system/cpu/cpu25/topology/thread_siblings_list:25,73
/sys/devices/system/cpu/cpu26/topology/thread_siblings_list:26,74
/sys/devices/system/cpu/cpu27/topology/thread_siblings_list:27,75
/sys/devices/system/cpu/cpu28/topology/thread_siblings_list:28,76
/sys/devices/system/cpu/cpu29/topology/thread_siblings_list:29,77
/sys/devices/system/cpu/cpu3/topology/thread_siblings_list:3,51
/sys/devices/system/cpu/cpu30/topology/thread_siblings_list:30,78
/sys/devices/system/cpu/cpu31/topology/thread_siblings_list:31,79
/sys/devices/system/cpu/cpu32/topology/thread_siblings_list:32,80
/sys/devices/system/cpu/cpu33/topology/thread_siblings_list:33,81
/sys/devices/system/cpu/cpu34/topology/thread_siblings_list:34,82
/sys/devices/system/cpu/cpu35/topology/thread_siblings_list:35,83
/sys/devices/system/cpu/cpu36/topology/thread_siblings_list:36,84
/sys/devices/system/cpu/cpu37/topology/thread_siblings_list:37,85
/sys/devices/system/cpu/cpu38/topology/thread_siblings_list:38,86
/sys/devices/system/cpu/cpu39/topology/thread_siblings_list:39,87
/sys/devices/system/cpu/cpu4/topology/thread_siblings_list:4,52
/sys/devices/system/cpu/cpu40/topology/thread_siblings_list:40,88
/sys/devices/system/cpu/cpu41/topology/thread_siblings_list:41,89
/sys/devices/system/cpu/cpu42/topology/thread_siblings_list:42,90
/sys/devices/system/cpu/cpu43/topology/thread_siblings_list:43,91
/sys/devices/system/cpu/cpu44/topology/thread_siblings_list:44,92
/sys/devices/system/cpu/cpu45/topology/thread_siblings_list:45,93
/sys/devices/system/cpu/cpu46/topology/thread_siblings_list:46,94
/sys/devices/system/cpu/cpu47/topology/thread_siblings_list:47,95
/sys/devices/system/cpu/cpu48/topology/thread_siblings_list:0,48
/sys/devices/system/cpu/cpu49/topology/thread_siblings_list:1,49
/sys/devices/system/cpu/cpu5/topology/thread_siblings_list:5,53
/sys/devices/system/cpu/cpu50/topology/thread_siblings_list:2,50
/sys/devices/system/cpu/cpu51/topology/thread_siblings_list:3,51
/sys/devices/system/cpu/cpu52/topology/thread_siblings_list:4,52
/sys/devices/system/cpu/cpu53/topology/thread_siblings_list:5,53
/sys/devices/system/cpu/cpu54/topology/thread_siblings_list:6,54
/sys/devices/system/cpu/cpu55/topology/thread_siblings_list:7,55
/sys/devices/system/cpu/cpu56/topology/thread_siblings_list:8,56
/sys/devices/system/cpu/cpu57/topology/thread_siblings_list:9,57
/sys/devices/system/cpu/cpu58/topology/thread_siblings_list:10,58
/sys/devices/system/cpu/cpu59/topology/thread_siblings_list:11,59
/sys/devices/system/cpu/cpu6/topology/thread_siblings_list:6,54
/sys/devices/system/cpu/cpu60/topology/thread_siblings_list:12,60
/sys/devices/system/cpu/cpu61/topology/thread_siblings_list:13,61
/sys/devices/system/cpu/cpu62/topology/thread_siblings_list:14,62
/sys/devices/system/cpu/cpu63/topology/thread_siblings_list:15,63
/sys/devices/system/cpu/cpu64/topology/thread_siblings_list:16,64
/sys/devices/system/cpu/cpu65/topology/thread_siblings_list:17,65
/sys/devices/system/cpu/cpu66/topology/thread_siblings_list:18,66
/sys/devices/system/cpu/cpu67/topology/thread_siblings_list:19,67
/sys/devices/system/cpu/cpu68/topology/thread_siblings_list:20,68
/sys/devices/system/cpu/cpu69/topology/thread_siblings_list:21,69
/sys/devices/system/cpu/cpu7/topology/thread_siblings_list:7,55
/sys/devices/system/cpu/cpu70/topology/thread_siblings_list:22,70
/sys/devices/system/cpu/cpu71/topology/thread_siblings_list:23,71
/sys/devices/system/cpu/cpu72/topology/thread_siblings_list:24,72
/sys/devices/system/cpu/cpu73/topology/thread_siblings_list:25,73
/sys/devices/system/cpu/cpu74/topology/thread_siblings_list:26,74
/sys/devices/system/cpu/cpu75/topology/thread_siblings_list:27,75
/sys/devices/system/cpu/cpu76/topology/thread_siblings_list:28,76
/sys/devices/system/cpu/cpu77/topology/thread_siblings_list:29,77
/sys/devices/system/cpu/cpu78/topology/thread_siblings_list:30,78
/sys/devices/system/cpu/cpu79/topology/thread_siblings_list:31,79
/sys/devices/system/cpu/cpu8/topology/thread_siblings_list:8,56
/sys/devices/system/cpu/cpu80/topology/thread_siblings_list:32,80
/sys/devices/system/cpu/cpu81/topology/thread_siblings_list:33,81
/sys/devices/system/cpu/cpu82/topology/thread_siblings_list:34,82
/sys/devices/system/cpu/cpu83/topology/thread_siblings_list:35,83
/sys/devices/system/cpu/cpu84/topology/thread_siblings_list:36,84
/sys/devices/system/cpu/cpu85/topology/thread_siblings_list:37,85
/sys/devices/system/cpu/cpu86/topology/thread_siblings_list:38,86
/sys/devices/system/cpu/cpu87/topology/thread_siblings_list:39,87
/sys/devices/system/cpu/cpu88/topology/thread_siblings_list:40,88
/sys/devices/system/cpu/cpu89/topology/thread_siblings_list:41,89
/sys/devices/system/cpu/cpu9/topology/thread_siblings_list:9,57
/sys/devices/system/cpu/cpu90/topology/thread_siblings_list:42,90
/sys/devices/system/cpu/cpu91/topology/thread_siblings_list:43,91
/sys/devices/system/cpu/cpu92/topology/thread_siblings_list:44,92
/sys/devices/system/cpu/cpu93/topology/thread_siblings_list:45,93
/sys/devices/system/cpu/cpu94/topology/thread_siblings_list:46,94
/sys/devices/system/cpu/cpu95/topology/thread_siblings_list:47,95
```

---

<br>
<br>

### **2. Kompiler det RAM-intensive programmet mem.c demonstrert på forelesning**

```
group20@os20:~$ for i in 0 1; do time ./a.out& done
[1] 20593
[2] 20594
group20@os20:~$ 
Real:10.015 User:9.998 System:0.000 99.82%
Real:10.030 User:10.011 System:0.000 99.81%
```

```
group20@os20:~$ for i in 0 1; do time taskset -c 0 ./a.out& done
[1] 20597
[2] 20598
group20@os20:~$ 
Real:20.047 User:10.020 System:0.000 49.98%
Real:20.052 User:10.020 System:0.000 49.97%
```
    Det tar dobbelt så lang tid når jeg velger hvilken CPU de skal kjøre på.

---

<br>
<br>

### **3.**

```
group20@os20:~$ for i in 0 48; do time taskset -c $i ./regn.sh& done
[1] 21016
[2] 21017
group20@os20:~$ 
Real:22.098 User:21.941 System:0.004 99.30%
Real:22.111 User:21.947 System:0.004 99.27%
for i in 0 48; do time taskset -c $i ./regn.sh& done^C
[1]-  Done                    time taskset -c $i ./regn.sh
[2]+  Done                    time taskset -c $i ./regn.sh
group20@os20:~$ for i in 0 1; do time taskset -c $i ./regn.sh& done
[1] 21033
[2] 21034
group20@os20:~$ 
Real:12.990 User:12.979 System:0.000 99.92%
Real:13.310 User:13.287 System:0.000 99.83%

```

    Det er stor forskjell mellom å bruke hyperthreading og to forskjellige CPU-kjerner. Det er fordi det er bare en ALU per CPU, og i et CPU-intensivt program som "regn" hvor alt foregår på ALU'en, så må de to prosessene stå i kø for å bruke denne i hyperthreading, mens de slipper det med hver sin ALU og CPU-kjerne.

### **4.**

 Siden programmet er veldig memory intensiv, så får den full effekt av hyperthreading. Da kan prosessene bruke ALU'en, mens den andre leser og skriver til minne. Det tar like lang tid med hyperthreading som å  bruke flere cpuer.

 ## **5. Docker LAB oppgaver**

 ### **1. Hello World**

 ```
 root@os20:/home/group20# docker container run hello-world

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/
```

---
<br>

### **2.Running Image**

```
root@os20:/home/group20# docker image pull alpine
Using default tag: latest
latest: Pulling from library/alpine
59bf1c3509f3: Pull complete
Digest: sha256:21a3deaa0d32a8057914f36584b5288d2e5ecc984380bc0118285c70fa8c9300
Status: Downloaded newer image for alpine:latest
docker.io/library/alpine:latest
```

```
root@os20:/home/group20# docker container run alpine ls -l
total 56
drwxr-xr-x    2 root     root          4096 Nov 24 09:20 bin
drwxr-xr-x    5 root     root           340 Mar  2 14:23 dev
drwxr-xr-x    1 root     root          4096 Mar  2 14:23 etc
drwxr-xr-x    2 root     root          4096 Nov 24 09:20 home
drwxr-xr-x    7 root     root          4096 Nov 24 09:20 lib
drwxr-xr-x    5 root     root          4096 Nov 24 09:20 media
drwxr-xr-x    2 root     root          4096 Nov 24 09:20 mnt
drwxr-xr-x    2 root     root          4096 Nov 24 09:20 opt
dr-xr-xr-x 2511 root     root             0 Mar  2 14:23 proc
drwx------    2 root     root          4096 Nov 24 09:20 root
drwxr-xr-x    2 root     root          4096 Nov 24 09:20 run
drwxr-xr-x    2 root     root          4096 Nov 24 09:20 sbin
drwxr-xr-x    2 root     root          4096 Nov 24 09:20 srv
dr-xr-xr-x   13 nobody   nobody           0 Mar  2 14:23 sys
drwxrwxrwt    2 root     root          4096 Nov 24 09:20 tmp
drwxr-xr-x    7 root     root          4096 Nov 24 09:20 usr
drwxr-xr-x   12 root     root          4096 Nov 24 09:20 var
```

```
root@os20:/home/group20#  docker container run alpine echo "hello from alpine"
hello from alpine
```

```
root@os20:/home/group20# docker container run -it alpine /bin/sh
/ # ls
bin    dev    etc    home   lib    media  mnt    opt    proc   root   run    sbin   srv    sys    tmp    usr    var
```

```
/ # exit
root@os20:/home/group20# docker container ls
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
root@os20:/home/group20# docker container ls -a
CONTAINER ID   IMAGE         COMMAND                  CREATED              STATUS                         PORTS     NAMES
9c2a08af1a43   alpine        "/bin/sh"                About a minute ago   Exited (130) 21 seconds ago              recursing_hertz
63d31428d089   alpine        "echo 'hello from al…"   3 minutes ago        Exited (0) 3 minutes ago                 flamboyant_darwin
b125142270ef   alpine        "ls -l"                  4 minutes ago        Exited (0) 4 minutes ago                 xenodochial_ellis
4e3e578d0664   hello-world   "/hello"                 10 minutes ago       Exited (0) 10 minutes ago                naughty_lehmann
bb20e94a493b   hello-world   "/hello"                 About an hour ago    Exited (0) About an hour ago             unruffled_mcnulty
507e90be950c   hello-world   "/hello"                 About an hour ago    Exited (0) About an hour ago             confident_archimedes
```

For å navngi en container "test"
```
root@os20:/home/group20# docker container run -it --name test alpine /bin/sh
```
---
<br>

### **3.Deletion**

```
$ rm -rf /
/ # ls
/bin/sh: ls: not found
/ # ls
/bin/sh: ls: not found
/ # cd
/bin/sh: cd: can't cd to /root: No such file or directory
/ # ls -la
/bin/sh: ls: not found
```

```
root@os20:/home/group20# docker container ls -as
CONTAINER ID   IMAGE         COMMAND                  CREATED          STATUS                        PORTS     NAMES                  SIZE
4887da041a22   alpine        "/bin/sh"                26 seconds ago   Exited (0) 7 seconds ago                peaceful_hamilton      8B (virtual 5.58MB)
eb1b453294cd   alpine        "/bin/sh"                5 minutes ago    Exited (127) 2 minutes ago              exciting_aryabhata     0B (virtual 5.58MB)
```

```
root@os20:/home/group20# docker container rm naughty_lehmann
naughty_lehmann

root@os20:/home/group20# docker container ls -a
CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS                        PORTS     NAMES
4887da041a22   alpine    "/bin/sh"                4 minutes ago    Exited (0) 4 minutes ago                peaceful_hamilton
eb1b453294cd   alpine    "/bin/sh"                9 minutes ago    Exited (127) 7 minutes ago              exciting_aryabhata
282c722abe3f   alpine    "/bin/sh"                11 minutes ago   Exited (127) 9 minutes ago              pedantic_chaplygin
36b804dd4fff   alpine    "/bin/sh"                12 minutes ago   Exited (0) 12 minutes ago               test
a74b05a229e8   alpine    "/bin/sh --name test"    13 minutes ago   Exited (2) 13 minutes ago               nostalgic_agnesi
9c2a08af1a43   alpine    "/bin/sh"                16 minutes ago   Exited (130) 15 minutes ago             recursing_hertz
63d31428d089   alpine    "echo 'hello from al…"   18 minutes ago   Exited (0) 18 minutes ago               flamboyant_darwin
b125142270ef   alpine    "ls -l"                  19 minutes ago   Exited (0) 19 minutes ago               xenodochial_ellis
```

```
root@os20:/home/group20# docker image ls
REPOSITORY    TAG       IMAGE ID       CREATED        SIZE
alpine        latest    c059bfaa849c   3 months ago   5.58MB
hello-world   latest    feb5d9fea6a5   5 months ago   13.3kB
root@os20:/home/group20# docker image rm feb5d9fea6a5
Untagged: hello-world:latest
Untagged: hello-world@sha256:97a379f4f88575512824f3b352bc03cd75e239179eea0fecc38e597b2209f49a
Deleted: sha256:feb5d9fea6a5e9606aa995e879d862b825965ba48de054caab5ef356dc6b3412
Deleted: sha256:e07ee1baac5fae6a26f30cabfe54a36d3402f96afda318fe0a96cec4ca393359
```

### **4.A basic webserver**

<p align="center">
    <img src="images\nginx.png" style="width: auto;" alt="">
</p>

    Kjører i bakgrunn
```
root@os20:/home/group20# docker container run -p 7979:80 -d nginx
c48e742e40da9208b4b8dd6bd6465649533ea29db60923714e79fad1bd453775
```

---
<br>

### **5. Executing**

```
root@os20:/home/group20# docker container exec -it c48e742e40da9208b4b8dd6bd6465649533ea29db60923714e79fad1bd453775 bash
root@c48e742e40da:/#
```
<p align="center">
    <img src="images\nginx_html_hack.png" style="width: auto;" alt="">
</p>

---


### **6.**

```
root@os20:/home/group20# docker container run -it -d -p 8082:80 apacheubuntu /bin/bash
a82a72a317dd5a40b8efd44bf054eb0e9681466b841b2047ed87a030348d9cc6
root@os20:/home/group20# docker container ps -a
CONTAINER ID   IMAGE          COMMAND                  CREATED          STATUS                      PORTS                  NAMES
a82a72a317dd   apacheubuntu   "/bin/bash"              27 seconds ago   Up 26 seconds               0.0.0.0:8082->80/tcp   awesome_chebyshev
f33a256aec01   ubuntu         "/bin/bash"              10 minutes ago   Up 10 minutes               0.0.0.0:8081->80/tcp   loving_satoshi
843e75d2b66c   ubuntu         "-p 8081:80 /bin/bash"   10 minutes ago   Created                                            zealous_hermann
94a83aab0150   ubuntu         "-it -p 8081:80 /bin…"   10 minutes ago   Created                                            charming_aryabhata
c48e742e40da   nginx          "/docker-entrypoint.…"   20 minutes ago   Up 20 minutes               0.0.0.0:7979->80/tcp   jovial_austin
fbcc326b26b4   nginx          "/docker-entrypoint.…"   23 minutes ago   Exited (0) 21 minutes ago                          tender_williamson
d35bcf4d428e   nginx          "/docker-entrypoint.…"   24 minutes ago   Exited (0) 23 minutes ago                          confident_williamson
294347c6baea   nginx          "/docker-entrypoint.…"   25 minutes ago   Exited (0) 24 minutes ago                          xenodochial_bassi
root@os20:/home/group20# docker container exec a82a72a317dd /bin/bash -c "/etc/init.d/apache2 start"
 * Starting Apache httpd web server apache2
AH00558: apache2: Could not reliably determine the server's fully qualified domain name, using 172.17.0.4. Set the 'ServerName' directive globally to suppress this message
 *
root@os20:/home/group20# docker container exec a82a72a317dd /bin/bash -c "echo container 1 > /var/www/html/index.html"
root@os20:/home/group20# docker container exec f33a256aec01 /bin/bash -c "echo container 2 > /var/www/html/index.html"
```
