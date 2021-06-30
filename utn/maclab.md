## PAT

**PAT** (port addres translation) es una variante del NAT. incorpora asignación dinámica de puertos en cada comunicación. capa 4 (transporte) del modelo OSI (el NAT trabaja en la capa 3, de RED, ya que solo gestiona direccionamiento IP). por ejemplo, 3 direcciones ip privadas son todas traducidas a una IP pública única pero con puerto distinto (en la máquina de destino)

| source | dest |
| ----- | ---- |
| 10.10.10.1:21 | 200.10.90.17:5001 |
| 10.10.10.2:80 | 200.10.90.17:5002 |
| 10.10.10.3:23 | 200.10.90.17:5003 |

de esta manera presentará a los equipos al exterior



nat: 192.168.0.185 -->  10.23.12.45 (PUBLIC IP ADDRESS)
pat: 192.168.0.185:1001 --> 10.23.12.45:1001

1. source 192.168.0.185:22 se quiere comunicar con X
2. el router recibe esa ip y
  2.1 natea: 192.168.0.185 se convierte en 10.23.12.45 (la ip pública del router)
  2.2 pat agrega un puerto aleatorio a la ip pública (en vez de usar una ip pública nueva)
3. el router manda el pedido al destino, ip 89.240.73.50

si yo estoy haciendo una comunicación SSH - a través del puerto 22, pat también cambia ese puerto? o por ejemplo, me quiero comunicar con un webserver en el puerto 80, PAT cambia el puerto a uno aleatorio?

pat is the most popular version of NAT

router looks at the ip address (private) and the internal port assigned to the machine and looks at the destination ip and port number:

- device sends request:
  - source: 192.168.0.1:100023
  - dest:   55.66.77.88:80
- router: 
  - source: 11.22.33.44:100023   ip pública nateada
  - dest:   55.66.77.88:80
- server responds: 
  - source: 55.66.77.88:80
  - dest:   11.22.33.44:100023
- router:
  - source: 55.66.77.88:80
  - dest:   192.168.0.1:100023  ip privada desnateada

se usa el __puerto__ para distinguir a qué dispositivo pertenecen los datos (la request) y a qué aplicación pertenece.

PAT no traduce el puerto, si no que lo MANTIENE durante toda la comunicación para que el router pueda encontrar el dispositivo correcto.

<https://www.youtube.com/watch?v=MrslAxSNJkI>
<https://www.youtube.com/watch?v=qij5qpHcbBk>
<https://study-ccna.com/port-address-translation-pat-configuration/>
<https://www.cisco.com/assets/sol/sb/RV320_Emulators/RV320_Emulator_v1-1-0-09/help/Setup13.html>
<https://www.geeksforgeeks.org/difference-between-network-address-translation-nat-and-port-address-translation-pat/>

## Ejercicio Número 2 Unidad 3

### Completar con direccionamiento y puertos, utilizando el protocolo PAT (subirlo al foro, no mandar por mail). Se solicita: IPs origen, IPs destino, puerto origen, puerto destino, de cada una de las PCs. Por otro lado, a nivel WAN, se pide una IP pública y el puerto identificador para cada servicio.

---------IMAGEN

- IPs y puerto de origen

| pc | ip | puerto |
| --- | --- | ---- |
| 1 | 192.168.0.100 | 1055 |
| 2 | 192.168.0.150 | 1056 |
| 3 | 129.168.0.200 | 1057 |

- IPs y puerto de destino

| pc | ip | puerto |
| ---- | ----- | ---- |
| 1 | 10.243.80.17 | 22 |
| 1 | 89.240.73.50 | 80 |
| 1 | 123.13.90.32 | 631 |

- a nivel WAN, se pide una IP pública y el puerto identificador para cada servicio

| pc | ip | puerto |
| ---- | ----- | ---- |
| 1 | 190.18.235.10 | 1055 |
| 2 | 190.18.235.10 | 1056 |
| 3 | 190.18.235.10 | 1057 |

- Resumen

| pc | ip privada | puerto | | ip pública | puerto id | | ip destino | puerto |
| --- | --- | --- | --- | ---- | --- | --- | --- | --- |
| 1 | 192.168.0.100 | 1055 | --- | 190.18.235.10 | 1055 | --- | 10.243.80.17 | 22 |
| 2 | 192.168.0.150 | 1056 | --- | 190.18.235.10 | 1056 | --- | 89.240.73.50 | 80 |
| 3 | 192.168.0.200 | 1057 | --- | 190.18.235.10 | 1057 | --- | 123.13.90.32 | 631 |

## ARP

dirección MAC: identificador único a nivel mundial para cada dispositivo de 48 bits para identificar la totalidad de dispositivos de red, como por ejemplo tarjetas de red ethernet, inalámbricas, switches, impresoras...

los primeros 24 bits pertenecen al OUI y los últimos 24 los asigna el vendedor.

la mac address se graba en formato fimario en una memoria ROM del dispositivo, en el hardware mismo.

cambiar la MAC address: cuando arranca la compu, la tarjeta de red copia la dirección MAC a nuestra memoria RAM. si queremos cambiar nuestra MAC tan solo tenemos que modificar la MAC address almacenada en nuestra memoria RAM.

ARP es un protocolo de la capa de enlace de datos responsable de encontrar la MAC address que corresponde a una determinada dirección IP. en ethernet, la capa de enlace trabaja con direcciones físicas.

ARP traduce direcciones IP en direcciones MAC (que son físicas). para realizar esta conversión, el nivel de enlace utiliza las tablas ARP - cada interfaz tiene tanto una dirección IP como una dirección física MAC: `arp -a`

## DNS

FQDN - fully qualified domain name: es.kioskea.net. DNS permite asociar nombres en lenguaje normal con direcciones ip numéricas. esta correlación entre las direcciones IP y el nombre de dominio asociado se llama resolución (de nombres) de dominio.

la estructura del sistema DNS es arbórea, en donde se definen los dominios de nivel superior (TLD, top level domains). la raíz se identifica por un punto.

- host: www           corresponde a un equipo o entidad en la red
- dominio: facebook   
- TLD: com
- Raíz: .

cada nodo del árbol se llama nombre de dominio (máx length 63 chars). cada nodo está separado por el siguiente nodo por un punto.

FQDN: nombre absoluto que termina en un punto final. el FQDN permite ubicar de manera única un equipo en internet.

DNS server: permiten establecer la relación entre los nombres de dominio y las direcciones IP de los equipos de una red. todos los dominios tienen un DNS server principal y uno secundario.

cada dns server está especificado en el dns server en el nivel superior inmediato, lo que significa que la atuoridad sobre los dominios --> delegación (de dominio?).

los servidores relacionados con los dominios de nivel superior (TLD) se llaman 'servidores de dominio de nivel superior'. son 13, están distribuidos por todo el mundo y sus nombres van desde "a.root-servers.net" hasta "m.root-servers.net"

resolución de nombre de dominio: mecanismo que consiste en encontrar la dirección ip relacionada al nombre un ordenador. hay una aplicación en el OS que se llama resolución.

- tipos de registros: un dns es una base de datos distribuida que contiene registros que se conocen como RR (registros de recursos) relacionados con nombres de dominio. dado que el sistema de memoria caché permite que el sistema DNS sea distribuido, los registros para cada dominio tienen una duración de vida que se conoce como TTL (tiempo de vida). por lo general un registro DNS contiene la siguiente información:

| FQDN | TTL | tipo | clase | RData |
| ---- | ---- | ---- | ---- | ----- |
| es.kioskea.net | 3600 | A | IN | 163.5.255.85 |

### TLD

dos tipos:

1. gTLD, genéricos, ofrecen una clasificación de acuerdo con el sector de la actividad
  1. históricos: .arpa, .com (inicialmente relacionado con empresas con fines comerciales), .edu (instituciones educativas), .gov (gobiernos), .int (org internacionales), .net (org que administran redes), .org (org sin fines de lucro)
  2. nuevos: .aero (industria aeronáutica), .biz (negocios), .museum, .name, .info, .coop. .pro
  3. especiales: infraestructura para la administración de redes
2. ccTLD country code - AR (argentina), ES (españa)...

## Ejercicio Número 3 Unidad 3

### Utilizar y probar el comando “nslookup”, usar como guía el help del mismo comando. Buscar 3 direcciones IP y resolverlas a través del mismo comando.

```console
ARGMAC015:~ jose.aliaga$ nslookup resolvit.com
Server:		8.8.8.8
Address:	8.8.8.8#53

Non-authoritative answer:
Name:	resolvit.com
Address: 198.55.245.164

ARGMAC015:~ jose.aliaga$ nslookup office365.com
Server:		8.8.8.8
Address:	8.8.8.8#53

Non-authoritative answer:
Name:	office365.com
Address: 52.165.129.203
Name:	office365.com
Address: 13.90.213.204

ARGMAC015:~ jose.aliaga$

ARGMAC015:~ jose.aliaga$ nslookup mercadolibre.com.ar
Server:		8.8.8.8
Address:	8.8.8.8#53

Non-authoritative answer:
Name:	mercadolibre.com.ar
Address: 13.227.92.90
Name:	mercadolibre.com.ar
Address: 13.227.92.12
Name:	mercadolibre.com.ar
Address: 13.227.92.15
Name:	mercadolibre.com.ar
Address: 13.227.92.74

ARGMAC015:~ jose.aliaga$
```

## DHCP

proveer las configuraciones necesarias de conectividad a los dispositivos. gracias a este servicio no es necesario configurar un dispositivo en forma manual - el solo hecho de conectarlo a la red hace que dicho dispositivo tome una dirección automáticamente

1. dispositivo se conecta a la red
2. dispositivo envia paquetes broadcast **DHCPDISCOVER** para encontrar el servidor DHCP
3. el servidor DHCP, al recibir la solicitud, reserva de su address pool una dirección asignada a la MAC del dispositivo solicitante y le envía una respuesta con un paquete unicast llamado **DHCPOFFER** donde indica un resumen del segmento de red.
4. este paquete lo recibe únicamente el dispositivo solicitante.
5. una vez el dispositivio reciba el DHCPOFFER, enviará un **DHCPREQUEST**, que simboliza el pedido oficial de obtención de su dirección IP y la conexión a la red
6. el servidor lo recibe, asigna la IP reservada anteriormente y envía un **DHCPACK** en el cual notifica la aceptación del servidor, junto con la lista completa de opciones de config más un tiempo de la duración de la reserva

## Ejercicio Número 4 Unidad 3

### Explicar el proceso de DHCP en este dibujo, y especificar cómo sería el direccionamiento IP que ofrecería a los dispositivos (la máscara es 255.255.255.0 o podría ser la 255.255.0.0)


Dentro de una red hay un servidor DHCP con un rango de IPs privadas sin usar, con una submáscara de 255.255.0.0 y unas IPs que arrancan con 192.168.0.0/16. Este servidor DHCP tendrá disponible para otorgar 65.534 IPs privadas (<http://jodies.de/ipcalc?host=192.168.0.1&mask1=16&mask2=>).

- Cuadro 1: cuando entra un nuevo dispositivo a la red, envia paquete broadcast **DHCPDISCOVER** hasta que encuentra el servidor DHCP de la red.
- Cuadro 2: el servidor DHCP responde con un paquete unicast llamado **DHCPOFFER** _únicamente_ al dispositivo nuevo. En este DHCPOFFER se envía una IP tentativa.
- Cuadro 3: el nuevo dispositivo, que ya sabe dónde está el servidor DHCP, envía un paquete **DHCPREQUEST** que simboliza el pedido oficial de una dirección IP dentro del rango de IPs dispoibles.
- Cuadro 4: finalmente el servidor DHCP reserva la IP pactada y envía un paquete **DHCPACK** donse especifican las opciones de configuración además del tiempo que dura la reserva de la IP.

### AYUDA: hay un servicio que todavía no se enseñó que permitiría el uso de dos segmentos de red diferentes a través de un SW, ¿cuál es?

Creo que se refiere al servicio de subnetting, donde usamos segmentos para lógicos para separar redes.


