# WIRESHARK CHEAT SHEET

## Operadores lógicos

| Operador | Descripción |
| ------------ | ------------  |
|and o && | Y lógico, Todas las condiciones deben coincidir |
|or o \|\| | O lógico, Todas o una de las condiciones deben coincidir|
|xor o ^^ | XOR lógico, sólo debe coincidir una de las dos condiciones, no ambas |
|not o !	| Not (Negación), No igual a |
|[ n ] [ ... ] | Operador de subcadena Filtrar una palabra o texto específico |

## Filtros de paquetes

| Operador | Descripción | Ejemplo |
| ------------ | ------------  | ------------  |
| eq o == | Igual | ip.dest == 192.168.1.1 |
| ne o != | No igual | ip.dest != 192.168.1.1 |
| gt o > | Mayor que | frame.len > 10 |
| it o < | menor que | frame.len < 10 |
| ge o >= | Mayor o igual que | frame.len >= 10 |
| le o <= | menor o igual que | frame.len <= 10 |

## Filtros comunes

| Uso | Ejemplo |
| ------------ | ------------ |
|Filtrar por IP | ip.add == 10.10.50.1 |
|Filtrar por IP de destino | ip.dest == 10.10.50.1 |
|Filtrar por IP de origen | ip.src == 10.10.50.1 |
|Filtrar por rango de IP | ip.addr >= 10.10.50.1 and ip.addr <=10.10.50.100 |
|Filtrar por múltiples ip | ip.addr == 10.10.50.1 and ip.addr == 10.10.50.100 |
|Filtrar direcciones IP diferentes a | ! (dirección ip == 10.10.50.1) |
|Filtrar subred | ip.addr == 10.10.50.1/24 |
|Filtrar por puerto | tcp.port == 25 |
|Filtrar por puerto de destino (TCP) | tcp.dstport == 23 |
|Filtrar por puerto de destino (UDP) | udp.dstport == 123 |
|Filtrar por dirección ip y puerto | ip.addr == 10.10.50.1 and Tcp.port == 25 |
|Filtrar por URL | http.host == "nombre de host" |
|Filtrar por peticiones http | http.request |
|Filtrar por marca de tiempo | frame.time >= "June 02, 2019 18:04:00" |
|Filtrar por flag SYN | Tcp.flags.syn == 1 and tcp.flags.ack ==0 |
|Filtrar por beacon | wlan.fc.type_subtype = 0x08 |
|Filtrar por broadcast | eth.dst == ff:ff:ff:ff:ff:ff |
|Filtrar por multicast | (eth.dst[0] & 1) |
|Filtrar por nombre de host | ip.host = hostname |
|Filtrar por dirección MAC | eth.addr == 00:70:f4:23:18:c4 |
|Filtrar por flag RST | tcp.flag.reset == 1 |
