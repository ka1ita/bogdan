# 1.	Установка операционной системы на CLI: 
* Установите операционную систему Альт Рабочая станция,
```
Создаем виртуальную машину CLI 
Linux, Other Linux 64bit, 2 процессора, более 2 ГБ оперативная память, 60 ГБ жесткий диск, видеопамять 128 МБ
Подключаем alt-workstation-10.1-x86_64.iso
И запускаем
```
* Задайте имя компьютера CLI
* При установке укажите имена пользователь user с паролем resu, и пользователь root с паролем toor,
* IP адрес вам приход от провайдера по DHCP,
* Остальные настройки при установки оставить по умолчанию.

# 3.	Настройка клиентского компьютера:
a.	Проведите обновление системы.
```
su -
apt-get update
apt-get dist-upgrade
apt-get clean
reboot
```

b.	Создайте пользователя user2 с паролем P@ssw0rd.
```
useradd user2
passwd user2
```
c.	Установите Яндекс браузер.
```
su -
apt-get update
apt-get install yandex-browser-stable
```
i.	Настройте блокировщик рекламы для работы с Яндекс браузером
```
Заходим в меню три полоски справа сверху, Расширения, в поиске пишем Adguard и нажимаем установить.
```
d.	Установите антивирус Kaspersky.
```
Скачать в Яндекс браузере
```
https://products.s.kaspersky-labs.com/endpoints/keslinux10/11.4.0.1096/multilanguage-11.4.0.1096/3732393737337c44454c7c31/kesl-11.4.0-1096.x86_64.rpm

https://products.s.kaspersky-labs.com/endpoints/keslinux10/11.4.0.1096/multilanguage-11.4.0.1096/3732393737367c44454c7c31/kesl-gui-11.4.0-1096.x86_64.rpm
```
Открыть каталог Загрузки 
Правой кнопкой kesl-11.4.0-1096.x86_64.rpm – «Открыть в установка RPM»
Ввести пароль root

Правой кнопкой kesl-gui-11.4.0-1096.x86_64.rpm – «Открыть в установка RPM»
Ввести пароль root

su -
/opt/kaspersky/kesl/bin/kesl-setup.pl

Enter
y
Enter
…
user with admin rights - указать user
advanced update settings - n 

```
i.	Настройте расписание сканирование системы.

ii.	Проверить работоспособность антивируса с помощью программы eicar.
```
В Яндекс Браузере ищем и скачиваем eicar.
```
http://www.virusanalyst.com/eicar.zip

e.	Установите Telegram (они должны запускается, но не авторизовывайтесь)
```
su -
apt-get update
apt-get install telegram-desktop
```
f.	Установите Steam (они должны запускается, но не авторизовывайтесь)
```
apt-get update; apt-get install i586-steam
```
g.	Установите игру «CS 1.6» (установочный файл запрашиваете у экспертов) используя программное обеспечение «Play on Linux» и программное обеспечение wine (их тоже необходимо установить)
```
su -
apt-get update
apt-get install wine-full i586-wine
```
Скачиваем тут:

https://your-cs.com/download.php?id=121

Или тут:

https://dl4.your-cs.com/yourmon_cs16.exe
```
Скопировать CS в «Файловая система» - /tmp
Открыть терминал в каталоге /tmp (правой кнопкой – Открыть  в терминале)
Не далать "su -"
wine yourmon_cs16.exe (нажать TAB чтобы дописать имя)
```
i.	После установки запустите игру и подключитесь к своему серверу 
```
На рабочем столе
```
ii.	Подключитесь к nextcloud и сохраните учётные данные для входа.

https://10.11.12.10:8080

# 2.	На SRV необходимо сделать следующие настройки: 
Текущие учетные данные пользователь user с паролем resu, и пользователь root с паролем toor.
a.	Настройте следующий IP адрес 10.11.12.10 с маской 255.255.255.0 (24) шлюз по умолчанию 10.11.12.1 и DNS сервер 10.11.12.1
```
открыть mc

В файл /etc/net/ifaces/enp0s3/ipv4address
10.11.12.10/24

В файл /etc/net/ifaces/enp0s3/ipv4route
default via 10.11.12.1

В файл /etc/net/ifaces/enp0s3/resolv.conf
nameserver 10.11.12.1

В файле /etc/net/ifaces/enp0s3/options
заменяем BOOTPROTO=dhcp на BOOTPROTO=static

reboot
```
b.	Проверьте связность между SRV и CLI, а также доступность в интернет.
```
Вводим в консоли
ping 10.11.12.11
ping 10.11.12.9
ping 10.11.12.1
```
c.	Проведите обновление системы.
```
su -
apt-get update
apt-get dist-upgrade
apt-get clean
reboot
```
d.	Задайте имя компьютера SRV. 
```
Открыть mc
В файл /etc/hostname
SRV
```
e.	Поменяйте пароль пользователю user на P@ssw0rd.
```
passwd user
```
j.	Установите Web-интерфейс Алтератор для управления сервером с CLI.
```
apt-get install alterator-fbi
service alteratord start; service ahttpd start
```
https://localhost:8080
f.	Подключите созданную NFS шару с сервера 10.11.12.1. Она должна автоматический монтироваться по пути /mnt/nfsshare.
```
su -
mkdir /mnt/nfsshare
mount -t nfs 10.11.12.1:/mysharedir /mnt/nfsshare
```
g.	Настройте подключение по SSH для удалённого конфигурирования устройства.
```
Открыть mc
В файе /etc/openssh/sshd_config

Дописываем:
Port 22
PermitRootLogin yes
PasswordAuthentication yes

Вводим:
systemctl restart sshd
```
h.	Необходимо поставить сервер для игры «CS 1.6» выбор пути установки на ваш выбор но мы рекомендуем поставить через docker.
```
apt-get install docker
docker pull febley/counter-strike_server
docker run --name counter-strike_server -p 27015:27015/udp -p 27015:27015 febley/counter-strike_server:latest
```
i.	Установите хранилище данных nextcloud.
```
apt-get install deploy
deploy nextcloud
```
Чтобы узнать пароль пользователя ncadmin сразу после разворачивания, можно посмотреть значение параметра admin-pass в журнале:
```
journalctl -b |grep admin-pass
```
Открываем:

http://localhost/nextcloud

Пользователь ncadmin, пароль тут:
```
journalctl -b |grep admin-pass
```
i.	Настройте пользователя USER_RESU с паролем P@ssw0rd для доступа с клиентского компьютера
```
useradd USER_RESU
passwd USER_RESU
P@ssw0rd
```
