<div align="center">
<h1><a id="intro">Лабораторная работа №3</a><br></h1>
<a href="https://docs.github.com/en"><img src="https://img.shields.io/static/v1?logo=github&logoColor=fff&label=&message=Docs&color=36393f&style=flat" alt="GitHub Docs"></a>
<a href="https://daringfireball.net/projects/markdown"><img src="https://img.shields.io/static/v1?logo=markdown&logoColor=fff&label=&message=Markdown&color=36393f&style=flat" alt="Markdown"></a> 
<a href="https://symbl.cc/en/unicode-table"><img src="https://img.shields.io/static/v1?logo=unicode&logoColor=fff&label=&message=Unicode&color=36393f&style=flat" alt="Unicode"></a> 
<a href="https://shields.io"><img src="https://img.shields.io/static/v1?logo=shieldsdotio&logoColor=fff&label=&message=Shields&color=36393f&style=flat" alt="Shields"></a>
<a href="https://img.shields.io/badge/Risk_Analyze-2448a2"><img src="https://img.shields.io/badge/Course-Risk_Analysis-2448a2" alt= "RA"></a> <img src="https://img.shields.io/badge/AppSec-2448a2" alt= "RA"></a> <img src="https://img.shields.io/badge/Contributor-Пасько_И._Д.-8b9aff" alt="Contributor Badge"></a></div>

***

Данная лабораторная работа посвещена изучению `nmap` и как с ним работать. Эта лабораторная работа послужит подпоркой для старта в выявлении и определении уязвимостей на уровне сканера портов, что бы освоить базовые методы сканирования. 

***

## Структура репозитория лабораторной работы

```bash
lab03
.
├── nmapres_new.txt
├── nmapres.txt
├── readme.md
└── reports
    ├── nmapres_new.html
    ├── nmapres_new.txt
    └── nmapres_new.xml
```

***

## Материал

**Nmap Network Mapper** `open-source` утилита для исследования и анализа сетей, в которой основная цель выявление активных устройств, открытых портов, сервисов, версий ПО, ОС и других характеристик, которые способствуют определнию вектора атаки и влияния, а также перехвата управления инфраструктурой или отслеживания. Фактически она рассматривается как виртуальная сетевая карта

- **Методы:**
    - TCP - connect, 
    - TCP SYN - stealth-сканирование, 
    - UDP 
    - FIN 
    - ACK 
    - Xmas tree 
    - NULL-сканирование
    -  ICMP ping
    -  FTP-proxy 
    -  idle scan - невидимое сканирование
    -  и т.д.
- **Возможности:**
    - Определение ОС удалённых хостов с помощью отпечатков TCP/IP-стеков - OS fingerprinting
    - Определение версий сервисов на открытых портах
    - Сканирование сетей с динамическим управлением временем отправки пакетов
    - Выявление пакетных фильтров, межсетевых экранов,маршрутизации и IP-фрагментации
    - Nmap Scripting Engine позволяет автоматизировать поиск уязвимостей SQL Injection и т.д.
    - Может избегать обнаружения, используя ложные хосты и изменение поведения сканера, и т.д.
    - Может сканировать диапазон IP-адресов и множества целей
    - Помогает определить, что открытый порт указывает на то, что служба запущена и ожидает соединений

- **Команды**

```bash
$ nmap -iL targets.txt # множествнные цели сканирований
     -sL # List Scan 
     -sn # Ping Scan 
     -Pn # all hosts online
     -PS/PA/PU/PY[portlist] # TCP SYN/ACK, UDP or SCTP
     -PE/PP/PM # ICMP echo, timestamp, netmask request
     -PO[protocol list] # IP Protocol Ping
     -n/-R # Не для DNS resolution
     --dns-servers <serv1[,serv2],...> # custom DNS
     --system-dns # Используйте OS
     --traceroute 
```

-  **Типы сканирований и опции nmap**

<table>
  <thead>
    <tr>
      <th>Scan type</th>
      <th>nmap option</th>
    </tr>
  </thead>
  <tbody>
    <tr><td>TCP (connect)</td><td>-sT</td></tr>
    <tr><td>TCP SYN</td><td>-sS</td></tr>
    <tr><td>TCP NULL</td><td>-sN</td></tr>
    <tr><td>TCP FIN</td><td>-sF</td></tr>
    <tr><td>TCP XMAS</td><td>-sX</td></tr>
    <tr><td>TCP idle (zombie)</td><td>-sI</td></tr>
    <tr><td>UDP</td><td>-sU</td></tr>
    <tr><td>OS</td><td>-A</td></tr>
  </tbody>
</table>

- **Порты**

<table>
  <thead>
    <tr>
      <th>Port</th>
      <th>Service</th>
      <th>Protocol</th>
    </tr>
  </thead>
  <tbody>
    <tr><td>20/21</td><td>FTP (File Transfer)</td><td>TCP</td></tr>
    <tr><td>22</td><td>SSH (Secure Shell)</td><td>TCP</td></tr>
    <tr><td>23</td><td>Telnet</td><td>TCP</td></tr>
    <tr><td>25</td><td>SMTP (Simple Mail Transfer)</td><td>TCP</td></tr>
    <tr><td>53</td><td>DNS (Domain Name System)</td><td>TCP/UDP</td></tr>
    <tr><td>67/68</td><td>DHCP (Dynamic Host Configuration Protocol)</td><td>UDP</td></tr>
    <tr><td>69</td><td>TFTP (Trivial File Transfer Protocol)</td><td>UDP</td></tr>
    <tr><td>80</td><td>HTTP (Hypertext Transfer Protocol)</td><td>TCP</td></tr>
    <tr><td>110</td><td>POP3 (Post Office Protocol version 3)</td><td>TCP</td></tr>
    <tr><td>443</td><td>HTTPS (HTTP Secure)</td><td>TCP</td></tr>
    <tr><td>3306</td><td>MySQL Database</td><td>TCP</td></tr>
  </tbody>
</table>

***

### Пример результата

```bash
nmap scan report for 10.1.1.10
Host is up, received echo-reply ttl 62 (0.024s latency).
Scanned at 2023-03-06 13:31:28 CET for 573s
Not shown: 993 closed tcp ports (reset)
PORT     STATE SERVICE     REASON         VERSION
22/tcp   open  ssh         syn-ack ttl 62 OpenSSH 8.9p1 Ubuntu 3ubuntu0.1 (Ubuntu Linux; protocol 2.0)
53/tcp   open  domain      syn-ack ttl 62 dnsmasq 2.86
80/tcp   open  http        syn-ack ttl 62 Apache httpd 2.4.52 ((Ubuntu))
139/tcp  open  netbios-ssn syn-ack ttl 62 Samba smbd 4.6.2
445/tcp  open  netbios-ssn syn-ack ttl 62 Samba smbd 4.6.2
631/tcp  open  ipp         syn-ack ttl 62 CUPS 2.4
3306/tcp open  mysql       syn-ack ttl 62 MySQL (unauthorized)
Aggressive OS guesses: HP P2000 G3 NAS device (90%), Linux 2.6.32 - 3.13 (88%), Linux 2.6.32 (88%), Linux 2.6.32 - 3.1 (88%), Ubiquiti AirMax NanoStation WAP (Linux 2.6.32) (88%), Linux 3.7 (88%), Linux 5.1 (88%), Linux 5.4 (88%), Netgear RAIDiator 4.2.21 (Linux 2.6.37) (88%), Ubiquiti Pico Station WAP (AirOS 5.2.6) (88%)
No exact OS matches for host (If you know what OS is running on it, see https://nmap.org/submit/ ).
TCP/IP fingerprint:
OS:SCAN(V=7.93%E=4%D=3/6%OT=22%CT=1%CU=33670%PV=Y%DS=3%DC=I%G=Y%TM=6405DF5D
OS:%P=x86_64-pc-linux-gnu)SEQ(SP=F8%GCD=1%ISR=104%TI=Z%CI=Z%II=I%TS=A)OPS(O
OS:1=M564ST11NW7%O2=M564ST11NW7%O3=M564NNT11NW7%O4=M564ST11NW7%O5=M564ST11N
OS:W7%O6=M564ST11)WIN(W1=FB28%W2=FB28%W3=FB28%W4=FB28%W5=FB28%W6=FB28)ECN(R
OS:=Y%DF=Y%T=40%W=FD5C%O=M564NNSNW7%CC=Y%Q=)T1(R=Y%DF=Y%T=40%S=O%A=S+%F=AS%
OS:RD=0%Q=)T2(R=N)T3(R=N)T4(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)T5(R=Y
OS:%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)T6(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=R
OS:%O=%RD=0%Q=)T7(R=N)U1(R=Y%DF=N%T=40%IPL=164%UN=0%RIPL=G%RID=G%RIPCK=G%RU
OS:CK=11AA%RUD=G)IE(R=Y%DFI=N%T=40%CD=S)
```

***

## Задание

- [✔] 1. Опишите используемые методы по их назначению, как они функционируют и какие результаты могут дать для оценки. Используйте сноску из материалов выше по флагам команд.
- [✔] 2. Выведите на терминале и проанализируйте следующие команды консоли

```bash
$ nmap localhost
$ nmap -sC localhost

$ nmap -p localhost
$ nmap -O localhost

$ nmap -p 80 localhost
$ nmap -p 443 localhost
$ nmap -p 8443 localhost
$ nmap -p "*" localhost
$ nmap -sV -p 22,8080 localhost

$ nmap -sP 192.168.1.0/24
$ nmap --open 192.168.1.1
$ nmap --packet-trace 192.168.1.1
$ nmap --packet-trace scanme.nmap.org 
$ nmap --iflist

$ nmap -iL scanme.nmap.org 
$ nmap -A -iL scanme.nmap.org 
$ nmap -sA scanme.nmap.org
$ nmap -PN scanme.nmap.org 

$ nmap --script=vuln IP_addr -vv
$ nmap -sV --script vuln -oN nmapres_new.txt localhost
$ cat > ./nmapres_new.txt # сделать подобный пример файлу exmp_targets.txt
$ grep "VULNERABLE" nmapres_new.txt

$ mkdir -p ~/project/reports
$ nmap -sV -p 8080 --script vuln -oN ~/project/reports/nmapres_new.txt -oX ~/project/reports/nmapres_new.xml localhost
$ xsltproc ~/project/reports/nmapres_new.xml -o ~/project/reports/nmapres_new.html
```

- [✔] 3. Используйте команду `tree` и выведите все вложенные файлы по директориям.
- [✔] 4.Найдите IP сетевой карты `Ethernet`, которая соответствует вашей виртуальной машине используя `ifconfig` и выполните команду

```bash
$ nmap -sP inet_addr
```

- [✔] 5. Определите ОС, данные ssh, telnet  с помощью `nmap` и выведитео них информацию.
- [✔] 6. Результаты из `nmapres_new.txt` надо перенести в `nmapres.txt` и оставить оба файла рядом в локальном репозитории. Желательно использовать `cp` в консоли через редактор.
- [✔] 7. Оформить `README.md` по аналогии и использовать `shield`, etc.
- [✔] 8. Составить `gist` отчет и отправить ссылку личным сообщением

## Выполнение задания

[✔] 1. Опишите используемые методы по их назначению, как они функционируют и какие результаты могут дать для оценки. Используйте сноску из материалов выше по флагам команд.
- TCP (connect) -sT: реализует полное трёхстороннее рукопожатие через системный вызов connect(): SYN - SYN/ACK - ACK. Возможные результаты: open, closed, filtered.
- TCP SYN -sS: реализует половинчатое рукопожатие через отправку tcp с флагом SYN, ожидание ответа и последующий разрыв соединения. Менее заметен, чем обычный connect() (так как незавершённое соединение реже логируется). Использует raw tcp, требует root. Возможные результаты open, closed, filtered.
- TCP NULL, FIN, XMAS -sN, -sF, -sX: работают по одному принципу, эксплуатируя следующий принцип из RFC 793: любой пакет, не содержащий битов SYN, ACK и RST, должен получить в ответ RST, если порт закрыт, и ничего если открыт. NULL отправляет все флаги = 0, FIN - только FIN (final), XMAS сияет как новогодняя ёлка, отправляя сразу FIN, PSH и URG. Преимущество этого скана в ещё большей незаметности, чем SYN. Недостаток в том, что не все системы чётко следуют RFC 793, поэтому он может не дать полезной информации совсем. Также он не видит разницы между open и filtered. Возможные выводы: open|filtered, closed.
- TCP idle (zombie) -sI: одно из самых скрытных сканирований. Вместо отправки пакетов со своего IP-адреса, Nmap использует другую, "бездействующую" ("зомби") машину. Сканирование осуществляется путем косвенного анализа изменений IP-идентификаторов (IP ID) на "зомби"-хосте, которые вызываются специально сформированными пакетами. Позволяет определить состояние портов (open, closed) на целевой машине, при этом в её логах будет фигурировать IP-адрес "зомби"-хоста, а не сканера. Возможные выводы: open, closed.
- UDP -sU: Сканирование портов по протоколу UDP. Отправляются пустые UDP-датаграммы. Очень медленное (из-за таймаутов на отсутствие ответа) и часто ненадежное, но критически важноe для аудита безопасности, так как многие уязвимости связаны с UDP-сервисами. Выводы: open, open|filtered, closed.
- OS -O: Активное определение операционной системы целевого хоста. Это сложная техника, называемая TCP/IP Stack Fingerprinting (снятие отпечатка стека TCP/IP). Nmap отправляет целую серию специально сконструированных TCP, UDP и ICMP-пакетов на открытые и закрытые порты. Он анализирует десятки параметров в ответах: начальное значение TTL, размер окна TCP, флаги в заголовках, поддержку определенных опций, последовательность номеров пакетов (ISN), реакции на нестандартные запросы. Полученная "сигнатура" сравнивается с обширной эталонной базой данных (nmap-os-db), содержащей отпечатки тысяч версий ОС и сетевых устройств. Результаты: тип ОС, поколение ОС, номер версии, тип устройства, вероятность.
- Aggressive -A: включение одновременно флагов -O, -sV (определение служб), -sC (сканирование скриптами), - --traceroute (определение сетевого пути до хоста).

[✔] 2. Выведите на терминале и проанализируйте следующие команды консоли

```bash
$ nmap localhost # сканирует собственную систему localhost. Использует -sT без root и -sS с root. Сканирует только ~1000 самых частых портов.
i@i8:~/Desktop/lab02$ nmap localhost
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-12-14 02:51 MSK
Nmap scan report for localhost (127.0.0.1)
Host is up (0.00011s latency).
Not shown: 999 closed tcp ports (conn-refused)
PORT    STATE SERVICE
631/tcp open  ipp

$ nmap -sC localhost # всё то же сканирование своей системы, но теперь с применением скриптов. 
По умолчанию используется набор default, который считается безопасным и предоставляет полезную 
дополнительную информацию без агрессивных действий. Также можно написать свой скрипт на Lua.
i@i8:~/Desktop/lab02$ nmap -sC localhost
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-12-14 04:17 MSK
Nmap scan report for localhost (127.0.0.1)
Host is up (0.00012s latency).
Not shown: 999 closed tcp ports (conn-refused)
PORT    STATE SERVICE
631/tcp open  ipp
|_http-title: Home - CUPS 2.4.7
| http-robots.txt: 1 disallowed entry 
|_/

$ nmap -p localhost # вообще флаг -p позволяет выбрать порты для сканирования (конкретные или диапазон),
но здесь синтаксис некорректный, поскольку localhost - это адрес, а не порт, и мы получим ошибку
i@i8:~/Desktop/lab02$ nmap -p localhost
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-12-14 04:18 MSK
Found no matches for the service mask 'localhost' and your specified protocols
QUITTING!

$ nmap -O localhost # сканирование ОС локалхоста
i@i8:~/Desktop/lab02$ sudo nmap -O localhost
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-12-14 04:20 MSK
Nmap scan report for localhost (127.0.0.1)
Host is up (0.00016s latency).
Not shown: 999 closed tcp ports (reset)
PORT    STATE SERVICE
631/tcp open  ipp
Device type: general purpose
Running: Linux 2.6.X
OS CPE: cpe:/o:linux:linux_kernel:2.6.32
OS details: Linux 2.6.32
Network Distance: 0 hops

OS detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 3.05 seconds

$ nmap -p 80 localhost # http
i@i8:~/Desktop/lab02$ nmap -p 80 localhost
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-12-14 04:21 MSK
Nmap scan report for localhost (127.0.0.1)
Host is up (0.000058s latency).

PORT   STATE  SERVICE
80/tcp closed http

Nmap done: 1 IP address (1 host up) scanned in 0.04 seconds

$ nmap -p 443 localhost # https
i@i8:~/Desktop/lab02$ nmap -p 443 localhost
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-12-14 04:21 MSK
Nmap scan report for localhost (127.0.0.1)
Host is up (0.00013s latency).

PORT    STATE  SERVICE
443/tcp closed https

Nmap done: 1 IP address (1 host up) scanned in 0.05 seconds

$ nmap -p 8443 localhost # https-alt
i@i8:~/Desktop/lab02$ nmap -p 8443 localhost
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-12-14 04:21 MSK
Nmap scan report for localhost (127.0.0.1)
Host is up (0.000058s latency).

PORT     STATE  SERVICE
8443/tcp closed https-alt

Nmap done: 1 IP address (1 host up) scanned in 0.05 seconds

$ nmap -p "*" localhost # любые порты localhost
i@i8:~/Desktop/lab02$ sudo nmap -p "*" localhost
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-12-14 04:22 MSK
Nmap scan report for localhost (127.0.0.1)
Host is up (0.0000040s latency).
Not shown: 8367 closed tcp ports (reset)
PORT    STATE SERVICE
631/tcp open  ipp

Nmap done: 1 IP address (1 host up) scanned in 0.44 seconds

$ nmap -sV -p 22,8080 localhost # 22 - ssh, 8080 - http-alt, -sV - сканирование служб
i@i8:~/Desktop/lab02$ nmap -sV -p 22,8080 localhost
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-12-14 04:22 MSK
Nmap scan report for localhost (127.0.0.1)
Host is up (0.000056s latency).

PORT     STATE  SERVICE    VERSION
22/tcp   closed ssh
8080/tcp closed http-proxy

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 0.36 seconds

$ nmap -sP 192.168.1.0/24 # -sP - ping scan (только обнаружение хостов в сети, без скана портов)
i@i8:~/Desktop/lab02$ nmap -sP 192.168.1.0/24
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-12-14 04:23 MSK
Stats: 0:00:13 elapsed; 0 hosts completed (0 up), 256 undergoing Ping Scan
Ping Scan Timing: About 12.70% done; ETC: 04:25 (0:01:29 remaining)
Stats: 0:00:23 elapsed; 0 hosts completed (0 up), 256 undergoing Ping Scan
Ping Scan Timing: About 22.46% done; ETC: 04:25 (0:01:23 remaining)
Nmap done: 256 IP addresses (0 hosts up) scanned in 106.47 seconds

$ nmap --open 192.168.1.1 # --open - показывать только открытые порты
i@i8:~/Desktop/lab02$ sudo nmap --open 192.168.1.1
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-12-14 04:28 MSK
Nmap done: 1 IP address (1 host up) scanned in 4.23 seconds

$ nmap --packet-trace 192.168.1.1 # --packet-trace - показывать сетевой путь каждого пакета
i@i8:~/Desktop/lab02$ sudo nmap --packet-trace 192.168.1.1
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-12-14 04:30 MSK
SENT (0.0624s) ICMP [10.0.2.15 > 192.168.1.1 Echo request (type=8/code=0) id=17827 seq=0] IP [ttl=37 id=18006 iplen=28 ]
SENT (0.0624s) TCP 10.0.2.15:60222 > 192.168.1.1:443 S ttl=40 id=35871 iplen=44  seq=971827825 win=1024 <mss 1460>
SENT (0.0625s) TCP 10.0.2.15:60222 > 192.168.1.1:80 A ttl=48 id=13185 iplen=40  seq=0 win=1024 
SENT (0.0626s) ICMP [10.0.2.15 > 192.168.1.1 Timestamp request (type=13/code=0) id=43711 seq=0 orig=0 recv=0 trans=0] IP [ttl=38 id=34553 iplen=40 ]
RCVD (0.0632s) TCP 192.168.1.1:80 > 10.0.2.15:60222 R ttl=255 id=54794 iplen=40  seq=971827825 win=0 
NSOCK INFO [0.0860s] nsock_iod_new2(): nsock_iod_new (IOD #1)
NSOCK INFO [0.0860s] nsock_connect_udp(): UDP connection requested to 127.0.0.53:53 (IOD #1) EID 8
NSOCK INFO [0.0860s] nsock_read(): Read request from IOD #1 [127.0.0.53:53] (timeout: -1ms) EID 18
NSOCK INFO [0.0860s] nsock_write(): Write request for 42 bytes to IOD #1 EID 27 [127.0.0.53:53]
NSOCK INFO [0.0870s] nsock_trace_handler_callback(): Callback: CONNECT SUCCESS for EID 8 [127.0.0.53:53]
NSOCK INFO [0.0870s] nsock_trace_handler_callback(): Callback: WRITE SUCCESS for EID 27 [127.0.0.53:53]
NSOCK INFO [0.0900s] nsock_trace_handler_callback(): Callback: READ SUCCESS for EID 18 [127.0.0.53:53] (101 bytes)
NSOCK INFO [0.0900s] nsock_read(): Read request from IOD #1 [127.0.0.53:53] (timeout: -1ms) EID 34
NSOCK INFO [0.0900s] nsock_iod_delete(): nsock_iod_delete (IOD #1)
NSOCK INFO [0.0900s] nevent_delete(): nevent_delete on event #34 (type READ)
SENT (0.0977s) TCP 10.0.2.15:60478 > 192.168.1.1:5900 S ttl=59 id=20718 iplen=44  seq=3344034151 win=1024 <mss 1460>
SENT (0.0979s) TCP 10.0.2.15:60478 > 192.168.1.1:110 S ttl=42 id=47485 iplen=44  seq=3344034151 win=1024 <mss 1460>
SENT (0.0980s) TCP 10.0.2.15:60478 > 192.168.1.1:3389 S ttl=39 id=53750 iplen=44  seq=3344034151 win=1024 <mss 1460>
SENT (0.0981s) TCP 10.0.2.15:60478 > 192.168.1.1:25 S ttl=39 id=38049 iplen=44  seq=3344034151 win=1024 <mss 1460>
SENT (0.0982s) TCP 10.0.2.15:60478 > 192.168.1.1:143 S ttl=43 id=38611 iplen=44  seq=3344034151 win=1024 <mss 1460>
...
Nmap scan report for 192.168.1.1
Host is up (0.0010s latency).
All 1000 scanned ports on 192.168.1.1 are in ignored states.
Not shown: 1000 filtered tcp ports (no-response)

Nmap done: 1 IP address (1 host up) scanned in 4.98 seconds

$ nmap --packet-trace scanme.nmap.org
i@i8:~/Desktop/lab02$ sudo nmap --packet-trace scanme.nmap.org 
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-12-14 04:33 MSK
SENT (0.4209s) ICMP [10.0.2.15 > 45.33.32.156 Echo request (type=8/code=0) id=26795 seq=0] IP [ttl=43 id=34039 iplen=28 ]
SENT (0.4212s) TCP 10.0.2.15:43417 > 45.33.32.156:443 S ttl=39 id=8175 iplen=44  seq=4251323482 win=1024 <mss 1460>
SENT (0.4216s) TCP 10.0.2.15:43417 > 45.33.32.156:80 A ttl=46 id=55043 iplen=40  seq=0 win=1024 
SENT (0.4217s) ICMP [10.0.2.15 > 45.33.32.156 Timestamp request (type=13/code=0) id=58703 seq=0 orig=0 recv=0 trans=0] IP [ttl=53 id=55351 iplen=40 ]
RCVD (0.4227s) TCP 45.33.32.156:80 > 10.0.2.15:43417 R ttl=255 id=56896 iplen=40  seq=4251323482 win=0 
NSOCK INFO [0.4530s] nsock_iod_new2(): nsock_iod_new (IOD #1)
NSOCK INFO [0.4530s] nsock_connect_udp(): UDP connection requested to 127.0.0.53:53 (IOD #1) EID 8
NSOCK INFO [0.4540s] nsock_read(): Read request from IOD #1 [127.0.0.53:53] (timeout: -1ms) EID 18
NSOCK INFO [0.4540s] nsock_write(): Write request for 43 bytes to IOD #1 EID 27 [127.0.0.53:53]
NSOCK INFO [0.4550s] nsock_trace_handler_callback(): Callback: CONNECT SUCCESS for EID 8 [127.0.0.53:53]
NSOCK INFO [0.4550s] nsock_trace_handler_callback(): Callback: WRITE SUCCESS for EID 27 [127.0.0.53:53]
NSOCK INFO [0.5840s] nsock_trace_handler_callback(): Callback: READ SUCCESS for EID 18 [127.0.0.53:53] (72 bytes): .G...........156.32.33.45.in-addr.arpa..............,...scanme.nmap.org.
NSOCK INFO [0.5850s] nsock_read(): Read request from IOD #1 [127.0.0.53:53] (timeout: -1ms) EID 34
NSOCK INFO [0.5850s] nsock_iod_delete(): nsock_iod_delete (IOD #1)
NSOCK INFO [0.5850s] nevent_delete(): nevent_delete on event #34 (type READ)
SENT (0.6056s) TCP 10.0.2.15:43673 > 45.33.32.156:1720 S ttl=55 id=5477 iplen=44  seq=1857007112 win=1024 <mss 1460>
SENT (0.6065s) TCP 10.0.2.15:43673 > 45.33.32.156:3389 S ttl=37 id=42866 iplen=44  seq=1857007112 win=1024 <mss 1460>
SENT (0.6073s) TCP 10.0.2.15:43673 > 45.33.32.156:135 S ttl=58 id=3890 iplen=44  seq=1857007112 win=1024 <mss 1460>
...
Nmap scan report for scanme.nmap.org (45.33.32.156)
Host is up (0.054s latency).
Other addresses for scanme.nmap.org (not scanned): 2600:3c01::f03c:91ff:fe18:bb2f
Not shown: 996 filtered tcp ports (no-response)
PORT      STATE SERVICE
22/tcp    open  ssh
80/tcp    open  http
9929/tcp  open  nping-echo
31337/tcp open  Elite

Nmap done: 1 IP address (1 host up) scanned in 12.37 seconds

$ nmap --iflist # показывает все доступные сетевые интерфейсы, а также таблицу маршрутизации ядра ОС
i@i8:~/Desktop/lab02$ sudo nmap --iflist
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-12-14 04:35 MSK
************************INTERFACES************************
DEV    (SHORT)  IP/MASK                                 TYPE     UP MTU   MAC
lo     (lo)     127.0.0.1/8                             loopback up 65536
lo     (lo)     ::1/128                                 loopback up 65536
enp0s3 (enp0s3) 10.0.2.15/24                            ethernet up 1500  08:00:27:F4:7E:83
enp0s3 (enp0s3) fd17:625c:f037:2:8331:297f:2cf6:ff2d/64 ethernet up 1500  08:00:27:F4:7E:83
enp0s3 (enp0s3) fe80::a00:27ff:fef4:7e83/64             ethernet up 1500  08:00:27:F4:7E:83
enp0s3 (enp0s3) fd17:625c:f037:2:a00:27ff:fef4:7e83/64  ethernet up 1500  08:00:27:F4:7E:83

**************************ROUTES**************************
DST/MASK                                 DEV    METRIC GATEWAY
10.0.2.0/24                              enp0s3 100
0.0.0.0/0                                enp0s3 100    10.0.2.2
::1/128                                  lo     0
fd17:625c:f037:2:a00:27ff:fef4:7e83/128  enp0s3 0
fd17:625c:f037:2:8331:297f:2cf6:ff2d/128 enp0s3 0
fe80::a00:27ff:fef4:7e83/128             enp0s3 0
fd17:625c:f037:2::/64                    enp0s3 256
fe80::/64                                enp0s3 256
ff00::/8                                 enp0s3 256
::/0                                     enp0s3 1024   fe80::2

$ nmap -iL scanme.nmap.org # сканирование списка целей из текстового файла (здесь синтаксис неверен, будет ошибка)
i@i8:~/Desktop/lab03$ sudo nmap -iL scanme.nmap.org 
Failed to open input file scanme.nmap.org for reading: No such file or directory (2)

$ nmap -A -iL scanme.nmap.org # (ошибка)
i@i8:~/Desktop/lab03$ sudo nmap -A -iL scanme.nmap.org
Failed to open input file scanme.nmap.org for reading: No such file or directory (2)

$ nmap -sA scanme.nmap.org # -sA: ACK-сканирование, используется для проверки на filtered/unfiltered = выявления правил работы файервола
i@i8:~/Desktop/lab03$ sudo nmap -sA scanme.nmap.org
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-12-14 05:09 MSK
Nmap scan report for scanme.nmap.org (45.33.32.156)
Host is up (0.00035s latency).
Other addresses for scanme.nmap.org (not scanned): 2600:3c01::f03c:91ff:fe18:bb2f
All 1000 scanned ports on scanme.nmap.org (45.33.32.156) are in ignored states.
Not shown: 1000 unfiltered tcp ports (reset)

Nmap done: 1 IP address (1 host up) scanned in 0.75 seconds

$ nmap -PN scanme.nmap.org # -PN (-Pn): No ping scan, сразу сканирует порты, не проверяя что хост живой
i@i8:~/Desktop/lab03$ sudo nmap -PN scanme.nmap.org 
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-12-14 05:10 MSK
Nmap scan report for scanme.nmap.org (45.33.32.156)
Host is up (0.19s latency).
Other addresses for scanme.nmap.org (not scanned): 2600:3c01::f03c:91ff:fe18:bb2f
Not shown: 996 filtered tcp ports (no-response)
PORT      STATE SERVICE
22/tcp    open  ssh
80/tcp    open  http
9929/tcp  open  nping-echo
31337/tcp open  Elite

Nmap done: 1 IP address (1 host up) scanned in 13.97 seconds

$ nmap --script=vuln IP_addr -vv # --script=vuln - запуск скриптов категории "уязвимости", -vv - очень детальный вывод
$ nmap -sV --script vuln -oN nmapres_new.txt localhost
i@i8:~/Desktop/lab03$ sudo nmap -sV --script=vuln -oN nmapres_new.txt localhost
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-12-14 05:34 MSK
Nmap scan report for localhost (127.0.0.1)
Host is up (0.0000070s latency).
Not shown: 999 closed tcp ports (reset)
PORT    STATE SERVICE VERSION
631/tcp open  ipp     CUPS 2.4
| http-slowloris-check: 
|   VULNERABLE:
|   Slowloris DOS attack
|     State: LIKELY VULNERABLE
|     IDs:  CVE:CVE-2007-6750
|       Slowloris tries to keep many connections to the target web server open and hold
|       them open as long as possible.  It accomplishes this by opening connections to
|       the target web server and sending a partial request. By doing so, it starves
|       the http server's resources causing Denial Of Service.
|       
|     Disclosure date: 2009-09-17
|     References:
|       http://ha.ckers.org/slowloris/
|_      https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2007-6750
| vulners: 
|   CUPS 2.4: 
|     	MSF:EXPLOIT-MULTI-MISC-CUPS_IPP_REMOTE_CODE_EXECUTION-	9.8	https://vulners.com/metasploit/MSF:EXPLOIT-MULTI-MISC-CUPS_IPP_REMOTE_CODE_EXECUTION-	*EXPLOIT*
|     	1337DAY-ID-39819	9.0	https://vulners.com/zdt/1337DAY-ID-39819*EXPLOIT*
|     	PACKETSTORM:182767	8.6	https://vulners.com/packetstorm/PACKETSTORM:182767	*EXPLOIT*
|     	6D7EB122-6604-5374-B851-DA56ABDA1F34	8.6	https://vulners.com/githubexploit/6D7EB122-6604-5374-B851-DA56ABDA1F34	*EXPLOIT*
|     	34D7D370-3683-5358-9692-BB0B5AF7F412	8.6	https://vulners.com/githubexploit/34D7D370-3683-5358-9692-BB0B5AF7F412	*EXPLOIT*
|     	CVE-2024-47850	7.5	https://vulners.com/cve/CVE-2024-47850
|     	MSF:AUXILIARY-SCANNER-MISC-CUPS_BROWSED_INFO_DISCLOSURE-	5.3	https://vulners.com/metasploit/MSF:AUXILIARY-SCANNER-MISC-CUPS_BROWSED_INFO_DISCLOSURE-	*EXPLOIT*
|     	F5502B30-710E-5D69-B67C-937F75899289	5.3	https://vulners.com/githubexploit/F5502B30-710E-5D69-B67C-937F75899289	*EXPLOIT*
|     	D0B85558-0ED9-5259-A56D-4C807CC07FCF	5.3	https://vulners.com/githubexploit/D0B85558-0ED9-5259-A56D-4C807CC07FCF	*EXPLOIT*
|     	ADDB422D-CF88-55B8-BA36-EC2BAC7507A0	5.3	https://vulners.com/githubexploit/ADDB422D-CF88-55B8-BA36-EC2BAC7507A0	*EXPLOIT*
|     	9DB4B6B1-3FB0-5827-B554-3F3779D23B09	5.3	https://vulners.com/githubexploit/9DB4B6B1-3FB0-5827-B554-3F3779D23B09	*EXPLOIT*
|_    	48FAED93-C711-59A0-B81E-A65D4463C7F0	5.3	https://vulners.com/githubexploit/48FAED93-C711-59A0-B81E-A65D4463C7F0	*EXPLOIT*
|_http-aspnet-debug: ERROR: Script execution failed (use -d to debug)
|_http-server-header: CUPS/2.4 IPP/2.1
| http-enum: 
|   /admin.php: Possible admin folder (401 Unauthorized)
|   /admin/: Possible admin folder (401 Unauthorized)
|   /admin/admin/: Possible admin folder (401 Unauthorized)
|   /administrator/: Possible admin folder (401 Unauthorized)
|   /adminarea/: Possible admin folder (401 Unauthorized)
|   /adminLogin/: Possible admin folder (401 Unauthorized)
|   /admin_area/: Possible admin folder (401 Unauthorized)
|   /administratorlogin/: Possible admin folder (401 Unauthorized)
|   /admin/account.php: Possible admin folder (401 Unauthorized)
|   /admin/index.php: Possible admin folder (401 Unauthorized)
|   /admin/login.php: Possible admin folder (401 Unauthorized)
|   /admin/admin.php: Possible admin folder (401 Unauthorized)
|   /admin_area/admin.php: Possible admin folder (401 Unauthorized)
|   /admin_area/login.php: Possible admin folder (401 Unauthorized)
|   /admin/index.html: Possible admin folder (401 Unauthorized)
|   /admin/login.html: Possible admin folder (401 Unauthorized)
|   /admin/admin.html: Possible admin folder (401 Unauthorized)
|   /admin_area/index.php: Possible admin folder (401 Unauthorized)
|   /admin/home.php: Possible admin folder (401 Unauthorized)
|   /admin_area/login.html: Possible admin folder (401 Unauthorized)
|   /admin_area/index.html: Possible admin folder (401 Unauthorized)
|   /admin/controlpanel.php: Possible admin folder (401 Unauthorized)
|   /admincp/: Possible admin folder (401 Unauthorized)
|   /admincp/index.asp: Possible admin folder (401 Unauthorized)
|   /admincp/index.html: Possible admin folder (401 Unauthorized)
|   /admincp/login.php: Possible admin folder (401 Unauthorized)
|   /admin/account.html: Possible admin folder (401 Unauthorized)
|   /adminpanel.html: Possible admin folder (401 Unauthorized)
|   /admin/admin_login.html: Possible admin folder (401 Unauthorized)
|   /admin_login.html: Possible admin folder (401 Unauthorized)
|   /admin/cp.php: Possible admin folder (401 Unauthorized)
|   /administrator/index.php: Possible admin folder (401 Unauthorized)
|   /administrator/login.php: Possible admin folder (401 Unauthorized)
|   /admin/admin_login.php: Possible admin folder (401 Unauthorized)
|   /admin_login.php: Possible admin folder (401 Unauthorized)
|   /administrator/account.php: Possible admin folder (401 Unauthorized)
|   /administrator.php: Possible admin folder (401 Unauthorized)
|   /admin_area/admin.html: Possible admin folder (401 Unauthorized)
|   /admin/admin-login.php: Possible admin folder (401 Unauthorized)
|   /admin-login.php: Possible admin folder (401 Unauthorized)
|   /admin/home.html: Possible admin folder (401 Unauthorized)
|   /admin/admin-login.html: Possible admin folder (401 Unauthorized)
|   /admin-login.html: Possible admin folder (401 Unauthorized)
|   /admincontrol.php: Possible admin folder (401 Unauthorized)
|   /admin/adminLogin.html: Possible admin folder (401 Unauthorized)
|   /adminLogin.html: Possible admin folder (401 Unauthorized)
|   /adminarea/index.html: Possible admin folder (401 Unauthorized)
|   /adminarea/admin.html: Possible admin folder (401 Unauthorized)
|   /admin/controlpanel.html: Possible admin folder (401 Unauthorized)
|   /admin.html: Possible admin folder (401 Unauthorized)
|   /admin/cp.html: Possible admin folder (401 Unauthorized)
|   /adminpanel.php: Possible admin folder (401 Unauthorized)
|   /administrator/index.html: Possible admin folder (401 Unauthorized)
|   /administrator/login.html: Possible admin folder (401 Unauthorized)
|   /administrator/account.html: Possible admin folder (401 Unauthorized)
|   /administrator.html: Possible admin folder (401 Unauthorized)
|   /adminarea/login.html: Possible admin folder (401 Unauthorized)
|   /admincontrol/login.html: Possible admin folder (401 Unauthorized)
|   /admincontrol.html: Possible admin folder (401 Unauthorized)
|   /adminLogin.php: Possible admin folder (401 Unauthorized)
|   /admin/adminLogin.php: Possible admin folder (401 Unauthorized)
|   /adminarea/index.php: Possible admin folder (401 Unauthorized)
|   /adminarea/admin.php: Possible admin folder (401 Unauthorized)
|   /adminarea/login.php: Possible admin folder (401 Unauthorized)
|   /admincontrol/login.php: Possible admin folder (401 Unauthorized)
|   /admin2.php: Possible admin folder (401 Unauthorized)
|   /admin2/login.php: Possible admin folder (401 Unauthorized)
|   /admin2/index.php: Possible admin folder (401 Unauthorized)
|   /administratorlogin.php: Possible admin folder (401 Unauthorized)
|   /admin/account.cfm: Possible admin folder (401 Unauthorized)
|   /admin/index.cfm: Possible admin folder (401 Unauthorized)
|   /admin/login.cfm: Possible admin folder (401 Unauthorized)
|   /admin/admin.cfm: Possible admin folder (401 Unauthorized)
|   /admin.cfm: Possible admin folder (401 Unauthorized)
|   /admin/admin_login.cfm: Possible admin folder (401 Unauthorized)
|   /admin_login.cfm: Possible admin folder (401 Unauthorized)
|   /adminpanel.cfm: Possible admin folder (401 Unauthorized)
|   /admin/controlpanel.cfm: Possible admin folder (401 Unauthorized)
|   /admincontrol.cfm: Possible admin folder (401 Unauthorized)
|   /admin/cp.cfm: Possible admin folder (401 Unauthorized)
|   /admincp/index.cfm: Possible admin folder (401 Unauthorized)
|   /admincp/login.cfm: Possible admin folder (401 Unauthorized)
|   /admin_area/admin.cfm: Possible admin folder (401 Unauthorized)
|   /admin_area/login.cfm: Possible admin folder (401 Unauthorized)
|   /administrator/login.cfm: Possible admin folder (401 Unauthorized)
|   /administratorlogin.cfm: Possible admin folder (401 Unauthorized)
|   /administrator.cfm: Possible admin folder (401 Unauthorized)
|   /administrator/account.cfm: Possible admin folder (401 Unauthorized)
|   /adminLogin.cfm: Possible admin folder (401 Unauthorized)
|   /admin2/index.cfm: Possible admin folder (401 Unauthorized)
|   /admin_area/index.cfm: Possible admin folder (401 Unauthorized)
|   /admin2/login.cfm: Possible admin folder (401 Unauthorized)
|   /admincontrol/login.cfm: Possible admin folder (401 Unauthorized)
|   /administrator/index.cfm: Possible admin folder (401 Unauthorized)
|   /adminarea/login.cfm: Possible admin folder (401 Unauthorized)
|   /adminarea/admin.cfm: Possible admin folder (401 Unauthorized)
|   /adminarea/index.cfm: Possible admin folder (401 Unauthorized)
|   /admin/adminLogin.cfm: Possible admin folder (401 Unauthorized)
|   /admin-login.cfm: Possible admin folder (401 Unauthorized)
|   /admin/admin-login.cfm: Possible admin folder (401 Unauthorized)
|   /admin/home.cfm: Possible admin folder (401 Unauthorized)
|   /admin/account.asp: Possible admin folder (401 Unauthorized)
|   /admin/index.asp: Possible admin folder (401 Unauthorized)
|   /admin/login.asp: Possible admin folder (401 Unauthorized)
|   /admin/admin.asp: Possible admin folder (401 Unauthorized)
|   /admin_area/admin.asp: Possible admin folder (401 Unauthorized)
|   /admin_area/login.asp: Possible admin folder (401 Unauthorized)
|   /admin_area/index.asp: Possible admin folder (401 Unauthorized)
|   /admin/home.asp: Possible admin folder (401 Unauthorized)
|   /admin/controlpanel.asp: Possible admin folder (401 Unauthorized)
|   /admin.asp: Possible admin folder (401 Unauthorized)
|   /admin/admin-login.asp: Possible admin folder (401 Unauthorized)
|   /admin-login.asp: Possible admin folder (401 Unauthorized)
|   /admin/cp.asp: Possible admin folder (401 Unauthorized)
|   /administrator/account.asp: Possible admin folder (401 Unauthorized)
|   /administrator.asp: Possible admin folder (401 Unauthorized)
|   /administrator/login.asp: Possible admin folder (401 Unauthorized)
|   /admincp/login.asp: Possible admin folder (401 Unauthorized)
|   /admincontrol.asp: Possible admin folder (401 Unauthorized)
|   /adminpanel.asp: Possible admin folder (401 Unauthorized)
|   /admin/admin_login.asp: Possible admin folder (401 Unauthorized)
|   /admin_login.asp: Possible admin folder (401 Unauthorized)
|   /adminLogin.asp: Possible admin folder (401 Unauthorized)
|   /admin/adminLogin.asp: Possible admin folder (401 Unauthorized)
|   /adminarea/index.asp: Possible admin folder (401 Unauthorized)
|   /adminarea/admin.asp: Possible admin folder (401 Unauthorized)
|   /adminarea/login.asp: Possible admin folder (401 Unauthorized)
|   /administrator/index.asp: Possible admin folder (401 Unauthorized)
|   /admincontrol/login.asp: Possible admin folder (401 Unauthorized)
|   /admin2.asp: Possible admin folder (401 Unauthorized)
|   /admin2/login.asp: Possible admin folder (401 Unauthorized)
|   /admin2/index.asp: Possible admin folder (401 Unauthorized)
|   /administratorlogin.asp: Possible admin folder (401 Unauthorized)
|   /admin/account.aspx: Possible admin folder (401 Unauthorized)
|   /admin/index.aspx: Possible admin folder (401 Unauthorized)
|   /admin/login.aspx: Possible admin folder (401 Unauthorized)
|   /admin/admin.aspx: Possible admin folder (401 Unauthorized)
|   /admin_area/admin.aspx: Possible admin folder (401 Unauthorized)
|   /admin_area/login.aspx: Possible admin folder (401 Unauthorized)
|   /admin_area/index.aspx: Possible admin folder (401 Unauthorized)
|   /admin/home.aspx: Possible admin folder (401 Unauthorized)
|   /admin/controlpanel.aspx: Possible admin folder (401 Unauthorized)
|   /admin.aspx: Possible admin folder (401 Unauthorized)
|   /admin/admin-login.aspx: Possible admin folder (401 Unauthorized)
|   /admin-login.aspx: Possible admin folder (401 Unauthorized)
|   /admin/cp.aspx: Possible admin folder (401 Unauthorized)
|   /administrator/account.aspx: Possible admin folder (401 Unauthorized)
|   /administrator.aspx: Possible admin folder (401 Unauthorized)
|   /administrator/login.aspx: Possible admin folder (401 Unauthorized)
|   /admincp/index.aspx: Possible admin folder (401 Unauthorized)
|   /admincp/login.aspx: Possible admin folder (401 Unauthorized)
|   /admincontrol.aspx: Possible admin folder (401 Unauthorized)
|   /adminpanel.aspx: Possible admin folder (401 Unauthorized)
|   /admin/admin_login.aspx: Possible admin folder (401 Unauthorized)
|   /admin_login.aspx: Possible admin folder (401 Unauthorized)
|   /adminLogin.aspx: Possible admin folder (401 Unauthorized)
|   /admin/adminLogin.aspx: Possible admin folder (401 Unauthorized)
|   /adminarea/index.aspx: Possible admin folder (401 Unauthorized)
|   /adminarea/admin.aspx: Possible admin folder (401 Unauthorized)
|   /adminarea/login.aspx: Possible admin folder (401 Unauthorized)
|   /administrator/index.aspx: Possible admin folder (401 Unauthorized)
|   /admincontrol/login.aspx: Possible admin folder (401 Unauthorized)
|   /admin2.aspx: Possible admin folder (401 Unauthorized)
|   /admin2/login.aspx: Possible admin folder (401 Unauthorized)
|   /admin2/index.aspx: Possible admin folder (401 Unauthorized)
|   /administratorlogin.aspx: Possible admin folder (401 Unauthorized)
|   /admin/index.jsp: Possible admin folder (401 Unauthorized)
|   /admin/login.jsp: Possible admin folder (401 Unauthorized)
|   /admin/admin.jsp: Possible admin folder (401 Unauthorized)
|   /admin_area/admin.jsp: Possible admin folder (401 Unauthorized)
|   /admin_area/login.jsp: Possible admin folder (401 Unauthorized)
|   /admin_area/index.jsp: Possible admin folder (401 Unauthorized)
|   /admin/home.jsp: Possible admin folder (401 Unauthorized)
|   /admin/controlpanel.jsp: Possible admin folder (401 Unauthorized)
|   /admin.jsp: Possible admin folder (401 Unauthorized)
|   /admin/admin-login.jsp: Possible admin folder (401 Unauthorized)
|   /admin-login.jsp: Possible admin folder (401 Unauthorized)
|   /admin/cp.jsp: Possible admin folder (401 Unauthorized)
|   /administrator/account.jsp: Possible admin folder (401 Unauthorized)
|   /administrator.jsp: Possible admin folder (401 Unauthorized)
|   /administrator/login.jsp: Possible admin folder (401 Unauthorized)
|   /admincp/index.jsp: Possible admin folder (401 Unauthorized)
|   /admincp/login.jsp: Possible admin folder (401 Unauthorized)
|   /admincontrol.jsp: Possible admin folder (401 Unauthorized)
|   /admin/account.jsp: Possible admin folder (401 Unauthorized)
|   /adminpanel.jsp: Possible admin folder (401 Unauthorized)
|   /admin/admin_login.jsp: Possible admin folder (401 Unauthorized)
|   /admin_login.jsp: Possible admin folder (401 Unauthorized)
|   /adminLogin.jsp: Possible admin folder (401 Unauthorized)
|   /admin/adminLogin.jsp: Possible admin folder (401 Unauthorized)
|   /adminarea/index.jsp: Possible admin folder (401 Unauthorized)
|   /adminarea/admin.jsp: Possible admin folder (401 Unauthorized)
|   /adminarea/login.jsp: Possible admin folder (401 Unauthorized)
|   /administrator/index.jsp: Possible admin folder (401 Unauthorized)
|   /admincontrol/login.jsp: Possible admin folder (401 Unauthorized)
|   /admin2.jsp: Possible admin folder (401 Unauthorized)
|   /admin2/login.jsp: Possible admin folder (401 Unauthorized)
|   /admin2/index.jsp: Possible admin folder (401 Unauthorized)
|   /administratorlogin.jsp: Possible admin folder (401 Unauthorized)
|   /admin1.php: Possible admin folder (401 Unauthorized)
|   /administr8.asp: Possible admin folder (401 Unauthorized)
|   /administr8.php: Possible admin folder (401 Unauthorized)
|   /administr8.jsp: Possible admin folder (401 Unauthorized)
|   /administr8.aspx: Possible admin folder (401 Unauthorized)
|   /administr8.cfm: Possible admin folder (401 Unauthorized)
|   /administr8/: Possible admin folder (401 Unauthorized)
|   /administer/: Possible admin folder (401 Unauthorized)
|   /administracao.php: Possible admin folder (401 Unauthorized)
|   /administracao.asp: Possible admin folder (401 Unauthorized)
|   /administracao.aspx: Possible admin folder (401 Unauthorized)
|   /administracao.cfm: Possible admin folder (401 Unauthorized)
|   /administracao.jsp: Possible admin folder (401 Unauthorized)
|   /administracion.php: Possible admin folder (401 Unauthorized)
|   /administracion.asp: Possible admin folder (401 Unauthorized)
|   /administracion.aspx: Possible admin folder (401 Unauthorized)
|   /administracion.jsp: Possible admin folder (401 Unauthorized)
|   /administracion.cfm: Possible admin folder (401 Unauthorized)
|   /administrators/: Possible admin folder (401 Unauthorized)
|   /adminpro/: Possible admin folder (401 Unauthorized)
|   /admins/: Possible admin folder (401 Unauthorized)
|   /admins.cfm: Possible admin folder (401 Unauthorized)
|   /admins.php: Possible admin folder (401 Unauthorized)
|   /admins.jsp: Possible admin folder (401 Unauthorized)
|   /admins.asp: Possible admin folder (401 Unauthorized)
|   /admins.aspx: Possible admin folder (401 Unauthorized)
|   /administracion-sistema/: Possible admin folder (401 Unauthorized)
|   /admin108/: Possible admin folder (401 Unauthorized)
|   /admin_cp.asp: Possible admin folder (401 Unauthorized)
|   /admin/backup/: Possible backup (401 Unauthorized)
|   /admin/download/backup.sql: Possible database backup (401 Unauthorized)
|   /robots.txt: Robots file
|   /admin/upload.php: Admin File Upload (401 Unauthorized)
|   /admin/CiscoAdmin.jhtml: Cisco Collaboration Server (401 Unauthorized)
|   /admin-console/: JBoss Console (401 Unauthorized)
|   /admin4.nsf: Lotus Domino (401 Unauthorized)
|   /admin5.nsf: Lotus Domino (401 Unauthorized)
|   /admin.nsf: Lotus Domino (401 Unauthorized)
|   /administrator/wp-login.php: Wordpress login page. (401 Unauthorized)
|   /admin/libraries/ajaxfilemanager/ajaxfilemanager.php: Log1 CMS (401 Unauthorized)
|   /admin/view/javascript/fckeditor/editor/filemanager/connectors/test.html: OpenCart/FCKeditor File upload (401 Unauthorized)
|   /admin/includes/tiny_mce/plugins/tinybrowser/upload.php: CompactCMS or B-Hind CMS/FCKeditor File upload (401 Unauthorized)
|   /admin/includes/FCKeditor/editor/filemanager/upload/test.html: ASP Simple Blog / FCKeditor File Upload (401 Unauthorized)
|   /admin/jscript/upload.php: Lizard Cart/Remote File upload (401 Unauthorized)
|   /admin/jscript/upload.html: Lizard Cart/Remote File upload (401 Unauthorized)
|   /admin/jscript/upload.pl: Lizard Cart/Remote File upload (401 Unauthorized)
|   /admin/jscript/upload.asp: Lizard Cart/Remote File upload (401 Unauthorized)
|   /admin/environment.xml: Moodle files (401 Unauthorized)
|   /classes/: Potentially interesting folder
|   /es/: Potentially interesting folder
|   /help/: Potentially interesting folder
|_  /printers/: Potentially interesting folder

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 529.24 seconds

$ cat > ./nmapres_new.txt # уже создан в предыдущем пункте
$ grep "VULNERABLE" nmapres_new.txt
i@i8:~/Desktop/lab03$ grep "VULNERABLE" nmapres_new.txt
|   VULNERABLE:
|     State: LIKELY VULNERABLE


$ mkdir -p ~/project/reports
$ nmap -sV -p 8080 --script vuln -oN ~/project/reports/nmapres_new.txt -oX ~/project/reports/nmapres_new.xml localhost
$ xsltproc ~/project/reports/nmapres_new.xml -o ~/project/reports/nmapres_new.html
i@i8:~/Desktop/lab03$ mkdir -p ~/project/reports
i@i8:~/Desktop/lab03$ sudo nmap -sV -p 8080 --script vuln -oN ~/project/reports/nmapres_new.txt -oX ~/project/reports/nmapres_new.xml localhost
[sudo] password for i: 
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-12-14 05:58 MSK
Nmap scan report for localhost (127.0.0.1)
Host is up (0.00011s latency).

PORT     STATE  SERVICE    VERSION
8080/tcp closed http-proxy

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 10.63 seconds
i@i8:~/Desktop/lab03$ sudo xsltproc ~/project/reports/nmapres_new.xml -o ~/project/reports/nmapres_new.html
```

[✔] 3. Используйте команду `tree` и выведите все вложенные файлы по директориям.
```bash
i@i8:~/Desktop/lab03$ tree
.
├── nmapres_new.txt
├── nmapres.txt
└── reports
    ├── nmapres_new.html
    ├── nmapres_new.txt
    └── nmapres_new.xml
```
- 
[✔] 4.Найдите IP сетевой карты `Ethernet`, которая соответствует вашей виртуальной машине используя `ifconfig` и выполните команду
```bash
$ nmap -sP inet_addr
i@i8:~/project/reports$ nmap --iflist
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-12-14 06:07 MSK
************************INTERFACES************************
DEV    (SHORT)  IP/MASK                                 TYPE     UP MTU   MAC
lo     (lo)     127.0.0.1/8                             loopback up 65536
lo     (lo)     ::1/128                                 loopback up 65536
enp0s3 (enp0s3) 10.0.2.15/24                            ethernet up 1500  08:00:27:F4:7E:83
enp0s3 (enp0s3) fd17:625c:f037:2:8331:297f:2cf6:ff2d/64 ethernet up 1500  08:00:27:F4:7E:83
enp0s3 (enp0s3) fe80::a00:27ff:fef4:7e83/64             ethernet up 1500  08:00:27:F4:7E:83
enp0s3 (enp0s3) fd17:625c:f037:2:a00:27ff:fef4:7e83/64  ethernet up 1500  08:00:27:F4:7E:83

**************************ROUTES**************************
DST/MASK                                 DEV    METRIC GATEWAY
10.0.2.0/24                              enp0s3 100
0.0.0.0/0                                enp0s3 100    10.0.2.2
::1/128                                  lo     0
fd17:625c:f037:2:a00:27ff:fef4:7e83/128  enp0s3 0
fd17:625c:f037:2:8331:297f:2cf6:ff2d/128 enp0s3 0
fe80::a00:27ff:fef4:7e83/128             enp0s3 0
fd17:625c:f037:2::/64                    enp0s3 256
fe80::/64                                enp0s3 256
ff00::/8                                 enp0s3 256
::/0                                     enp0s3 1024   fe80::2

i@i8:~/project/reports$ sudo nmap -sP 10.0.02.15/24
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-12-14 06:09 MSK
Nmap scan report for _gateway (10.0.2.2)
Host is up (0.00029s latency).
MAC Address: 52:55:0A:00:02:02 (Unknown)
Nmap scan report for 10.0.2.3
Host is up (0.00029s latency).
MAC Address: 52:55:0A:00:02:03 (Unknown)
Nmap scan report for i8 (10.0.2.15)
Host is up.
Nmap done: 256 IP addresses (3 hosts up) scanned in 2.02 seconds

```


[✔] 5. Определите ОС, данные ssh, telnet  с помощью `nmap` и выведитео них информацию.
```bash
i@i8:~/project/reports$ sudo nmap -O localhost
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-12-14 06:11 MSK
Nmap scan report for localhost (127.0.0.1)
Host is up (0.00013s latency).
Not shown: 999 closed tcp ports (reset)
PORT    STATE SERVICE
631/tcp open  ipp
Device type: general purpose
Running: Linux 2.6.X
OS CPE: cpe:/o:linux:linux_kernel:2.6.32
OS details: Linux 2.6.32
Network Distance: 0 hops

OS detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 2.22 seconds

i@i8:~/project/reports$ sudo nmap -p 22,23 localhost
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-12-14 06:12 MSK
Nmap scan report for localhost (127.0.0.1)
Host is up (0.000028s latency).

PORT   STATE  SERVICE
22/tcp closed ssh
23/tcp closed telnet

Nmap done: 1 IP address (1 host up) scanned in 0.09 seconds
```

[✔] 6. Результаты из `nmapres_new.txt` надо перенести в `nmapres.txt` и оставить оба файла рядом в локальном репозитории. Желательно использовать `cp` в консоли через редактор.
```bash
i@i8:~/Desktop/lab03$ cp nmapres_new.txt nmapres.txt 
```
[✔] 7. Оформить `README.md` по аналогии и использовать `shield`, etc.
[✔] 8. Составить `gist` отчет и отправить ссылку личным сообщением

***
