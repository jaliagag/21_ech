# Experto Universitario en Hacking Ético

```md
El mail mio para la presentación de ejercicios es : banchiero.UTN@gmail.com
```

MITM

forward traffic on linux: `sysctl -w net.ipv4.ip_forward=1`

## links de interés

- OSINT:
  - <https://centralops.net/co/>
  - <https://www.robtex.com/>
- tools:
  - <https://github.com/ElevenPaths/EvilFOCA>
  - software ids:
    - <https://www.snort.org/>
    - <https://suricata.io/>
- test and lab:
  - <https://archive.org/search.php?query=subject%3A%22IEVM%22>
- scanner de vulnerabilidades: NESSUS
- scanner:
  - NIKTO
  - WPSCAN
  - SKIPFISH
- dispositivos: IPS/FIREWALL
- CVE: sistema de identificación de vulnerabilidades
- w3af: scan de vulnerabilidades
- Nirsoft
- Sysinternals
  

## unidad 1

ejercicios

1- OR, NOT, XOR

OR: siempre que haya una señal, la salida se activa; solo es inactiva si todas las señales son 0. en un grupo de amigos, con que uno solo salga al boliche, se considera que "el grupo salió".

NOT: es una u otra, solo tiene una señal y si es una, quiere decir que no es la otra y viceversa. dos grupos que son archienemigos entre sí solo pueden salir al boliche cuando el otro no salió.

XOR: se activa cuando las entradas son diferentes y desactiva cuando son iguales - dos amigos saldrán solamente si son diferentes y no saldrán si son iguales (aburrido)

2- mis inicios en informática

desde que descargaba películas, series y juegos que soy el "que arregla computadoras", básicamente buscador de soluciones en google. siempre me interesó probar las nuevas características y diferencias entre los sistemas operativos.

3- 3 ejemplos de lo que podemos encontrar dentro de cada capa del modelo osi

| capa | nombre | ejemplo |
| --- | --- | ----|
| 1 | física | cables, conectores, luces, bluetooth, USB, tarjeta PCIe, rj-45 |
| 2 | enlace de datos | swtich, router, arp, modem, nic|
| 3 | nivel de red | ARP, icmp, router, ip |
| 4 | transporte | tcp, udp, gateway, firewall |
| 5 | sesión | smb, pap (printer), rpc, autenticación, autorización |
| 6 | presentación | ssl, ssh, tls, compresión, encriptación y desencriptación |
| 7 | aplicación | puertos, protocolos, APIs |

4- una ventaja y una desventaja de las topologías árbol, malla y estrella extendida

- árbol: similar a redes en estrella salvo que no tiene un concentrador central - tiene un nodo de enlace troncal (un hub o switch) desde el que se ramifican los demás nodos. combinación de bus y topología estrella.
  - ventaja
    - el fallo de un nodo no implica una interrupción en las comunicaciones
    - es muy rápida
    - facilidad de identificación y resolución de problemas
    - todas las computadoras reciben al mismo tiempo las señales transmitidas por el dispositivo central
    - compatible con muchos proveedores de hardware y software
    - monitoreo centralizado
  - desventaja
    - requiere mucho cable, es costosa
    - si se desconecta un segmento principal todo el segmento cae también
    - si se desconecta un nodo, todos los que están conectados a él se desconectan también
    - a medida que crece puede complicarse el mantenimiento
- malla
  - ventaja
    - muy resistente a fallas - si uno o varios dispositivos tienen una falla, la topología de malla puede seguir trabajando
    - fácil de escalar
    - existencia de otras vías de comunicación para entregar datos al usuario - fiabilidad
  - desventaja
    - alto gasto de mantenimiento
    - configuración inicial compleja
- estrella extendida: <https://clasificaciondelasredesblog.files.wordpress.com/2017/05/25ef1-estrellaextendida.png?w=343&h=328&zoom=2>
  - ventaja:
    - cableado es más corto y limita la cantidad de dispositivos quese deben interconectar con cualquier nodo central.
    - permite extender la longitud de la red (solo hay que incorporar nuevos conectores)
    - si un dispositivo conectado a la red se desconecta o se le rompe el cable, solo afecta a ese dispositivo
  - desventaja:
    - el cable viaja por separado del concentrador a cada computadora
    - si el nodo central falla, toda la red deja de transmitir
    - costosa, ya que requiere más cable que las topologías bus o anillo

5- tipos de topología y posibles puntos de incidencia

1. estrella extendida: routers de cada sede, principalmente el router de la sede central y los cables de ethernet que conectan la red bus interna, especialmente la red que conecta los servidores corporativos
2. árbol: si el nodo central se desconecta, es imposible la comunicación entre las dos redes. en menor medida, los hubs que conectan a los otros nodos también serían puntos de incidencia, ya que aislarían a los nodos de la red en caso de sufrir una falla

### topologías

- mesh: todos los dispositivos poseen conexiones directas hacia el resto y los enlaces entre sí son punto a punto (comienzan en un equipo y terminan en otro)
- anillo: cada estación está conectada a la _siguiente_ y la última conectada a la primera. cada estación tiene un receptor y un transmisor que hace la función de repetidor, pasando la señal (token) a la siguiente estación
- doble anillo: en ambas direcciones pero solo se usa un anillo a la vez. fault tolerant
- red estrella: todos los nodos de la red se conectan a un conectador o _hub_.
- red bus: un cable con un terminador en cada extremo del que se cuelgan todos los elementos de una red. todos los nodos de una red están unidos a este cable
- árbol: hay equipos que se conectan a un conectador primario y otros a uno secundario. menos colisiones de paquetes y el desempeño de la red sea más eficiente

<http://www.etitudela.com/fpm/comind/downloads/topologiadered.pdf>

punto de indiencia: problema si pasara algo en un dispositivo, afectando la disponibilidad, integridad o confidencialidad de la red (corte de luz, falta de backups, SPOF)

## unidad 2 - instalación y configuración en redes

### TCP/IP

TCP/IP suite de protocolos que provee los servicios necesarios para poder conectar distintos dispositivos. 4 capas

1. aplicación (1 Application, 2 presentation, 3 session). administra todas las funciones utilizadas y requeridas por las aplicaciones y los servicios que tengan una relación directa con el usuario final: HTTP, SMTP, FTP, SSH, DNS, RIP, SNMP, DHCP
2. transporte (4 transport). proveer la conectividad punta a punta entre el origen (emisor) y el destinatario (receptor) y permite intercambiar los roles de emisor y receptor dinámicamente. TCP, DCCP UDP, ICMP, FCP, UTP
3. internet (5 network). definir el esquema de direccionamiento lógico de los equipos que se conecten a la red y el direccionamiento de cada uno de los equipos de la red. servicio de enrutamiento (información de los equipos de origen y destino). IP, ICMP, IPSEC, IGMP
4. acceso a la red (6 Data link y 7 physical). protocolos encargados de preparar el ambiente físico y lógico necesario para realizar las comunicaciones. se define el modo de acceso físico a la red y la traducción del direccionamiento. ARP (data link), L2TP, NDP, ETHERNET

### protocolo ip

protocolo de comunicación en la capa de red (2). uso bidireccional (origen o destino) de comunicación para transmitir datos mediante un protocolo __no rientado a conexión__ (una comunicación entre dos puntos finales de una red en los que un mensaje puede ser enviado desde un punto final a otro _sin acuerdo previo_) que transfiere paquetes conmutados. los paquetes pueden tomar disntintas rutas para atravesar la red - no se hace contacto con el destino antes de que se envíe el paquete.

las cabeceras IP contienen las direcciones IP de las máquinas de origen y destino, que serán usadas por los routers para decidir el tramo de red por el que enviarán los paquetes.

Direccionamiento vs enrutamiento

- direccionamiento: una etiqueta que nos encontramos en el dispositivo de la red. **dentro de una red necesitamos identificar a todos los dispositivos** para la comunicación en la red. el direccionamiento privado es para la red LAN y el público para todo lo que sea WAN. todo direccionamiento no expuesto es considerado direccionamiento público. el direccionamiento IP se gestiona a nivel global por la corporación ICANN, que reparte los grandes bloques de direccionamiento a cinco regiones
  - AfriNIC
  - APNIC
  - ARIN
  - LACNIC
  - RIPE NCC

- enrutamiento: aprender la manera de encontrar un equipo  o una determinada IP dentro de esa red. en la tabla de enrutamiento, se encuentran todas laredes publicadas y/o aprendidas

una dirección ip asignada a un equipo es única.

la **máscara de red** es una combinación de bits que sirve para delimitar el ámbito de una red de computadoras. 192.168.0.0/16 - el número que aparece después de la "/" es la suma de los bits que se utilizan para la máscara de red. esa identificación se la conoce como CIDR. la función de la máscara de red es indicar a los dispositivos qué parte de la dirección IP es el número de la red, incluyendo la subred, y qué parte es la que corresponde al host.

la puerta de enlace o **gateway** es un dispositivo que permite interconectar redes con protocolos y arquitecturas diferentes a todos los niveles de comunicación. su función es traducir la información del protocolo utilizado en una red al protocolo usado en la red de destino. la default gateway indica al tráfico de red por dónde tiene que salir

Un byte está formado por 8 bits; la direcciones ip tienen 4 bytes, 32 bits. se forman SIEMPRE sumando de izquierda a derecha

| 128 | 64 | 32 | 16 | 8 | 4 | 2 | 1 | dirección |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 1 | 1 | 0 | 0 | 0 | 0 | 0 | 0 | 192 |
| 1 | 0 | 1 | 0 | 1 | 0 | 0 | 0 | 168 |
| 0 | 0 | 0 | 1 | 0 | 0 | 0 | 0 | 16 |
| 0 | 0 | 0 | 1 | 1 | 0 | 0 | 0 | 24 |

```md
Crear un informe explicando que son las bases de datos “WHOIS” y cuáles son las correspondientes a nuestra zona (continente) y país.

Las bases de datos WHOIS son un registro que identifica a quién pertenece un dominio y cómo contactarlo. la ICANN (Internet Corporation for Assigned Names and Numbers) regula el registro y a quién pertenecen los nombres de dominio. no es exclusivo de la ICANN, si no que los datos son almacenados por "registradores" que deben estar acreditados por la ICANN.

los datos que almacenan estas bases datos incluyen: nombre, domicilio, correo electrónico, número de teléfono y contactos técnicos y administrativos. estos datos son de acceso público a los datos sobre nombres registrados. WHOIS es también el protocolo que se usa para buscar en sus bases de datos e identificar al titular o "registrario" de un dominio.

En América Latina la principales bases de datos WHOIS son <https://nic.ar/es/whois>, <https://www.lacnic.net/1002/1/lacnic/whois> y ya un poco más al norte <https://www.iar.mx/jsf/static_content/services/current_services/resource_registry/whoisDatabase.jsf> o más a nivel internacional <https://ar.godaddy.com/whois>.

Buscar en Internet 4 direcciones IP y examinarlas - Transformar a las mismas en binario y subirlas al foro correspondiente

www.cordoba.gob.ar
IP: 76.223.3.255
binario: 01001100.11011111.00000011.1111111

www.dxc.com
IP: 151.101.3.10
binario: 10010111.01100101.00000011.00001010

www.resolvit.com
IP: 198.55.245.164
binario: 11000110.00110111.111110101.10100100

mail.google.com
IP: 216.58.222.37
binario: 1101100.00111010.11011110.00100101
```

### Dispositivos de seguridad de red

firewall, IDS, IPS NIDS, HIDS. dentro de los dispositivos tenemos los ACL (access control list).

#### Firewall

el firewall es un dispositivo de red cuya función principal es la de bloquear todo acceso hacia la red y desde ella mediante configuraciones llamadas reglas o políticas.

- restrictivo: lo que no sea explícitamente permitido, será negado
- permisivo: lo que no sea explícitamente negado, será permitido

Dónde se instale el firewall nos indicará cómo intermedia las comunicaciones de la red que desea inspeccionar.

- dual-homed firewall: el equipo cuenta con dos dispositivos o interfaces que permitirán interactuar tant ocon la red pública como con la privada
- multi-homed firewall: el equipo cuenta con varios dispositivos que permitirán interactuar con varias redes distintas (distintas políticas para cada red)
- DMZ (demilitarized zone) o red perimetral es una red local que se ubica entre la red interna de una organización y una red externa (internet). generalmente se posicionan en esta zona los servicios que se quieren publicar en una red pública (internet) como servidores de correo electrónico, web y dns.

servicios de firewall: packet filtering (filtrado de paquetes), application layer y statefull (recuerdo de sesiones establecidas)

#### IDS (intrusion detection systems)

los ids realizan un análisis de cada paquete que circule por su rango de cobertura. son capaces de detectar anomalías o firmas y programar acciones/reglas. un **ids basado en patrones** analiza paquetes en la red y los compara con patrones de ataque conocidos y preconfigurados. estos patrones se denominan firmas.

un **IDS basado en heurística** determina la actividad normal de la red, como el orden de ancho de banda usado, protocolos, puertos y dispositivos habituales y alerta cuando encuentra variaciones. cuenta con una base de datos (firmas) que usa para comparar y actuar en consecuencia.

- NIDS: basado en software o hardware para analizar segmentos de red donde estén conectados
- HIDS: basado en software, aplicado sobre un OS - el famoso antivirus del OS

IDS Cisco 4250

#### IPS (intrusion prevention systems)

ips analiza en tiempo real. monitorear en tiempo real. rendimiento de tráfico afectado??

- detección basada en firmas
- detección basada en políticas
- detección basada en anomalías: puede ser que el aparato mismo genere la base de la normalidad o que se fije manualmente (lo cual puede generar falsos positivos)

IPS Cisco 4265

IPS previene -> proactivo - se pone siempre antes del router del proveedor. adelante del router del proveedor no podemos poner nada. atrás todo lo que quieras
IDS detecta -> dentro de la red, ya entraron. monitorear segmentos

#### honeypot

honeypot es un sistema muy flexible dentro de la seguridad informática que se encarga de atraer y analizar el comportamiento de los atacantes en internet. sirve para atraer atacantes (?) y así capturar el tráfico de red entrante y conocer todos los detalles acerca de latendencias y metodologías de ataque de los atacantes así como los fallos de seguridad en nuestra red y así prevenirlos.

- según su implementación
  - producción: obtención de información sobre técnicas empleadas para tratar de vulnerar los sistemas que componen dicha infraestructura
  - investigación: recursos educativos
- según su interacción
  - alta interacción: sistema convencional, mal configurado para que sean atacados (metasploit?). cada interacción se considera sospechosa
  - baja interacción: investigación de nuevas amenazas en la red (máquina con vbox o vmware)

### Material adicional

L4: en ocasiones los datos que vienen de la capa de sesión (L5) exceden el tamaño máximo de transmisión (Maximum Transmission Unit o **MTU**) de la interfaz de red, por lo que es necesario partirlos y enviarlos en unidades más pequeñas - esta fragmentación y el ensamblado de paquetes se realiza en esta capa. también se realiza el control de flujo.

- protocolo: conjunto de reglas que indican cómo se debe llevar a cabo un intercambio de datos. para que dos o más nodos en una red puedan intercambiar información es necesario que manejen el mismo conjunto de reglas

## unidad 3 - redes informáticas - potenciales riegos

agujeros de seguridad (vulnerabilidades) en SO.

vulnerabilidades en aplicaciones

usuarios sin conocimientos suficientes

escáner de seguridad: nessus, tenable, openvas, nmap (`nmap -sS -v <ip>`)

tipos de técnicas de ataques de red:

1. denegación de servicio
2. contral la autenticación
3. modificación y daño a la integridad
4. deficiencias de seguridad

### nat - pat - arp - dns - dhcp

- Network Address Translation: mecanismo utilizado por routers IP para intercambiar paquetes entre dos redes que asignan mutuamente direcciones incompatibles. la mayoría de los NAT asignan varias máquins (hosts) privadas a una dirección IP expuesta públicamente (el router).
- Port Address Translation (PAT): variante de NAT que incorpora asignación dinámica de puertos en cada comunicación. trabajo(port forwarding)

#### PAT

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

#### ARP

dirección MAC: identificador único a nivel mundial para cada dispositivo de 48 bits para identificar la totalidad de dispositivos de red, como por ejemplo tarjetas de red ethernet, inalámbricas, switches, impresoras...

los primeros 24 bits pertenecen al OUI y los últimos 24 los asigna el vendedor.

la mac address se graba en formato fimario en una memoria ROM del dispositivo, en el hardware mismo.

cambiar la MAC address: cuando arranca la compu, la tarjeta de red copia la dirección MAC a nuestra memoria RAM. si queremos cambiar nuestra MAC tan solo tenemos que modificar la MAC address almacenada en nuestra memoria RAM.

ARP es un protocolo de la capa de enlace de datos responsable de encontrar la MAC address que corresponde a una determinada dirección IP. en ethernet, la capa de enlace trabaja con direcciones físicas.

ARP traduce direcciones IP en direcciones MAC (que son físicas). para realizar esta conversión, el nivel de enlace utiliza las tablas ARP - cada interfaz tiene tanto una dirección IP como una dirección física MAC: `arp -a`

#### DNS

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

los servidores relacionados con los dominios de nivel superior (TLD) se llaman 'servidores de dominio de nivel superior'. son 13, están distribuidos por todo el mundo y sus nombres van desde "a.root-ser
vers.net" hasta "m.root-servers.net"

resolución de nombre de dominio: mecanismo que consiste en encontrar la dirección ip relacionada al n
ombre un ordenador. hay una aplicación en el OS que se llama resolución.

- tipos de registros: un dns es una base de datos distribuida que contiene registros que se conocen c
omo RR (registros de recursos) relacionados con nombres de dominio. dado que el sistema de memoria ca
ché permite que el sistema DNS sea distribuido, los registros para cada dominio tienen una duración d
e vida que se conoce como TTL (tiempo de vida). por lo general un registro DNS contiene la siguiente
información:

| FQDN | TTL | tipo | clase | RData |
| ---- | ---- | ---- | ---- | ----- |
| es.kioskea.net | 3600 | A | IN | 163.5.255.85 |

#### TLD

dos tipos:

1. gTLD, genéricos, ofrecen una clasificación de acuerdo con el sector de la actividad
  1. históricos: .arpa, .com (inicialmente relacionado con empresas con fines comerciales), .edu (ins
tituciones educativas), .gov (gobiernos), .int (org internacionales), .net (org que administran redes
), .org (org sin fines de lucro)
  2. nuevos: .aero (industria aeronáutica), .biz (negocios), .museum, .name, .info, .coop. .pro
  3. especiales: infraestructura para la administración de redes
2. ccTLD country code - AR (argentina), ES (españa)...

#### DHCP

proveer las configuraciones necesarias de conectividad a los dispositivos. gracias a este servicio no es necesario configurar un dispositivo en forma manual - el solo hecho de conectarlo a la red hace que dicho dispositivo tome una dirección automáticamente

1. dispositivo se conecta a la red
2. dispositivo envia paquetes broadcast **DHCPDISCOVER** para encontrar el servidor DHCP
3. el servidor DHCP, al recibir la solicitud, reserva de su address pool una dirección asignada a la MAC del dispositivo solicitante y le envía una respuesta con un paquete unicast llamado **DHCPOFFER** donde indica un resumen del segmento de red.
4. este paquete lo recibe únicamente el dispositivo solicitante.
5. una vez el dispositivio reciba el DHCPOFFER, enviará un **DHCPREQUEST**, que simboliza el pedido oficial de obtención de su dirección IP y la conexión a la red
6. el servidor lo recibe, asigna la IP reservada anteriormente y envía un **DHCPACK** en el cual notifica la aceptación del servidor, junto con la lista completa de opciones de config más un tiempo de la duración de la reserva

#### Laboratorio teórico: ataques potenciales al DHCP

- DHCP STARVATION: inundar con peticiones DHCPREQUEST al servidor DHCP, con direcciones MAC falsas con el objetivo de agotar su espacio de direcciones asignables. El objetivo es que el servidor DHCP no sea capaz de responder a otros clientes
- DHCP SPOOFING: suplantar al servidor DHCP de una red y modificar los parámetros de red que reciben los equipos conectados al renovar o solicitar una nueva IP.
- DHCP ROGUE SERVER: servidor que se encuentra e nla red fuera del control del administrador y que se usa para hacer ataques de tipo MITM (man in the middle).
- DHCP ACK INJECTION ATTACK: mejora la utilización de un DHCP ROGUE SERVER para hacer DHCP SPOOFING ya que asegura que los equipos reciban la configuración del servidor atacante.
- DHCP EXHAUSTION ATTACK: similar o igual a dhcp starvation; llega un momento cuando el servidor dhcp no responde más (denial of services)

## Módulo 1 Unidad 4

### dispositivos de seguridad

objetivo de un firewall: bloquear acceso no autorizado. qué proteger, cómo proteger y dónde proteger

_siendo que el tráfico verde es interno (al servidor) y el rojo tiene salida al exterior, considero que es más importante proteger el tráfico orientado hacia el exterior. Ya que la red de la derecha tiene más dispositivos que usan la red roja/externa, pondría un firewall entre el router principal y el switch del conjunto derecho, como se indica en esta imagen:_

ACL: forma de determinar los permisos de acceso apropiados a un determinado objeto dependiendo de ciertos criterios del **proceso que hace el pedido**. según los ACL del proceso se le dará acceso o no. los criterios son: el origen del tráfico, el destino del tráfico, el protocolo usado. funciona a través de un firewall o router que analiza cada paquete, lo compara con la acl correspondiente línea por línea - toma la acción correspondiente: PERMIT o DENY (o drop?). el comportamiento predeterminado es deny all; si no encuentra una regla para el pedido, fue. 

CISCO: 2 tipos de ACL más conocidas, las extendidas y las estándar que se pueden configurar tanto en routers como en firewalls:

- listas de acceso estándar: filtran paquetes IP y solo consideran la dirección de origen: `Roter(config)#access-list 10 permit 192.168.2.10 0.0.0.0`. 192.168.2.10 es la dirección ip de origen y 0.0.0.0 es la máscara de wildcard
- listas de acceso extendidas: filtran paquetes ip y consideran tanto la dirección de origen como la de destino y los números de puerto del encabezado de la capa de transporte: `Router(config)#access-list 105 deny tcp host 192.168.2.5 any eq 21` 
  - 105: ACL IP extendida
  - deny: deniega el acceso
  - tcp: paquetes tcp
  - host 192.168.2.5: dirección IP de origen
  - any: dirección IP de destion
  - eq 21: puerto TCP de destino

- Escribir un ACL que permita el tráfico de la PC0 a la PC1: `access-list 101 permit ip host 10.20.20.50 0.0.0.0 host 10.10.10.51 0.0.0.0`
- y otro ACL que permita el tráfico de la PC0 al server: `access-list 101 permit ip host 10.20.20.50 0.0.0.0 host 10.10.10.50 0.0.0.0`
- Consigna: Logística y Ventas pueden verse entre sí, pero no pueden ver a Administración, sin embargo, Administración puede ver a todas
  - `access-list 101 permit ip 172.16.1.0 0.0.0.255 192.168.1.0 0.0.0.255` + `access-list 101 permit ip 192.168.1.0 0.0.0.255 172.16.1.0 0.0.0.255` 
  - `access-list 1 permit IP host 10.10.10.0 0.0.0.255` o `access-list 101 permit ip 10.10.10.0 192.168.1.0 0.0.0.255` + `access-list 101 permit ip 10.10.10.0 172.16.1.0 0.0.0.255`

1. Relevamiento: tenemos una red que consiste en un modem de acceso, que se conecta a un firewall (primera y única medida de seguridad de hardware) que después se conecta con un main switch. De este switch dependen _TODAS_ las conexiones con los dispositivos finales, desde impresores a WAP y distintos servidores. El main switch funciona también con enrutador. También observamos que existe (al menos) una conexión remota capaz de acceder a la red interna. 
2. Idealmente, hay que proteger todo. Prioritariamente, habría que seleccionar los servidores, especialmente el servidor de BackUp. También proteger las computadores de los trabajadores ya que también hay está almacenada información confidencial. Al mismo tiempo, para las conexiones remotas, establecer medidas de control para asegurarnos de 
3. Los dispositivos principales, que son los servidores NO están bien posicionados, ya que no existe un dispositivo intermedio entre ellos y el main switch. Si bien existe un firewall entre el modem y el main switch, sigue siendo un SPOF (single point of failure)
4. Agregar al menos un IPS después del firewall o detrás de otro switch entre el main switch y el grupo de servidores. También implementar un reglas al nivel del switch para permitir acceso de menor privilegio (least privilege access). Implementar un IDS en las subredes que se deberían crear, tanto en la subred de las estaciones de los usuarios finales como en la subred de los servidores.
5. Existe un solo servidor de backup. Si este falla, la red se quedaría sin respaldo. Se podría crear un servidor redundante de backup.
6. Cosas a mejorar podría ser implementar una VPN para el acceso remoto.

Dada la estructura en el ejercicio añadí un firewall después de cada router además de un IPS después de cada firewall. Agregué dos routers (Router3 y 4) para la comunicación lateral, entre los dispositivos (doble router para asegurar redundancia). En los dispositivos agregué H-IDS. En el switch principal agregué un N-IDS al igual que otro N-IDS en los routers usamos para la comunicación lateral. Veo un SPOF que es el Switch0 - agregaría un segundo switch con las conexiones a los routers, aun sabiendo que eso significaría switches más grandes.

## final01

router - equipo de última milla.

redundacia, replicación; 2 firewalls como backup. IPS es la bocha

switch de capa 3 capaz que segmenta
