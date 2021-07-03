# Módulo 1 - Unidad 2

1. Crear un informe explicando que son las bases de datos “WHOIS” y cuáles son las correspondientes a nuestra zona (continente) y país.

Las bases de datos WHOIS son un registro que identifica a quién pertenece un dominio y cómo contactarlo. La ICANN (Internet Corporation for Assigned Names and Numbers) regula el registro y a quién pertenecen los nombres de dominio. No es exclusivo de la ICANN, si no que los datos son almacenados por "registradores" que deben estar acreditados por la ICANN.

Los datos que almacenan estas bases datos incluyen: nombre, domicilio, correo electrónico, número de teléfono y contactos técnicos y administrativos. Estos datos son de acceso público a los datos sobre nombres registrados. WHOIS es también el protocolo que se usa para buscar en sus bases de datos e identificar al titular o "registrario" de un dominio.

En América Latina la principales bases de datos WHOIS son nic.ar (<https://nic.ar/es/whois>), lacnic (<https://www.lacnic.net/1002/1/lacnic/whois>) y ya un poco más al norte iar.mx (<https://www.iar.mx/jsf/static_content/services/current_services/resource_registry/whoisDatabase.jsf>) o más a nivel internacional godaddy (<https://ar.godaddy.com/whois>).

2. Buscar en Internet 4 direcciones IP y examinarlas - Transformar a las mismas en binario y subirlas al foro correspondiente

| URL | IP | BINARIO |
| --- | --- | ---- |
| www.cordoba.gob.ar | 76.223.3.255 | 01001100.11011111.00000011.1111111 |
| www.dxc.com | 151.101.3.10 | 10010111.01100101.00000011.00001010 |
| www.resolvit.com | 198.55.245.164 | 11000110.00110111.111110101.10100100 |
| mail.google.com | 216.58.222.37 | 11011000.00111010.11011110.00100101 |

1. Topología

![image001](./001.PNG)

El IPS controla todo el tráfico que pasa por el primer firewall. El  El segundo firewall controla la red interna, pero antes de llegar está ubicado el IDS. Es una topología de árbol, en general.
