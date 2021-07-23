# Módulo 2 - Unidad 2

## A- ¿Si tuviéramos a nuestra disposición un servidor DNS, cuales piensan que serían los puntos a tener en cuenta en su creación respecto a la seguridad?

Cuando se crea un servidor DNS se deben tener en cuenta varios aspectos relacionados con la seguridad:

- Tener un ambiente DNS de alta disponibilidad, para que en caso de que perdamos un servidor DNS, podamos seguir dando servicio. Para prevenir un ataque DDoS, debemos agregar reglas de firewall (o un firewall físico directamente) para bloquear IPs identificadas como maliciosas.
- Agregar herramientas de monitoreo de integridad de los datos, para evitar servir información falsa o implantada por un atacante.
- Asegurar que se le da a los usuarios ACLs del mínimo privilegio posible, es decir, que si un usuario lograra ingresar al servidor DNS, que no pueda realizar modificaciones porque solo el usuario Admin (por ejemplo) puede escribir en la base de datos.

## B- ¿En nuestro entorno de trabajo, en caso de disponer un servidor de DNS o DHCP, que sabemos de ellos?

El servidor DNS es el que permite que ingresemos a lugares que solo estarán disponibles en la intranet. También se pueden acceder a ellos a través de una VPN para conexiones remotas. Solo las personas que puedan llegar al servidor DNS tendrán acceso a las IP que almacena el servidor.

El servidor DHCP nos proveerá direcciones IP de manera dinámica que estén dentro de su rango.

## C- De los distintos balanceadores de carga que vimos, ¿cuál sería el más conveniente para nuestra empresa y porque? (o sea justificar la respuesta.

Me imagino un escenario donde muchos administradores usan una misma interfaz web para iniciar sesión en distintos servidores (uso de Citrix, por ejemplo). En este caso, considero que la mejor forma de balanceo de carga es a través del uso de un **Nodo de balanceo**, ya que de esta manera todos los administradores tienen que usar una sola IP (que puede estar relacionada con un nombre de dominio en un servidor DNS) para iniciar sesión y estar dentro de la red. Sin importar en qué servidor específico estan logeados, después pueden saltar a otros servidores finales que tienen que administrar.

