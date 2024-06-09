# guard_network

# Задание 1

Проведите разведку системы и определите, какие сетевые службы запущены на защищаемой системе:

```
sudo nmap -sA < ip-адрес >
```
```
sudo nmap -sT < ip-адрес >
```
```
sudo nmap -sS < ip-адрес >
```
```
sudo nmap -sV < ip-адрес >
```

По желанию можете поэкспериментировать с опциями: https://nmap.org/man/ru/man-briefoptions.html.

В качестве ответа пришлите события, которые попали в логи Suricata и Fail2Ban, прокомментируйте результат.



# Ответ 1
Судя по логам, Suricata показал себя после всех запросов, кроме -sA. В остальных же случаях лог Suricata выдает, что происходило подозрительное сканирование и классификация идет как "Потенциально опасный трафик" и "Возможна утечка информации" ( Attempted Information Leak) .
Fail2Ban во всех случаях молчал



![alt text](https://github.com/StepanovSA/guard_network/blob/main/Kali%201.png)

![alt text](https://github.com/StepanovSA/guard_network/blob/main/deb%201.1.png)

![alt text](https://github.com/StepanovSA/guard_network/blob/main/deb%201.2.png)

![alt text](https://github.com/StepanovSA/guard_network/blob/main/deb%201.3.png)

# Задание 2

Проведите атаку на подбор пароля для службы SSH:
```
hydra -L users.txt -P pass.txt < ip-адрес > ssh
```
Настройка hydra:
создайте два файла: users.txt и pass.txt;
в каждой строчке первого файла должны быть имена пользователей, второго — пароли. В нашем случае это могут быть случайные строки, но ради эксперимента можете добавить имя и пароль существующего пользователя.
Дополнительная информация по hydra: https://kali.tools/?p=1847.

Включение защиты SSH для Fail2Ban:
открыть файл /etc/fail2ban/jail.conf,
найти секцию ssh,
установить enabled в true.
Дополнительная информация по Fail2Ban:https://putty.org.ru/articles/fail2ban-ssh.html.

В качестве ответа пришлите события, которые попали в логи Suricata и Fail2Ban, прокомментируйте результат.

# Ответ 2
Fail2ban выключен. Suricata также показывает сканирование ssh.

![alt text](https://github.com/StepanovSA/guard_network/blob/main/Kali%202.1.png)

![alt text](https://github.com/StepanovSA/guard_network/blob/main/deb%202.1%20fail%202ban.png)

![alt text](https://github.com/StepanovSA/guard_network/blob/main/deb%202.2%20log.png)


Fail2ban включен. Как мы видим , что пароли не были подобраны. Во время включенного Fail2ban, и попытки на Kali подобрать пароль, она была заблокирована.

![alt text](https://github.com/StepanovSA/guard_network/blob/main/Kali%202.2.png)

![alt text](https://github.com/StepanovSA/guard_network/blob/main/deb%202.3%20active%202ban.png)

![alt text](https://github.com/StepanovSA/guard_network/blob/main/deb%202.4%20log%202ban.png)
