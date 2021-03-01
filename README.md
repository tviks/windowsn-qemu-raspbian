# windowsn-qemu-raspbian
Запуск Raspbian под Windows10 с возможностью модификации образа

____

## Скачивание необходимых инструментов

Создаем папку на рабочем столе quemu затем,
скачиваем и распаковываем(устанавливаем) в нее:

-  [QEMU](https://qemu.weilnetz.de/w64/)
-  [quemu_raspi_kernel](https://github.com/dhruvvyas90/qemu-rpi-kernel)
-  [Raspbian](http://downloads.raspberrypi.org/raspbian/images/)
	
*Примечание к установке*
*QEMU путь для установки должен выглядить как .../qemu/qemu*

## Распаковка и копирование образов

Разархивируем и копируем скаченный образ в .../qemu/qemu (при необходимости изменить строчку "-hda 2021-01-11-raspios-buster-armhf-lite.img" в start.bat
Копируем из папки qemu-rpi-kernel в папку .../qemu/qemu kernel-qemu-4.4.34-jessie

### Создаем start.bat со следующим содержанием:
```
	qemu-system-arm ^
	-kernel kernel-qemu-4.4.34-jessie ^
	-cpu arm1176 ^
	-m 256 ^
	-M versatilepb ^
	-serial stdio ^
	-append "root=/dev/sda2 rootfstype=ext4 rw" ^
	-hda 2021-01-11-raspios-buster-armhf-lite.img ^
	-net nic ^
	-net user,hostfwd=tcp::5022-:22 ^
	-no-reboot
```
