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
update-kernel
apt-get clean
reboot
```

b.	Создайте пользователя user2 с паролем P@ssw0rd.
```
useradd user2
passwd user2
P@ssw0rd
```
c.	Установите Яндекс браузер.
```
su -
apt-get update
apt-get install yandex-browser-stable
```
i.	Настройте блокировщик рекламы для работы с Яндекс браузером
```
Заходим в меню, в поиске пишем Adguard и нажимаем установить.
```
ii.	Подключитесь к nextcloud и сохраните учётные данные для входа.

d.	Установите антивирус Kaspersky.

```
Скачать в Яндекс браузере
https://products.s.kaspersky-labs.com/endpoints/keslinux10/12.0.0.6672/multilanguage-12.0.0.6672/3739343633377c44454c7c31/kesl-gui-12.0.0-6672.x86_64.rpm
https://products.s.kaspersky-labs.com/endpoints/keslinux10/12.0.0.6672/multilanguage-12.0.0.6672/3739343633347c44454c7c31/kesl-12.0.0-6672.x86_64.rpm
Открыть каталог Загрузки 
Правой кнопкой – «Открыть в установка RPM»
Ввести пароль root

Открыть каталог с Kaspersky_GUI
Скопировать Kaspersky_GUI в «Файловая система» - /tmp
Правой кнопкой – «Открыть в установка RPM»
Ввести пароль root

su -
/opt/kaspersky/kesl/bin/kesl-setup.pl

Enter
y
Enter
…
```
i.	Настройте расписание сканирование системы.

ii.	Проверить работоспособность антивируса с помощью программы eicar.
```
В Яндекс Браузере ищем и скачиваем eicar.
http://www.virusanalyst.com/eicar.zip
```
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
Скопировать CS в «Файловая система» - /tmp
Открыть терминал в каталоге /tmp (правой кнопкой – Открыть  в терминале)
wine yourmon_cs16.exe (нажать TAB чтобы дописать имя)
```
i.	После установки запустите игру и подключитесь к своему серверу 
```
На рабочем столе
```
# 2.	На SRV необходимо сделать следующие настройки: 
Текущие учетные данные пользователь user с паролем resu, и пользователь root с паролем toor.
a.	Настройте следующий IP адрес 10.11.12.10 с маской 255.255.255.0 (24) шлюз по умолчанию 10.11.12.1 и DNS сервер 10.11.12.1
```
Зайти в «система» и во вкладку «центр управления», и ещё раз ту даже уже во вкладке. Зайти нажать и Ethernet. 
```
b.	Проверьте связность между SRV и CLI, а также доступность в интернет.
```
Вводим в консоли ping и IP адрес. (Для его просмотра введите команду   «ip a» и второй не служебный IP адрес)    
```
c.	Проведите обновление системы.
```
su -
apt-get update
apt-get dist-upgrade
update-kernel
apt-get clean
reboot
```
d.	Задайте имя компьютера SRV. 
```
Зайти в «система» и во вкладку «центр управления», и ещё раз ту даже уже во вкладке. Зайти нажать и Ethernet и там поменяйте имя.
```
e.	Поменяйте пароль пользователю user на P@ssw0rd.
```
passwd user
```
f.	Подключите созданную NFS шару с сервера 10.11.12.1. Она должна автоматический монтироваться по пути /mnt/nfsshare.

g.	Настройте подключение по SSH для удалённого конфигурирования устройства.

h.	Необходимо поставить сервер для игры «CS 1.6» выбор пути установки на ваш выбор но мы рекомендуем поставить через docker.

i.	Установите хранилище данных nextcloud.

i.	Настройте пользователя USER_RESU с паролем P@ssw0rd для доступа с клиентского компьютера
```
useradd USER_RESU
passwd USER_RESU
P@ssw0rd
```
j.	Установите Web-интерфейс Алтератор для управления сервером с CLI.
```
apt-get install alterator-fbi
service alteratord start; service ahttpd start
[https://localhost:8080](https://localhost:8080)
```
