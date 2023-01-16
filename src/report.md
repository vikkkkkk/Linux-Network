## Part 1. Инструмент ipcalc<br>
1. Сети и маски<br>
    * Устанавливаем **ipcalc** командой `sudo apt install ipcalc`<br>
    ![Установка ipcalc](screen/part1.png)*Установка ipcalc*<br><br>
    1) Адрес сети **192.167.38.54/13** `ipcalc 192.167.38.54/13`<br>
    ![Адрес сети](screen/part1.1.png)*Адрес сети*<br><br>
    2) Перевод маски **255.255.255.0** в префиксную и двоичную запись `ipcalc 255.255.255.0`<br>
    ![Префиксная и двоичная запись](screen/part1.2.png)*Префиксная и двоичная запись*<br><br>
    * **/15** в обычную и двоичную `ipcalc /15`<br>
    ![Обычная и двоичная запись](screen/part1.3.png)*Обычная и двоичная запись*<br><br>
    * **11111111.11111111.11111111.11110000** в обычную и префиксную `ipcalc 11111111.11111111.11111111.11110000`<br>
    ![Обычная и префиксная запись](screen/part1.4.png)*Обычная и префиксная запись*<br><br>
    3) Минимальный и максимальный хост в сети **12.167.38.4** при масках:<br>
    * **/8** `ipcalc 12.167.38.4 /8`<br>
    ![HostMin & HostMax](screen/part1.5.png)*HostMin & HostMax*<br><br>
    * **11111111.11111111.00000000.00000000** `ipcalc 12.167.38.4 11111111.11111111.00000000.00000000`<br>
    ![HostMin & HostMax](screen/part1.6.png)*HostMin & HostMax*<br><br>
    * **255.255.254.0** `ipcalc 12.167.38.4 255.255.254.0`<br>
    ![HostMin & HostMax](screen/part1.7.png)*HostMin & HostMax*<br><br>
    * **/4** `ipcalc 12.167.38.4 /4`<br>
    ![HostMin & HostMax](screen/part1.8.png)*HostMin & HostMax*<br><br>
    <br>
2. localhost<br>
    * По адресам **194.34.23.100** && **128.0.0.1** обратиться к приложению не получится, потому что у них нет петли.<br>
    ![194.34.23.100](screen/part1_ws1.png)*194.34.23.100*<br><br>
    ![128.0.0.1](screen/part1.1_ws1.png)*128.0.0.1*<br><br>
    * У **127.0.0.2** && **127.1.0.1** есть **loopback**, так что к ним обратиться можно.<br>
    ![127.0.0.2](screen/part1.1.1_ws1.png)*127.0.0.2*<br><br>
    ![127.1.0.1](screen/part1.1.1.1_ws1.png)*127.1.0.1*<br><br>
    <br>
3.  Диапазоны и сегменты сетей<br>
    1. <br>
        * **10.0.0.45** - Частный `ipcalc 10.0.0.45`<br>
        ![Private](screen/part1.9.png)*Private*<br><br>
        * **134.43.0.2** - Публичный `ipcalc 134.43.0.2`<br>
        ![Public](screen/part1.10.png)*Public*<br><br>
        * **192.168.4.2** - Частный `ipcalc 192.168.4.2`<br>
        ![Private](screen/part1.11.png)*Private*<br><br>
        * **172.20.250.4** - Частный `ipcalc 172.20.250.4`<br>
        ![Private](screen/part1.12.png)*Private*<br><br>
        * **172.0.2.1** - Публичный `ipcalc 172.0.2.1`<br>
        ![Public](screen/part1.13.png)*Public*<br><br>
        * **192.172.0.1** - Публичный `ipcalc 192.172.0.1`<br>
        ![Public](screen/part1.14.png)*Public*<br><br>
        * **172.68.0.2** - Публичный `ipcalc 172.68.0.2`<br>
        ![Public](screen/part1.15.png)*Public*<br><br>
        * **172.16.255.255** - Частный `ipcalc 172.16.255.255`<br>
        ![Private](screen/part1.16.png)*Private*<br><br>
        * **10.10.10.10** - Частный `ipcalc 10.10.10.10`<br>
        ![Private](screen/part1.17.png)*Private*<br><br>
        * **192.169.168.1** - Публичный `ipcalc 192.169.168.1`<br>
        ![Public](screen/part1.18.png)*Public*<br><br>

    2. <br>
        * **10.10.0.2** - да.<br>
        * **10.10.10.10** - да.<br>
        * **10.10.1.255** - да.<br>

## Part 2. Статическая маршрутизация между двумя машинами<br>
1. <br>
    * Поднимаем две виртуальные машины **ws1** && **ws2**<br>
    * `ip a`<br>
    ![ip a](screen/part2_ws1.png)*ip a*<br><br>
    ![ip a](screen/part2_ws2.png)*ip a*<br><br>
    * **ws1** `sudo vim etc/netplan/00-installer-config.yaml`<br>
    ![ws1](screen/part2.1_ws1.png)*ws1*<br><br>
    * **ws2** `sudo vim etc/netplan/00-installer-config.yaml`<br>
    ![ws2](screen/part2.1_ws2.png)*ws2*<br><br>
    <br>
    * Выполняем команды `sudo netplan apply` && `ip a`<br>
    * **ws1**<br>
    ![ws1](screen/part2.2_ws1.png)*ws1*<br><br>
    * **ws2**<br>
    ![ws2](screen/part2.2_ws2.png)*ws2*<br><br>
    <br>

2. Добавление статического маршрута вручную<br>
    * Добавление статического маршрута от одной машины до другой и обратно при помощи команды `ip r add`<br>
    * **ws1** - `ip r add 172.24.116.8 dev enp0s8`<br>
    ![Добавление статического маршрута](screen/part2.3_ws1.png)*Добавление статического маршрута*<br><br>
    * **ws2** - `ip r add 192.168.100.10 dev enp0s8`<br>
    ![Добавление статического маршрута](screen/part2.3_ws2.png)*Добавление статического маршрута*<br><br>
    * Пропинговать соединение между машинами:<br>
    * **ws1**<br>
    ![ws1](screen/part2.4_ws1.png)*ws1*<br><br>
    * **ws2**<br>
    ![ws2](screen/part2.4_ws2.png)*ws2*<br><br>
    <br>
    * Добавление статического маршрута с сохранением<br>
    * `sudo nano /etc/netplan/00-installer-config.yaml`<br>
    ![ws1](screen/part2.5_ws1.png)*ws1*<br><br>
    ![ws2](screen/part2.5_ws2.png)*ws2*<br><br>
    * `sudo netplan apply`<br>
    * `sudo reboot`<br>
    <br>
    * Пропинговать соединение между машинами<br>
    * **ws1** - `ping 192.168.100.10`<br>
    ![ws1](screen/part2.6_ws1.png)*ws1*<br><br>
    * **ws2** - `ping 172.24.116.8`<br>
    ![ws2](screen/part2.6_ws2.png)*ws2*<br><br>
    <br>
## Part 3. Утилита iperf3<br>
1. Перевести и записать в отчёт:<br>
    * 8 Mbps = 1 MS/s.<br>
    * 100 MB.s = 100000 Kbps.<br>
    * 1 Gbps = 1000 Mbps.<br>
    <br>
2. Утилита **iperf3**<br>
    * **ws1** - `iperf3 -s`<br>
    ![ws1](screen/part3_ws1.png)*ws1*<br><br>
    * **ws2** - `iperf3 -c 192.168.100.10 -p 5201`<br>
    ![ws2](screen/part3_ws2.png)*ws2*<br><br>
    <br>
## Part 4. Сетевой экран<br>
1. Утилита **iptables**<br>
    * Устанавливаем **iptables** `sudo apt-get install iptables`<br>
    ![ws1](screen/part4_ws1.png)*ws1*<br><br>
    ![ws2](screen/part4_ws2.png)*ws2*<br><br>
    <br>
    * на **ws1** применить стратегию когда в начале пишется запрещающее правило, а в конце пишется разрешающее правило (это касается пунктов 4 и 5)<br>
    * открыть на машинах доступ для порта **22** (ssh) и порта **80** (http)<br>
    * **запретить** echo reply (машина не должна "пинговаться”, т.е. должна быть блокировка на OUTPUT)<br>
    * **разрешить** echo reply (машина должна "пинговаться")<br>
    ![ws1](screen/part4.1_ws1.png)*ws1*<br><br>
    <br>
    * на **ws2** применить стратегию когда в начале пишется разрешающее правило, а в конце пишется запрещающее правило (это касается пунктов 4 и 5)<br>
    * открыть на машинах доступ для порта **22** (ssh) и порта **80** (http)<br>
    * **разрешить** echo reply (машина должна "пинговаться")<br>
    * **запретить** echo reply (машина не должна "пинговаться”, т.е. должна быть блокировка на OUTPUT)<br>
    ![ws2](screen/part4.1_ws2.png)*ws2*<br><br>
    <br>
    * Запустить файлы на обеих машинах командами `sudo chmod +x /etc/firewall.sh` && `sudo sh /etc/firewall.sh`<br>
    ![ws1](screen/part4.2_ws1.png)*ws1*<br><br>
    ![ws2](screen/part4.2_ws2.png)*ws2*<br><br>
    <br>
    * **ws1** - INPUT для пакетов на ping-reply DROP - не работает т.е. пакеты отправляет, но не принемает.<br>
    ![ws1](screen/part4.3_ws1.png)*ws1*<br><br>
    * **ws2** - INPUT для пакетов на ping-reply ACCEPT - работает.<br>
    ![ws2](screen/part4.3_ws2.png)*ws2*<br><br>
    <br>
2. Утилита **nmap**<br>
    * Устанавливаем **nmap** `sudo apt-get install nmap`<br>
    * **ws1** - `ping -c 3 172.24.116.8`<br>
    ![ws1](screen/part4.4_ws1.png)*ws1*<br><br>
    * **ws2** - `ping -c 3 192.168.100.10`
    ![ws2](screen/part4.4_ws2.png)*ws2*<br><br>
    <br>
## Part 5. Статическая маршрутизация сети<br>
1. Настройка адресов машин<br>
    * Настроить конфигурации машин в `etc/netplan/00-installer-config.yaml`<br>
    ![ws11](screen/part5_ws11.png)*ws11*<br><br>
    ![ws21](screen/part5_ws21.png)*ws21*<br><br>
    ![ws22](screen/part5_ws22.png)*ws22*<br><br>
    ![r1](screen/part5_r1.png)*r1*<br><br>
    ![r2](screen/part5_r2.png)*r2*<br><br>
    <br>
    * Перезапустить сервис сети. Если ошибок нет, то командой `ip -4 a` проверить, что адрес машины задан верно. Также пропинговать **ws22** && **ws21**. Аналогично пропинговать **r1** && **ws11**.<br>
    ![ws11](screen/part5.1_ws11.png)*ws11*<br><br>
    ![r1](screen/part5.1_r1.png)*r1*<br><br>
    ![ws21](screen/part5.1_ws21.png)*ws21*<br><br>
    ![ws22](screen/part5.1_ws22.png)*ws22*<br><br>
    <br>
2. Включение переадресации IP-адресов<br>
    * Для включения переадресации IP, выполните команду на роутерах: `sudo sysctl -w net.ipv4.ip_forward=1`<br>
    ![r1](screen/part5.2_r1.png)*r1*<br><br>
    ![r2](screen/part5.2_r2.png)*r2*<br><br>
    * Откройте файл `/etc/sysctl.conf` и добавьте в него следующую строку: `net.ipv4.ip_forward = 1`<br>
    ![r1](screen/part5.2.2_r1.png)*r1*<br><br>
    ![r2](screen/part5.2.2_r2.png)*r2*<br><br>
    <br>
3. Установка маршрута по-умолчанию<br>
    * Настроить маршрут по-умолчанию (шлюз) для рабочих станций. Для этого добавить **gateway4** [ip роутера] в файле конфигураций<br>
    ![ws11](screen/part5.3_ws11.png)*ws11*<br><br>
    ![ws21](screen/part5.3_ws21.png)*ws21*<br><br>
    ![ws22](screen/part5.3_ws22.png)*ws22*<br><br>
    ![r1](screen/part5.3_r1.png)*r1*<br><br>
    ![r2](screen/part5.3_r2.png)*r2*<br><br>
    <br>
    * Вызвать `ip r` и показать, что добавился маршрут в таблицу маршрутизации<br>
    ![ws11](screen/part5.3.1_ws11.png)*ws11*<br><br>
    ![ws21](screen/part5.3.1_ws21.png)*ws21*<br><br>
    ![ws22](screen/part5.3.1_ws22.png)*ws22*<br><br>
    <br>
    * Пропинговать с **ws11** роутер **r2** и показать на **r2**, что пинг доходит. Для этого использовать команду: `tcpdump -tn -i eth1`<br>
    ![ws11](screen/part5.3.2_ws11.png)*ws11*<br><br>
    ![r2](screen/part5.3.2_r2.png)*r2*<br><br>
    <br>
4. Добавление статических маршрутов<br>
    * Добавить в роутеры **r1** && **r2** статические маршруты в файле конфигураций.<br>
    ![r1](screen/part5.4_r1.png)*r1*<br><br>
    ![r2](screen/part5.4_r2.png)*r2*<br><br>
    * Вызвать `ip r` и показать таблицы с маршрутами на обоих роутерах.<br>
    ![r1](screen/part5.4.1_r1.png)*r1*<br><br>
    ![r2](screen/part5.4.1_r2.png)*r2*<br><br>
    * Запустить команды на **ws11**: `ip r list 10.10.0.0/18` && `ip r list 0.0.0.0/0`<br>
    ![ws11](screen/part5.4.2_ws11.png)*ws11*<br><br>
    * В отчете выбран путь отличный от **10.10.0.0** - этот адрес указывает на все адреса.<br>
    <br>
5. Построение списка маршрутизаторов<br>
    * Запустить на **r1** команду дампа: `tcpdump -tnv -i enp0s8`<br>
    ![r1](screen/part5.5_r1.png)*r1*<br><br>
    * При помощи утилиты `traceroute` построить список маршрутизаторов на пути от **ws11** до **ws21** `traceroute 10.20.0.10`<br>
    ![ws11](screen/part5.5_ws11.png)*ws11*<br><br>
    * Путь строится от узла к узлу до того момента, пока не будет достигнута конечная точка. Каждый пакет проходит на своем пути определенное количество узлов, пока не достигнет своей цели. На каждом узле добавляется счетчик, который отслеживает количество пройденых узлов.<br>
    <br>
6. Использование протокола **ICMP** при маршрутизации<br>
    * Запустить на **r1** перехват сетевого трафика, проходящего через **enp0s8** с помощью команды: `tcpdump -n -i enp0s8 icmp`<br>
    ![r1](screen/part5.6_r1.png)*r1*<br><br>
    * Пропинговать с **ws11** несуществующий **IP** (например, **10.30.0.111**) с помощью команды: `ping -c 1 10.30.0.111`<br>
    ![ws11](screen/part5.6_ws11.png)*ws11*<br><br>
    <br>
## Part 6. Динамическая настройка IP с помощью DHCP<br>
1. Для **r2** настроить в файле `/etc/dhcp/dhcpd.conf` конфигурацию службы **DHCP**:<br>
    * указать адрес маршрутизатора по-умолчанию, DNS-сервер и адрес внутренней сети.<br>
    ![r2](screen/part6_r2.png)*r2*<br><br>
    <br>
2.  * в файле `/etc/resolv.conf` прописать `nameserver 8.8.8.8.`<br>
    ![r2](screen/part6.1_r2.png)*r2*<br><br>
    * Перезагрузить службу **DHCP** командой `systemctl restart isc-dhcp-server`<br>
    ![r2](screen/part6.2_r2.png)*r2*<br><br>
    * Машину **ws21** перезагрузить при помощи `sudo reboot` и через `ip a` показать, что она получила адрес.<br>
    ![ws21](screen/part6.3_ws21.png)*ws21*<br><br>
    * Также пропинговать **ws22** && **ws21**.<br>
    ![ws22](screen/part6.4_ws22.png)*ws22*<br><br>
    ![ws21](screen/part6.4_ws21.png)*ws21*<br><br>
    * Указать MAC адрес у **ws11**, для этого в `etc/netplan/00-installer-config.yaml` надо добавить строки: **macaddress: 10:10:10:10:10:BA**, **dhcp4: true**<br>
    ![ws11](screen/part6.5_ws11.png)*ws11*<br><br>
    * Для **r1** настроить аналогично **r2**, но сделать выдачу адресов с жесткой привязкой к **MAC-адресу (ws11)**. Провести аналогичные тесты.<br>
    ![r1](screen/part6_r1.png)*r1*<br><br>
    * в файле `/etc/resolv.conf` прописать `nameserver 8.8.8.8.`<br>
    ![r1](screen/part6.1_r1.png)*r1*<br><br>
    * Перезагрузить службу **DHCP** командой `systemctl restart isc-dhcp-server`<br>
    ![r1](screen/part6.2_r1.png)*r1*<br><br>
    * Машину **ws11** перезагрузить при помощи `sudo reboot` и через `ip a` показать, что она получила адрес.<br>
    ![ws11](screen/part6.3_ws11.png)*ws11*<br><br>
    <br>
3. Запросить с ws21 обновление ip адреса<br>
    * В отчёте поместить скрины ip до и после обновления.<br>
    ![ws21](screen/part6.6_ws21.png)*ws21*<br><br>
    ![ws21](screen/part6.7_ws21.png)*ws21*<br><br>
    * В отчёте описать, какими опциями DHCP сервера пользовались в данном пункте.<br>
    * **dhclient -r** && **dhclient -v**<br>

## Part 7. NAT<br>
1. В файле `/etc/apache2/ports.conf` на **ws22** && **r2** изменить строку **Listen 80** на **Listen 0.0.0.0:80**, то есть сделать сервер **Apache2** общедоступным<br>
    ![ws22](screen/part7_ws22.png)*ws22*<br><br>
    ![r2](screen/part7_r2.png)*r2*<br><br>
    * Запустить веб-сервер **Apache** командой `service apache2 start` на **ws22** && **r1**<br>
    ![ws22](screen/part7.1_ws22.png)*ws22*<br><br>
    ![r1](screen/part7.1_r1.png)*r1*<br><br>
    * Добавить в фаервол, созданный по аналогии с фаерволом из **Части 4**, на **r2** следующие правила:<br>
    1) Удаление правил в таблице **filter** - `iptables -F`<br>
    2) Удаление правил в таблице **NAT** - `iptables -F -t nat`<br>
    3) Отбрасывать все маршрутизируемые пакеты - `iptables --policy FORWARD DROP`<br>
    ![r2](screen/part7.2_r2.png)*r2*<br><br>
    * Запускать файл также, как в **Части 4.**<br>
    ![r2](screen/part7.3_r2.png)*r2*<br><br>
    * Проверить соединение между **ws22** && **r1** командой `ping`<br>
    * При запуске файла с этими правилами, **ws22 не должна** "пинговаться" с **r1**<br>
    ![ws22](screen/part7.4_ws22.png)*ws22*<br><br>
    * Добавить в файл ещё одно правило:<br>
    4) Разрешить маршрутизацию всех пакетов протокола **ICMP**<br>
    ![r2](screen/part7.5_r2.png)*r2*<br><br>
    ![r2](screen/part7.6_r2.png)*r2*<br><br>
    * Проверить соединение между **ws22** && **r1** командой `ping`<br>
    * При запуске файла с этими правилами, **ws22 должна** "пинговаться" с **r1**<br>
    ![r1](screen/part7.7_r1.png)*r1*<br><br>
    * Добавить в файл ещё два правила:<br>
    5) Включить **SNAT**, а именно маскирование всех локальных **ip** из локальной сети, находящейся за **r2** (по обозначениям из **Части 5** - **сеть 10.20.0.0**)<br>
    6) Включить **DNAT** на **8080 порт** машины **r2** и добавить к веб-серверу **Apache**, запущенному на **ws22**, доступ извне сети<br>
    ![r2](screen/part7.8_r2.png)*r2*<br><br>
    * апускать файл также, как в **Части 4**<br>
    ![r2](screen/part7.9_r2.png)*r2*<br><br>
    * Проверить соединение по **TCP** для **DNAT**, для этого с **r1** подключиться к серверу **Apache** на **ws22** командой `telnet` (обращаться по адресу **r2** и порту **8080**)<br>
    ![r1](screen/part7.10_r1.png)*r1*<br><br>

## Part 8. Дополнительно. Знакомство с SSH Tunnels<br>
1. Запустить веб-сервер Apache на ws22 только на localhost (то есть не изменять файл /etc/apache2/ports.conf или, если был изменен ранее, вернуть строку Listen 80)<br>
    ![ws22](screen/part8_ws22.png)*ws22*<br><br>
    ![ws22](screen/part8.1_ws22.png)*ws22*<br><br>
    * Воспользоваться Local TCP forwarding с ws21 до ws22, чтобы получить доступ к веб-серверу на ws22 с ws21<br>
    ![ws21](screen/part8.2_ws21.png)*ws21*<br><br>
    ![ws22](screen/part8.3_ws22.png)*ws22*<br><br>
    * Воспользоваться Remote TCP forwarding c ws11 до ws22, чтобы получить доступ к веб-серверу на ws22 с ws11<br>
    ![ws11](screen/part8.4_ws11.png)*ws11*<br><br>
    * Для проверки, сработало ли подключение в обоих предыдущих пунктах, перейдите во второй терминал (например, клавишами Alt + F2) и выполните команду: `telnet 127.0.0.1 [локальный порт]`<br>
    ![ws11](screen/part8.5_ws11.png)*ws11*<br><br>
    <br>
    ![omg](screen/part8.6.png)*omg*<br><br>