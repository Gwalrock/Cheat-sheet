# NMAP CHEAT SHEET

## Reconocimiento de objetivo e identificación

| Uso | Ejemplo |
| ------------ | ------------ |
|Mostrar ayuda  | nmap -h|
|Escaneo básico  | nmap <objetivo>|
|Lanzar un escaneo ping (subred) | nmap -sn <objetivo> Ej: nmap -sn 192.168.1.0/24|
|Escanear una lista de objetivos | nmap -iL [objetivos.txt]|
|Escaneo ping con traceroute | nmap -sn --traceroute acme.org ejemplo.org|
|Ping TCP SYN | nmap -PS <objetivo>|
|Ping UDP | nmap -PU <objetivo>|
|Escanear objetivo IPv6 | nmap -6 <objetivo>|
|Especificar script NSE | nmap -sn --script dns-brute ejemplo.org|
|Asignar manualmente servidores DNS | nmap --dns-servers <servers> <objetivo>|
|Detección ARP | nmap -PR <objetivo> Ej: nmap -PR 192.168.1.0/24|
|Descubrimiento UDP en el puerto especificado | nmap -PU53 <objetivo>|
|Sin resolución DNS | nmap -n <objetivo>|
|Seleccionar interfaz de red | nmap -e <interfaz> <objetivo>|
|Omitir descubrimiento de host | nmap -Pn <objetivo>|

## Detección de versiones

| Uso | Ejemplo |
| ------------ | ------------ |
|Detección de servicios | nmap -sV <objetivo> Ej: nmap -sV scanme.nmap.org|
|Detección de SO | nmap -O <objetivo>|
|Intentar adivinar el SO | nmap -O --osscan-guess <objetivo>|
|Aumentar la detección de versiones | nmap -sV --version-intensity <0-9> <objetivo>|
|Solucionar problemas de escaneado de versiones | nmap -sV --version-trace <objetivo>|
|Modo de detección agresivo | nmap -A <objetivo>|
|Modo detallado | nmap -O -v <objetivo>|

## Red y escaneo de puertos

| Uso | Ejemplo |
| ------------ | ------------ |
|Escaneo de ping TCP SYN | nmap -sn -PS <objetivo> o nmap -sS|
|Escaneo de todos los puertos | nmap -P- <objetivo>|
|Escaneo de múltiples puertos | nmap -sn -PS80,100-1000 <objetivo>|
|Escaneo de ping TCP ACK | nmap -sn -PA <objetivo> o nmap -sA|
|Escaneo de ping UDP | nmap -sn -PU <objetivo>|
|Escaneo de ping ICMP | nmap -sn -PE <objetivo>|
|Escaneo de ping SCTP INIT | nmap -sn -PY <objetivo> o nmap -sY|
|Escaneo de ping de protocolo IP (rastreo) | nmap -sn -PO --packet-trace <objetivo>|
|Escanear un número aleatorio de hosts | nmap -iR [número]|
|Escaneo de ping de difusión | nmap --script broadcast-ping --packet-trace|
|Escaneo Xmas (Establece las banderas FIN, PSH y URG) | nmap -sX <objetivo>|
|Escaneo UDP (con verbosidad) | nmap -sU -v <objetivo>|
|Escanear un cortafuegos (dividir la cabecera TCP en pequeños fragmentos) | nmap -f <objetivo>|
|Ocultar un escaneo con señuelos | nmap -D <decoy1>[,<decoy2>] <objetivo>Ex: nmap -D 192.168.1.101,192.168.1.102 <objetivo>|
|Suplantación de la dirección IP de origen | nmap -S <dirección_IP> <objetivo>|
|Dirección MAC falsa | nmap --spoof-mac [MAC] <objetivo|
|Escanear utilizando una dirección MAC aleatoria | nmap -v -sT -PN --spoof-mac 0 <objetivo>|

## Rendimiento y velocidad

| Uso | Ejemplo |
| ------------ | ------------ |
|Ajuste retardo básico | nmap --scan-delay <time>|
|Ajustar retardo entre pruebas | nmap --scan-delay <time>; --max-scan-delay <time>|
|Modo paranóico | nmap -T0 <objetivo>|
|Modo furtivo | nmap -T1 <objetivo>|
|Cortes – Más lento que el normal | scan nmap -T2 <objetivo>|
|Normal – Velocidad por defecto | nmap -T3 <objetivo>|
|Agresivo | nmap -T4 -n -Pn -p- <objetivo>|
|Insane – el más rápido | nmap -T5 <objetivo>|
|Host timeouts | nmap -sV -A -p- --host-timeout 5m <objetivo>|
|Enviar paquetes a una velocidad no inferior a <número> por segundo| nmap –min-rate <number> <objetivo>|
|Enviar paquetes no más rápido que <número> por segundo| nmap –max-rate <number> <objetivo>|

## Scripts nse

| Uso | Ejemplo |
| ------------ | ------------ |
|Categoría segura - Por defecto | nmap -sC <host> Ej: nmap -sC scanme.nmap.org|
|Ejecutar (múltiples) scripts por nombre | nmap --script default,safe|
|Seleccionar script por categoría | nmap --script exploit <objetivo>|
|Ejecutar el archivo de script NSE | nmap --script /ruta/a/script.nse <objetivo>|
|Excluir una categoría específica | nmap -sV --script "not exploit" <objetivo>|
|Incluir dos categorías diferentes | nmap --script "broadcast and discovery" <objetivo>|
|Combinar comodines | nmap --script "http-*" <objetivo>|
|Establecer argumentos | nmap -sV --script http-title --script-args http.useragent="Mozilla 1337"<objetivo>|
|Cargar argumentos de un archivo | nmap --script "discovery" --script-args-file nmap-args.txt<objetivo>|

## Escaner de servidores web

| Uso | Ejemplo |
| ------------ | ------------ |
|Lista de métodos HTTP compatibles | nmap -p80,443 --script http-methods --script-args httpmethods.test-all=true <objetivo>|
|Descubrir rutas/carpetas interesantes | nmap --script http-enum -sV <objetivo>|
|Fuerza bruta HTTP basic auth | nmap -p80 --script http-brute <objetivo>|
|Proporcionar una lista propia de usuarios/contraseñas | nmap -sV --script http-brute --script-args userdb=usernames.txt,passdb=passwords.txt <objetivo>|
|Fuerza bruta a plataformas web comunes (por ejemplo, WordPress) | nmap -sV --script http-wordpress-brute <objetivo>|
|Detectar un cortafuegos de aplicaciones web | nmap -sV --script http-waf-detect,http-waf-fingerprint<objetivo>|
|Detectar vulnerabilidades XST (a través del método HTTP TRACE) | nmap -sV --script http-methods,http-trace --script-argshttp-methods.retest <objetivo>|
|Detectar vulnerabilidades XSS | nmap -sV --script http-unsafe-output-escaping <objetivo>|
|Detectar vulnerabilidades de inyección SQL | nmap -sV --script http-sql-injection <objetivo>|
|Encontrar credenciales por defecto | nmap -sV --script http-default-accounts <objetivo>|
|Encontrar repositorios Git expuestos | nmap -sV --script http-git <objetivo>|

## Escaner de servidores de correo

| Uso | Ejemplo |
| ------------ | ------------ |
|Fuerza bruta SMTP | nmap -p25 --script smtp-brute <objetivo>|
|Fuerza bruta IMAP | nmap -p143 --script imap-brute <objetivo> (destino)|
|Fuerza bruta POP3 | nmap -p110 --script pop3-brute <objetivo>|
|Enumerar usuarios | nmap -p 25 --script=smtp-enum-users <objetivo>|
|SMTP ejecutándose en puerto(s) alternativo(s) | nmap -sV --script smtp-strangeport <objetivo>|
|Descubrir open relay | nmap -sV --script smtp-open-relay -v <objetivo>|
|Encontrar comandos SMTP disponibles | nmap -p 25 --script=smtp-commands <objetivo>|

## Escaner de base de datos

| Uso | Ejemplo |
| ------------ | ------------ |
|Identificar servidores MS SQL | nmap -p1433 --script ms-sql-info <objetivo>|
|Fuerza bruta de contraseñas MS SQL | nmap -p1433 --script ms-sql-brute <objetivo>|
|Volcar hashes de contraseñas (MS SQL) | nmap -p1433 --script ms-sql-empty-password,ms-sql-dump-hashes<objetivo>|
|Listar bases de datos (MySQL) | nmap -p3306 --script mysql-databases --script-args mysqluser=[usuario],mysqlpass=[contraseña] <objetivo>|
|Fuerza bruta de contraseñas MySQL | nmap -p3306 --script mysql-brute <objetivo>|
|Cuentas Root/Anónimas con contraseñas vacías | nmap -p3306 --script mysql-empty-password <objetivo>|
|Fuerza bruta Oracle SIDs | nmap -sV --script oracle-sid-brute <objetivo>|
|Identificar servidores MongoDB | nmap -p27017 --script mongodb-info <objetivo>|
|Identificar bases de datos CouchDB | nmap -p5984 --script couchdb-databases <objetivo>|
|Identificar bases de datos Cassandra | nmap -p9160 --script cassandra-brute <objetivo>|
|Fuerza bruta Redis | nmap -p6379 --script redis-brute <objetivo>|

## Escaner de ICS/SCADA

| Uso | Ejemplo |
| ------------ | ------------ |
|Detectar puertos estándar (abiertos) | nmap -Pn -sT --scan-delay 1s --max-parallelism 1-p80,102,443,502,1089, 1091,2222,4000,4840, 20000,34962,34964, 34980,44818,47808, 55000,55003 <objetivo>|
|Puertos del sistema de control (BACnet/IP) | nmap -Pn -sU -p47808 --script bacnet-info <objetivo>|
|Ethernet/IP | nmap -Pn -sU -p44818 --script enip-info <objetivo>|
|Descubrir un dispositivo Modbus | nmap -Pn -sT -p502 --script modbus-discover <objetivo>|
|Descubrir un dispositivo Niagara Fox | nmap -Pn -sT -p1911,4911 --script fox-info <objetivo>|
|Descubrir un dispositivo PCWorx | nmap -Pn -sT -p1962 --script pcworx-info <objetivo>|

## Generar informes

| Uso | Ejemplo |
| ------------ | ------------ |
|Salida normal a nombre de archivo | nmap -oN [nombre de archivo] <objetivo>|
|Enviar los resultados al formato XML | nmap -oN [nombrearchivo] -oX <nombrearchivo.xml> <objetivo>|
|Enviar los resultados a todos los formatos (Normal, XML y grep) | nmap -oA [filename] <objetivo>|
|Aumenta los niveles de verbosidad y depuración | nmap -v3 -d2 -oN [filename] <objetivo>|
|Mostrar razones de estado de host y puerto | nmap --reason <objetivo>|
|Imprimir estadísticas de temporización periódicas | nmap -Pn <objetivo> --stats-every 10s|
|Rastrear paquetes y datos enviados y recibidos | nmap -T4 --packet-trace <objetivo>|
|Mostrar sólo los puertos abiertos | nmap --open <objetivo>
|Listar interfaces y rutas | nmap --iflist
