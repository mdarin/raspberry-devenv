# DEVENV для Raspberry

Как настроить sshfs на винде и на маке для подключения к малинке
настрока ssh есть в imager

инструкция для windows
<https://winitpro.ru/index.php/2025/01/20/podkluchit-disk-po-ssh-windows/>

gui для windows
<https://github.com/evsar3/sshfs-win-manager/releases>

инструкция для мак(не проверялась!)
<https://phoenixnap.com/kb/sshfs-mac>

настройка vnc на малинке
<https://www.raspberrypi.com/documentation/computers/remote-access.html#enable-the-vnc-server-on-the-command-line>

клиент рекомендованый
<https://tigervnc.org/>

Монтирование сетевых дисков в wsl2
<https://winitpro.ru/index.php/2023/10/25/montirovanie-diskov-wsl2/>
Для windows надо подключить sshfs сетевой диск к букве(например Z:).

Далее смонтировать сетевой дикс Z: в wsl. /mnt/z/

И уже там пробросить в docker контейнеры для сборки приложений.

Распиновка разъёма

![R- pi zero GPIO pinout diagram](https://www.etechnophiles.com/wp-content/uploads/2023/05/R-pi-zero-GPIO-pinout-Diagram.jpg)

Назначение контактов на разъёме(гребёнке)
<https://pinout.xyz/pinout/pin3_gpio2/>

Для сборки проектов на хосте(Dockerfile приложены)

```sh
$ cd to/your/awesom/rpi/project
$ docker build -t go25-arm6l:v0.2 -f Dockerfile.armv6l .
$ docker run --rm -ti -v $(pwd):/ws -w /ws go25-arm6l:v0.2 ash
container@/ws# go build ... -o your-app-bin
# move to /usr/local/bin
# run the application!
```

## Что такое systemd-nspawn?

По сути, это утилита для запуска команды или целой ОС в легковесном контейнере, используя только встроенные механизмы ядра Linux: namespaces (для изоляции процессов, сети, пользователей) и cgroups (для контроля ресурсов).

Установка **systemd-nspawn** на Raspberry Pi OS
Выполните следующие команды:

Обновите список пакетов:

```bash
sudo apt update
sudo apt install systemd-container
```

Проверьте установку:

```bash
systemd-nspawn --version
```
