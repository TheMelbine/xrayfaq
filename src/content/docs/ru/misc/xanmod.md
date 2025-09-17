---
title: Установка ядра xanmod
description: В данном руководстве мы осуществим установку xanmod kernel
---

Для того, что бы воспользоваться BBR3, Вам нужно перейти на ядро XanMod kernel.


Вы должны понимать что меняете ЯДРО



Все вопросы касаемо установки и использования ядра, Вы можете узнать:

https://t.me/kernel_xanmod

https://xanmod.org



## Ручная установка
1. Добавляем Ключ
	```bash
	wget -qO - https://gitlab.com/afrd.gpg | sudo gpg --dearmor -o /usr/share/keyrings/xanmod-archive-keyring.gpg
	``` 
2. Добавляем репо
	```bash
	echo 'deb [signed-by=/usr/share/keyrings/xanmod-archive-keyring.gpg] http://deb.xanmod.org releases main' | sudo tee /etc/apt/sources.list.d/xanmod-release.list
	``` 
3. Обновляем 
	```bash
	sudo apt update 
	``` 
4. Проверяем поддерживаемую архитектуру

	```bash
	wget -qO - https://dl.xanmod.org/check_x86-64_psabi.sh | awk -f -
	``` 
</Steps>
В зависимости от вывода (v1, v2, v3, v4) и выбранной ветки ядра, Вам необходимо указать соотвествующее имя пакета в следующей команде

| Ветка | v1				|v2|v3|v4|
| ----- | ------------------ | ------------------ | ------------------ | ------------------ |
| MAIN | linux-xanmod-x64v1 | linux-xanmod-x64v2 | linux-xanmod-x64v3 | linux-xanmod-x64v4 |
| EDGE | -					 | linux-xanmod-edge-x64v2 | linux-xanmod-edge-x64v3 | linux-xanmod-edge-x64v4 |
| LTS |  linux-xanmod-lts-x64v1 | linux-xanmod-lts-x64v2 | linux-xanmod-lts-x64v3 | linux-xanmod-lts-x64v3 |
| RT | - | linux-xanmod-rt-x64v2 | linux-xanmod-rt-x64v3 | linux-xanmod-rt-x64v4 |


3. Устанавливаем ядро
   
	В данном примере мы устанавливаем  main ветку для v3 (x86-64-v3)

	```bash
	sudo apt install linux-xanmod-x64v3
	``` 
5. перезагрузка
   
	```bash
	reboot now
	```
6. Подгружаем модули
   
	```bash
	depmod -a
	``` 
7. Проверяем корректность загрузки модуля
	```bash
	modinfo tcp_bbr
	```  	
8. Открываем файл
   
	```bash
	sudo nano /etc/sysctl.conf
	```  	
9. Добавляем необходимые переменные
    
	```bash
   nano /etc/sysctl.conf
	net.core.default_qdisc=fq
	net.ipv4.tcp_congestion_control=bbr

11. Выполняем

	```bash
	sysctl -p
	```  	
