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
5. Через какие сети проходит пакет, отправленный с вашего компьютера на адрес 8.8.8.8? Через какие AS? Воспользуйтесь утилитой `traceroute`  

```
us@ubuntu:~$ traceroute -An 8.8.8.8
traceroute to 8.8.8.8 (8.8.8.8), 30 hops max, 60 byte packets
 1  192.168.0.1 [*]  0.387 ms  0.431 ms  0.362 ms
 2  10.154.109.2 [AS21127/AS20485]  1.642 ms  1.683 ms  1.852 ms
 3  188.43.12.201 [AS20485]  1.893 ms  1.835 ms  1.757 ms
 4  188.43.12.202 [AS20485]  5.017 ms  5.157 ms  5.082 ms
 5  217.150.55.234 [AS20485]  39.719 ms  42.243 ms  42.362 ms
 6  188.43.10.141 [AS20485]  42.305 ms  39.640 ms  39.544 ms
 7  108.170.250.99 [AS15169]  42.752 ms 108.170.250.130 [AS15169]  40.527 ms 108.170.250.34 [AS15169]  37.424 ms
 8  * * 209.85.249.158 [AS15169]  54.356 ms
 9  172.253.66.108 [AS15169]  48.428 ms 172.253.65.82 [AS15169]  51.098 ms 74.125.253.109 [AS15169]  51.390 ms
10  142.250.238.181 [AS15169]  53.239 ms 142.250.236.77 [AS15169]  55.338 ms 216.239.47.173 [AS15169]  52.240 ms
11  * * *
12  * * *
13  * * *
14  * * *
15  * * *
16  * * *
17  * * *
18  * * *
19  * * *
20  8.8.8.8 [AS15169]  48.343 ms *  53.900 ms
```

---

6. Повторите задание 5 в утилите `mtr`. На каком участке наибольшая задержка - delay?  

Худший результат:
```
Host                                                                                                                      Loss%   Snt   Last   Avg  Best  Wrst StDev
9. AS15169  172.253.65.82                                                                                                  0.0%    65   54.2  56.7  53.8 121.2   9.0
```

---

7. Какие DNS сервера отвечают за доменное имя dns.google? Какие A записи? воспользуйтесь утилитой `dig`  


11. Проверьте PTR записи для IP адресов из задания 7. Какое доменное имя привязано к IP? воспользуйтесь утилитой `dig`

В качестве ответов на вопросы можно приложите лог выполнения команд в консоли или скриншот полученных результатов.

---
