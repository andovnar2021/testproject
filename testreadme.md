# Homeworks TeachMySkills
## DOS-07

![image1](/images/devops.png)

![image1](/images/andovnar.png)




<TeachMySkills\>            ✨
## Homework №12

1) Поднять несколько виртуальных машин в одной сети.
2) На вторую машину поставить nginx, jenkins. 
3) Просканить все порты и машины в сети одной командой.
4) Есть ip адрес 172.16.1.48 и маска подсети 255.255.224.0
- определить адрес сети в десятичном и двоичном представлении
- ip адрес первого узла подсети
- широковещательный адрес
- ip адрес последнего узла подсети
5) Разделить IP-сеть 192.168.16.0/24 на подсети с 100, 20, 10, 6 и 40 узлами. 
Для каждой подсети указать широковещательный адрес.
6) Что такое сокет? Что такое сокетное соединение? *






#### Task1

1) Поднять несколько виртуальных машин в одной сети.

 - +VM a@VM192.168.0.156
 - +VM a@testvm1 192.168.0.153

#### Task2
2) На вторую машину поставить nginx, jenkins. 
##### Install nginx


```sh
sudo apt update
sudo apt install nginx
sudo ufw app list
Output
Available applications:
  Nginx Full
  Nginx HTTP
  Nginx HTTPS
  OpenSSH
  sudo ufw allow 'Nginx HTTP'
  sudo ufw status
  systemctl status nginx
```
##### Install Jenkins
```sh
wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -
sudo sh -c 'echo deb http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
sudo apt update
sudo apt install jenkins
sudo systemctl start jenkins
sudo systemctl status jenkins
```

![image1](/images/12-2.png)

#### Task3
3) Просканить все порты и машины в сети одной командой.

![image1](/images/12-3.png)

#### Task4
4) Есть ip адрес 172.16.1.48 и маска подсети 255.255.224.0
- определить адрес сети в десятичном и двоичном представлении

  маска подсети = 255.255.254.0
  адрес клиента = 172.16.1.48 

Двоичное представление: (делим на 2 октеты) затем AND

 маска подсети = 11111111.11111111.11111110.00000000
 адрес клиента = 10101100.00010000.00000001.00110000
 адрес сети    = 10101100.00010000.00000000.00000000

Десятичное представление:

адрес сети = 172.16.0.0


- ip адрес первого узла подсети
172.16.0.1

- широковещательный адрес OR
адрес клиента =              10101100.00010000.00000001.00110000
inverted маска подсети = 00000000.00000000.00000001.11111111

broadcast address=10101100.00010000.00000001.1111111
172.16.1.255

- ip адрес последнего узла подсети
172.16.1.255

#### Task5
5) Разделить IP-сеть 192.168.16.0/24 на подсети с 100, 20, 10, 6 и 40 узлами. 
Для каждой подсети указать широковещательный адрес.
- 100 nodes
 192.168.16.0/24  2^7-2=126
192.168.16.0/25
broadcast address =192.168.16.127
- 20 nodes
192.168.16.128/25 2^5-2=30
192.168.16.128/27
broadcast address =192.168.16.159
- 10 nodes
192.168.16.160/26 2^4-2=14
192.168.16.160/28
broadcast address =192.168.16.175
- 6 nodes
192.168.16.176/28 2^3-2=6
192.168.16.176/29
broadcast address =192.168.16.183
- 40 nodes
192.168.16.184/29 2^6-2=62
192.168.16.192/26
broadcast address =192.168.16.255




#### Task6
6) Что такое сокет? Что такое сокетное соединение? *
> Сокет - это абстракция сетевого взаимодействия в операционной системе Linux. Каждому сокету соответствует пара IP-адрес + номер порта. Это стандартное определение, к которому привыкли все, спасибо вики. Хотя нет, вот здесь лучше описано. Поскольку сокет является только лишь абстракцией, то связка IP-адрес + номер порта - это уже имплементация в ОС. Верное название этой имплементации - "Интернет сокет". Абстракция используется для того, чтобы операционная система могла работать с любым типом канала передачи данных. Именно поэтому в ОС Linux Интернет сокет - это дескриптор, с которым система работает как с файлом. Типов сокетов, конечно же, намного больше. В ядре ОС Linux сокеты представлены тремя основными структурами:
struct socket - представление сокета BSD, того вида сокета, который стал основой для современных "Интернет сокетов";
struct sock - собственная оболочка, которая в Linux называется "INET socket";
struct sk_buff - "хранилище" данных, которые передает или получает сокет;
Как видно по исходным кодам, все структуры достаточно объемны. Работа с ними возможна при использовании языка программирования или специальных оберток и написания приложения. Для эффективного управления этими структурами нужно знать, какие типы операций над сокетами существуют и когда их применять. Для сокетов существует набор стандартных действий:
socket - создание сокета;
bind - действие используется на стороне сервера. В стандартных терминах - это открытие порта на прослушивание, используя указанный интерфейс;
listen - используется для перевода сокета в прослушивающее состояние. Применяется к серверному сокету;
connect - используется для инициализации соединения;
accept - используется сервером, создает новое соединение для клиента;
send/recv - используется для работы с отправкой/приемом данных;
close - разрыв соединения, уничтожение сокета.
Если о структурах, которые описаны выше, заботится ядро операционной системы, то в случае команд по управлению соединением ответственность берет на себя приложение, которое хочет пересылать данные по сети. 



## Information links



| Plugin | README |
| ------ | ------ |
| Jenkins | [https://www.digitalocean.com/community/tutorials/how-to-install-jenkins-on-ubuntu-20-04-ru]|
| Nginx | [https://www.digitalocean.com/community/tutorials/how-to-install-nginx-on-ubuntu-20-04-ru]|



