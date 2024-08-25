# LDAP
LDAP. Централизованная авторизация и аутентификация 
## Цель домашнего задания
* Научиться настраивать LDAP-сервер и подключать к нему LDAP-клиентов
1. После создания Vagrantfile, запустим виртуальные машины командой vagrant up. Будут созданы 3 виртуальных машины
2. **Установка FreeIPA сервера.** Для начала нам необходимо настроить FreeIPA-сервер. Подключимся к нему по SSH с помощью команды: ``` vagrant ssh ipa.otus.lan ``` и перейдём в root-пользователя:``` sudo -i ``` 
3. Начнем настройку FreeIPA-сервера:
* Установим часовой пояс:``` timedatectl set-timezone Europe/Samara ```
* Установим утилиту chrony:``` yum install -y chrony ```
* Запустим chrony и добавим его в автозагрузку:``` systemctl enable chronyd ```
* Выключим Firewall:``` systemctl stop firewalld ```
* Отключаем автозапуск Firewalld:``` systemctl disable firewalld ```
* Остановим Selinux:``` setenforce 0 ```
* Поменяем в файле /etc/selinux/config, параметр Selinux на disabled ``` nano /etc/selinux/config ```
```
...
#    grubby --update-kernel ALL --remove-args selinux
#
SELINUX=disabled
# SELINUXTYPE= can take one of these three values:
#     targeted - Targeted processes are protected,
#     minimum - Modification of targeted policy. Only selected processes are protected.
#     mls - Multi Level Security protection.
SELINUXTYPE=targeted
``` 

