# Домашнее задание к занятию "3.6. Компьютерные сети, лекция 1"

1. Работа c HTTP через телнет.
- Подключитесь утилитой телнет к сайту stackoverflow.com
`telnet stackoverflow.com 80`
- отправьте HTTP запрос
```bash
GET /questions HTTP/1.0
HOST: stackoverflow.com
[press enter]
[press enter]
```
- В ответе укажите полученный HTTP код, что он означает?

```
us@ubuntu:~$ telnet stackoverflow.com 80
Trying 151.101.65.69...
Connected to stackoverflow.com.
Escape character is '^]'.
GET /questions HTTP/1.0
HOST: stackoverflow.com

HTTP/1.1 301 Moved Permanently
cache-control: no-cache, no-store, must-revalidate
location: https://stackoverflow.com/questions
x-request-guid: f4ff15e2-aa2d-49ae-99a3-a5c61f2013ce
feature-policy: microphone 'none'; speaker 'none'
content-security-policy: upgrade-insecure-requests; frame-ancestors 'self' https://stackexchange.com
Accept-Ranges: bytes
Date: Fri, 03 Dec 2021 15:21:31 GMT
Via: 1.1 varnish
Connection: close
X-Served-By: cache-ams21076-AMS
X-Cache: MISS
X-Cache-Hits: 0
X-Timer: S1638544892.586027,VS0,VE75
Vary: Fastly-SSL
X-DNS-Prefetch-Control: off
Set-Cookie: prov=846d8bdd-144f-855f-6797-d9a6d2858952; domain=.stackoverflow.com; expires=Fri, 01-Jan-2055 00:00:00 GMT; path=/; HttpOnly

Connection closed by foreign host.
```
Код 301 говорит что запрошенный ресурс окончательно переехал по адресу указанному в строке: 
`location: https://stackoverflow.com/questions`

---

2. Повторите задание 1 в браузере, используя консоль разработчика F12.
- откройте вкладку `Network`
- отправьте запрос http://stackoverflow.com
- найдите первый ответ HTTP сервера, откройте вкладку `Headers`
- укажите в ответе полученный HTTP код.
- проверьте время загрузки страницы, какой запрос обрабатывался дольше всего?
- приложите скриншот консоли браузера в ответ.

Первый ответ http:
```
Request URL: http://stackoverflow.com/questions
Request Method: GET
Status Code: 307 Internal Redirect
Referrer Policy: strict-origin-when-cross-origin
Location: https://stackoverflow.com/questions
Non-Authoritative-Reason: HSTS
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
DNT: 1
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/96.0.4664.45 Safari/537.36
``` 
Дольше всего обрабатывался запрос questions(самый первый) если не считать ошибок с какими-то скриптами. Указан на скрине ниже.  
![Картинка screen1](img/screen1.jpg)

---

3. Какой IP адрес у вас в интернете?
![Картинка screen3](img/screen3.jpg)

---

4. Какому провайдеру принадлежит ваш IP адрес? Какой автономной системе AS? Воспользуйтесь утилитой `whois`  

```
netname:        DISKUS-TELECOM
origin:         AS197831

```

---

5. Через какие сети проходит пакет, отправленный с вашего компьютера на адрес 8.8.8.8? Через какие AS? Воспользуйтесь утилитой `traceroute`  

```
us@ubuntu:~$ traceroute -An 8.8.8.8
traceroute to 8.8.8.8 (8.8.8.8), 30 hops max, 60 byte packets
 1  192.168.5.2 [*]  1.435 ms  1.172 ms  1.026 ms
 2  80.89.151.XXX [AS21127/AS20485]  1.776 ms  2.007 ms  2.095 ms
 3  188.43.12.201 [AS20485]  2.941 ms  2.885 ms  3.049 ms
 4  188.43.12.202 [AS20485]  3.181 ms  3.437 ms  3.455 ms
 5  217.150.55.234 [AS20485]  42.910 ms  42.853 ms  42.797 ms
 6  188.43.10.141 [AS20485]  42.741 ms  42.854 ms  42.776 ms
 7  108.170.250.99 [AS15169]  42.875 ms 108.170.250.66 [AS15169]  38.324 ms  40.472 ms
 8  172.253.66.116 [AS15169]  52.704 ms * 142.251.49.24 [AS15169]  49.173 ms
 9  74.125.253.94 [AS15169]  48.595 ms 74.125.253.109 [AS15169]  52.118 ms 172.253.65.82 [AS15169]  62.776 ms
10  216.239.47.167 [AS15169]  47.733 ms 216.239.46.139 [AS15169]  49.299 ms 108.170.233.163 [AS15169]  48.962 ms
11  * * *
12  * * *
13  * * *
14  * * *
15  * * *
16  * * *
17  * 8.8.8.8 [AS15169]  48.803 ms *
```

---

6. Повторите задание 5 в утилите `mtr`. На каком участке наибольшая задержка - delay?  

```
ubuntu (192.168.5.155)                                                                                                                       2021-12-05T12:59:49+0700
Keys:  Help   Display mode   Restart statistics   Order of fields   quit
                                                                                                                             Packets               Pings
 Host                                                                                                                      Loss%   Snt   Last   Avg  Best  Wrst StDev
 1. AS???    192.168.5.2                                                                                                    0.0%    37   12.0   1.4   0.3  12.0   2.2
 2. AS21127  80.89.151.XXX                                                                                                  0.0%    37    1.3   1.4   1.2   4.6   0.6
 3. AS20485  188.43.12.201                                                                                                  0.0%    37    1.8   2.3   1.5  18.7   2.9
 4. AS20485  188.43.12.202                                                                                                  0.0%    37    2.1   3.0   2.1   6.7   1.0
 5. AS20485  217.150.55.234                                                                                                 0.0%    37   42.4  43.4  42.1  64.3   3.8
 6. AS20485  188.43.10.141                                                                                                  0.0%    37   79.8  48.7  42.1 204.2  27.1
 7. AS15169  108.170.250.66                                                                                                 0.0%    37   40.3  40.7  40.2  44.9   0.8
 8. AS15169  209.85.255.136                                                                                                18.9%    37   55.8  55.1  54.7  55.8   0.3
 9. AS15169  172.253.65.82                                                                                                  0.0%    37   54.7  61.3  53.8 124.1  17.5
10. AS15169  172.253.51.219                                                                                                 0.0%    37   52.2  52.9  51.9  55.5   0.7
11. (waiting for reply)
12. (waiting for reply)
13. (waiting for reply)
14. (waiting for reply)
15. (waiting for reply)
16. (waiting for reply)
17. (waiting for reply)
18. (waiting for reply)
19. (waiting for reply)20. AS15169  8.8.8.8                                                                                 5.6%    36   63.1  55.2  53.6  63.1   2.6
```
Худший результат:
```
Host                                                                                                                      Loss%   Snt   Last   Avg  Best  Wrst StDev
8. AS15169  209.85.255.136                                                                                                18.9%    37   55.8  55.1  54.7  55.8   0.3
```

---

7. Какие DNS сервера отвечают за доменное имя dns.google? Какие A записи? воспользуйтесь утилитой `dig`  

```
us@ubuntu:~$ dig NS gmail.com

; <<>> DiG 9.16.1-Ubuntu <<>> NS gmail.com
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 54253
;; flags: qr rd ra; QUERY: 1, ANSWER: 4, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;gmail.com.                     IN      NS

;; ANSWER SECTION:
gmail.com.              21600   IN      NS      ns2.google.com.
gmail.com.              21600   IN      NS      ns4.google.com.
gmail.com.              21600   IN      NS      ns3.google.com.
gmail.com.              21600   IN      NS      ns1.google.com.

;; Query time: 532 msec
;; SERVER: 127.0.0.53#53(127.0.0.53)
;; WHEN: Вс дек 05 13:33:14 +07 2021
;; MSG SIZE  rcvd: 117
```

```
us@ubuntu:~$ dig gmail.com

; <<>> DiG 9.16.1-Ubuntu <<>> gmail.com
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 36638
;; flags: qr rd ra; QUERY: 1, ANSWER: 4, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;gmail.com.                     IN      A

;; ANSWER SECTION:
gmail.com.              274     IN      A       108.177.14.18
gmail.com.              274     IN      A       108.177.14.83
gmail.com.              274     IN      A       108.177.14.19
gmail.com.              274     IN      A       108.177.14.17

;; Query time: 0 msec
;; SERVER: 127.0.0.53#53(127.0.0.53)
;; WHEN: Вс дек 05 13:34:10 +07 2021
```

---

8. Проверьте PTR записи для IP адресов из задания 7. Какое доменное имя привязано к IP? воспользуйтесь утилитой `dig`  

us@ubuntu:~$ dig -x  108.177.14.18
```
; <<>> DiG 9.16.1-Ubuntu <<>> -x 108.177.14.18
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 41195
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;18.14.177.108.in-addr.arpa.    IN      PTR

;; ANSWER SECTION:
18.14.177.108.in-addr.arpa. 13669 IN    PTR     lt-in-f18.1e100.net.

;; Query time: 60 msec
;; SERVER: 127.0.0.53#53(127.0.0.53)
;; WHEN: Вс дек 05 13:36:23 +07 2021
;; MSG SIZE  rcvd: 88
```
Т.е. для адреса 108.177.14.18 привязано имя `lt-in-f18.1e100.net.`
Или вот: 
```
us@ubuntu:~$ dig -x 216.239.34.10

; <<>> DiG 9.16.1-Ubuntu <<>> -x 216.239.34.10
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 61065
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;10.34.239.216.in-addr.arpa.    IN      PTR

;; ANSWER SECTION:
10.34.239.216.in-addr.arpa. 21600 IN    PTR     ns2.google.com.

;; Query time: 63 msec
;; SERVER: 127.0.0.53#53(127.0.0.53)
;; WHEN: Вс дек 05 13:41:17 +07 2021
;; MSG SIZE  rcvd: 83
```
К адресу 216.239.34.10 привязяно имя `ns2.google.com.`

---
