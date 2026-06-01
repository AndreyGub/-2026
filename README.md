# -2026 Домашнее задание по лекции "Защита сети" Губайдуллин Андрей
 


### Подготовка к выполнению заданий

1. Подготовка защищаемой системы:

- установите **Suricata**,
- <img width="655" height="109" alt="image" src="https://github.com/user-attachments/assets/58b5d1c0-2d6e-4204-9db0-4f790711e810" />

- установите **Fail2Ban**.
  <img width="772" height="191" alt="image" src="https://github.com/user-attachments/assets/ce419260-4027-44af-8ed1-af8fb467a5c1" />

2. Подготовка системы злоумышленника: установите **nmap** и **thc-hydra** либо скачайте и установите **Kali linux**.

Обе системы должны находится в одной подсети.

------

### Задание 1

Проведите разведку системы и определите, какие сетевые службы запущены на защищаемой системе:

**sudo nmap -sA < ip-адрес >**

**sudo nmap -sT < ip-адрес >**

**sudo nmap -sS < ip-адрес >**

**sudo nmap -sV < ip-адрес >**

По желанию можете поэкспериментировать с опциями: https://nmap.org/man/ru/man-briefoptions.html.


*В качестве ответа пришлите события, которые попали в логи Suricata и Fail2Ban, прокомментируйте результат.*
# Ответ
1. Выполним сканирование:
   
sudo nmap -sA 10.129.0.15
sudo nmap -sT 10.129.0.15
sudo nmap -sS 10.129.0.15
sudo nmap -sV 10.129.0.15
------
<img width="903" height="310" alt="image" src="https://github.com/user-attachments/assets/59134b72-2f04-44d6-bee0-ab351ddec868" />
<img width="795" height="179" alt="image" src="https://github.com/user-attachments/assets/55bb22f0-f5c4-4eee-b747-91ffa51d04cd" />
<img width="889" height="165" alt="image" src="https://github.com/user-attachments/assets/b103e86e-92f4-4324-a784-30fe05632dd8" />

# События, попавшие в логи Suricata. Видим, что Suricata успешно зафиксил сканирование портов с IP-адреса 10.129.0.19

<img width="951" height="473" alt="image" src="https://github.com/user-attachments/assets/7d66fa8f-7b9c-414e-9888-7ae23aba6915" />

# События, попавшие в логи Fail2Ban. Видим, что обнаружил сканироване портов, так как анализирует логи аутентификации, а сканирование портов не создает записей в логах служб

<img width="670" height="182" alt="image" src="https://github.com/user-attachments/assets/33681f9c-151c-4065-86f3-d16e4d6f4134" />

### Задание 2

Проведите атаку на подбор пароля для службы SSH:

**hydra -L users.txt -P pass.txt < ip-адрес > ssh**

1. Настройка **hydra**: 
 
 - создайте два файла: **users.txt** и **pass.txt**;
 - в каждой строчке первого файла должны быть имена пользователей, второго — пароли. В нашем случае это могут быть случайные строки, но ради эксперимента можете добавить имя и пароль существующего пользователя.

Дополнительная информация по **hydra**: https://kali.tools/?p=1847.

2. Включение защиты SSH для Fail2Ban:

-  открыть файл /etc/fail2ban/jail.conf,
-  найти секцию **ssh**,
-  установить **enabled**  в **true**.

Дополнительная информация по **Fail2Ban**:https://putty.org.ru/articles/fail2ban-ssh.html.

# Ответ 
1. Производим атаку на хост 10.129.0.15
   <img width="933" height="485" alt="image" src="https://github.com/user-attachments/assets/4ecbe197-6b78-4c76-a6ba-fea668dd56c3" />


# Логи Fail2Ban

# Просмотр логов Fail2Ban
sudo tail -50 /var/log/fail2ban.log
<img width="1198" height="471" alt="image" src="https://github.com/user-attachments/assets/5eb8b4ac-d96d-4cfd-9517-63409c562ecb" />
<img width="1217" height="442" alt="image" src="https://github.com/user-attachments/assets/5da37262-03a9-4ab6-b86b-870307c82ca5" />


# Статус Fail2Ban после блокировки атакую с ip 10.129.0.19

<img width="844" height="184" alt="image" src="https://github.com/user-attachments/assets/cf937d3d-da3e-4e38-9c4d-2138e396e878" />

*В качестве ответа пришлите события, которые попали в логи Suricata и Fail2Ban, прокомментируйте результат.*
