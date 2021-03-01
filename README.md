# windowsn-qemu-raspbian
Запуск Raspbian под Windows10 с возможностью модификации образа

____
# Метод №1


# Скачивание необходимых инструментов

-  [QEMU](https://qemu.weilnetz.de/w64/)
-  [quemu_raspi_kernel](https://github.com/dhruvvyas90/qemu-rpi-kernel)
-  [Raspbian](http://downloads.raspberrypi.org/raspbian/images/)

## Скачивание Qemu

![](https://raw.githubusercontent.com/tviks/windowsn-qemu-raspbian/main/pic/1.png "qemu")



# Распаковка и установка

*Примечание к установке:*  
*QEMU путь для установки должен выглядить как .../qemu/qemu*  
	
	Создаем папку на рабочем столе qemu затем, скачиваем и распаковываем (устанавливаем) в нее:

![](https://raw.githubusercontent.com/tviks/windowsn-qemu-raspbian/main/pic/2.png "")
	
	Разархивируем и копируем скачанный образ в .../qemu/qemu
	
![](https://raw.githubusercontent.com/tviks/windowsn-qemu-raspbian/main/pic/3.png "")
	
	Копируем из папки qemu-rpi-kernel в папку .../qemu/qemu kernel-qemu-4.4.34-jessie
	
![](https://raw.githubusercontent.com/tviks/windowsn-qemu-raspbian/main/pic/4.png "")
	
# Увеличение размера образа 

	qemu-img resize 2021-01-11-raspios-buster-armhf-lite.img +2G
*размер увеличился на 2Gb*

### Создаем start.bat со следующим содержанием:
*при необходимости изменить строчку "-hda 2021-01-11-raspios-buster-armhf-lite.img"*

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

# Рекомедуемая настройка виртуальной машины:

### Логинимся под пользователем

	user: pi
	password: raspberry

### Расширение места на диске 

	sudo raspi-config  
	6) Advanced options > A1 Expand Filesystem  
	
### Увеличение производительности 

	sudo raspi-config  
	4) Perfomance Options > P1 Overclock > set Turbo  

###Обновление системы

	sudo apt-get update && sudo apt-get upgrade -y  

____
# Метод №1

