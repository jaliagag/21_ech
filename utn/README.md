# Experto Universitario en Hacking Ético

```md
El mail mio para la presentación de ejercicios es : banchiero.UTN@gmail.com
```

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

- direccionamiento: una etiqueta que nos encontramos en el dispositivo de la red. **dentro de una red necesitamos identificar a todos los dispositivos** para la comunicación en la red. el direccionamiento privado es para la red LAN y el público para todo lo que sea WAN. todo direccionamiento no expuesto es considerado direccionamiento público.
- enrutamiento: aprender la manera de encontrar un equipo  o una determinada IP dentro de esa red. en la tabla de enrutamiento, se encuentran todas laredes publicadas y/o aprendidas

una dirección ip asignada a un equipo es única.

la **máscara de red** es una combinación de bits que sirve para delimitar el ámbito de una red de computadoras. 192.168.0.0/16 - el número que aparece después de la "/" es la suma de los bits que se utilizan para la máscara de red. esa identificación se la conoce como CIDR. la función de la máscara de red es indicar a los dispositivos qué parte de la dirección IP es el número de la red, incluyendo la subred, y qué parte es la que corresponde al host.

la puerta de enlace o **gateway** es un dispositivo que permite interconectar redes con protocolos y arquitecturas diferentes a todos los niveles de comunicación. su función es traducir la información del protocolo utilizado en una red al protocolo usado en la red de destino. la default gateway indica al tráfico de red por dónde tiene que salir

Crear un informe explicando que son las bases de datos “WHOIS” y cuáles son las correspondientes a nuestra zona (continente) y país.

bases de datos WHOIS: registro que identifica a quién pertenece un dominio y cómo contactarlo. la ICANN (Internet Corporation for Assigned Names and Numbers) regula el registro y a quién pertenecen los nombres de dominio. no es exclusivo de la ICANN, si no que los datos son almacenados por "registradores" que deben estar acreditados por la ICANN.

los datos que almacenan estas bases datos incluyen: nombre, domicilio, correo electrónico, número de teléfono y contactos técnicos y administrativos. estos datos son de acceso público a los datos sobre nombres registrados. WHOIS es también el protocolo que se usa para buscar en sus bases de datos e identificar al titular o "registrario" de un dominio.
