Vídeos de repàs:  
IP-1: https://youtu.be/lw8tITa5Cd8 (Adreçament IP)  
IP-2: https://youtu.be/lgHit1Io54Y (Subxarxes IP)  
IP-3: https://youtu.be/TiLpbNlYz3o (Talues d'encaminament)  
IP-4: https://youtu.be/a8osS-fVkqI (Protocol ARP)  
IP-5: https://youtu.be/wWd2skddCuY (Capçalera IP)  
IP-6: https://youtu.be/fnlAeTgdxBM (Protocol ICMP)  
IP-7: https://youtu.be/FPl72YMMf1w (DNS)  
IP-8: https://youtu.be/5JbE1eWcg7c (DHCP)  
IP-9: https://youtu.be/-nXRVIb1u5s (NAT)  

- [IP](#ip)
  - [Classes:](#classes)
  - [Adreces especials:](#adreces-especials)
  - [Adreces privades:](#adreces-privades)
  - [Subnetting](#subnetting)
  - [Classless Inter-Domain Routing (CIDR)](#classless-inter-domain-routing-cidr)
  - [Taules d'encaminament](#taules-dencaminament)
  - [Protocol ARP (Address Resolution Protocol)](#protocol-arp-address-resolution-protocol)
  - [Capçalera IP](#capçalera-ip)
  - [Fragmentació IP](#fragmentació-ip)
  - [Protocol ICMP](#protocol-icmp)
    - [Format](#format)
    - [Missatges comuns](#missatges-comuns)
    - [MTU Path Discovery](#mtu-path-discovery)
  - [Protocol DNS](#protocol-dns)
  - [Protocol DHCP](#protocol-dhcp)
    - [Missatges DHCP](#missatges-dhcp)
      - [Fields](#fields)
    - [Com funciona](#com-funciona)
  - [Mecanisme NAT (Network Address Translation)](#mecanisme-nat-network-address-translation)
    - [DNAT (Destination NAT)](#dnat-destination-nat)
  - [Algorismes d'enrutament](#algorismes-denrutament)
    - [Routing Information Protocol (RIP)](#routing-information-protocol-rip)
      - [Solució al *Count to Infinity*](#solució-al-count-to-infinity)

# IP

- 32 bits
- > 147.83.24.28
- **netid**: Identifica xarxa
- **hostid**: Identifica host a la xarxa
- Cada IP identifica una interficie

## Classes:
| classe | netid | hostid |             rang              |
| :----: | :---: | :----: | :---------------------------: |
|   A    |   1   |   3    | `  0.0.0.0 ~ 127.255.255.255` |
|   B    |   2   |   2    | `128.0.0.0 ~ 191.255.255.255` |
|   C    |   3   |   1    | `192.0.0.0 ~ 223.255.255.255` |
|   D    |   -   |   -    | `224.0.0.0 ~ 239.255.255.255` |
|   E    |   -   |   -    | `240.0.0.0 ~ 255.255.255.255` |

## Adreces especials:
| netid | hostid | significat                                            | exemple            |
| :---: | :----: | :---------------------------------------------------- | :----------------- |
|  xxx  | tot 0  | Identifica una xarxa (Routing tables)                 | `192.168. 35.  0`  |
|  xxx  | tot 1  | Broadcast a la xarxa                                  | `192.168. 35.255`  |
| tot 0 | tot 0  | Identifica un host (DHCP)                             | `  0.  0.  0.  0`  |
| tot 1 | tot 1  | Broadcast a la xarxa, adreça destí en DHCP            | `255.255.255.255`  |
|  127  |  xxx   | host loopback: comunicació entre processos amb TCP/IP | `127.xxx.xxx.xxx`  |

## Adreces privades:
Aquestes adreces s'ignoren si s'esperava una adreça global.

| classe |             rang              | num |
| :----: | :---------------------------: | :-: |
|   A    | ` 10.  0.0.0 ~  10.  0.  0.0` |  1  |
|   B    | `172. 16.0.0 ~ 172. 31.  0.0` | 16  |
|   C    | `192.168.0.0 ~ 192.168.255.0` | 256 |

> FI VIDEO 1

## Subnetting
Xarxes més petites dins d'una altra (Subxarxes).  
Utilitza part dels bits del hostid.

>  **210.50.30.0/26**  
   El `/26` és la màscara que s'aplica, que significa el número d'uns de la màscara.  
   Seria equivalent a `255.255.255.255.192`.

Si fem una AND llògica ens quedem amb el prefix de xarxa (la IP de la xarxa original).

- **Variable Length Subnet Mask (VLSM)**: Subxarxes amb diferents mides.  

- Per cada subxarxa perdem 3 adreces, l'adreça de xarxa, l'adreça de broadcast i l'adreça del router.
  - Al final es tradueix en restar 2 al número d'adreces disponibles del rang.

## Classless Inter-Domain Routing (CIDR)
S'utilitzen màscares en comptes de classes, s'agreguen les IPs.
A => `/8`  => 255.  0.  0.0
B => `/16` => 255.255.  0.0
C => `/24` => 255.255.255.0

> Dues subxarxes estrictament consecutives es poden agregar en un `/x - 1`.  
> `200.1.10.0/24 i 200.1.11.0/24 => 200.1.10.0/23`

> FI VIDEO 2

## Taules d'encaminament
Taula on tenim el prefix de xarxa de destinació i cap a on s'ha d'enviar cada datagrama.

- Accés
  - Directe: Connectat directament
  - Indirecte: Connectat a través d'un router

- Ruta per defecte: On s'envien tots els datagrames amb adreça de destinació no present a la taula.
  - Normalment és `0.0.0.0/0`.

| Paràmetres  |                         |
| ----------- | ----------------------- |
| Destination | Xarxa on volem arribar  |
| Genmask     | Màscara de la xarxa     |
| Gateway     | Per on hi volem arribar |

> FI VIDEO 3

## Protocol ARP (Address Resolution Protocol)
Protocol que tradueix direccions IP a adreces físiques (MAC).  
L'associació d'IP a MAC no és fixa, les adreces que s'assignen a cada MAC poden canviar.

- Les adreces MAC tenen 48 bits.

El protocol detecta adreces duplicades i actualitza les MAC de les taules ARP si hi ha un canvi d'IP.

> FI VIDEO 4

## Capçalera IP
- 20 bytes en total

| Nom                 | Bits | Descripcio                                                   |
| ------------------- | ---- | ------------------------------------------------------------ |
| Version             | 4    | Versió del protocol                                          |
| IHL                 | 4    | Longitud de la capçalera (blocs de 4 octets / 32 bits)       |
| Type of Service     | 8    | Tipus de servei `xxxdtrc0`                                   |
| Total Length        | 16   | Mida del datagrama en bytes                                  |
| Identification      | 16   | Fragmentació: Identifica els fragments d'un datagrama        |
| Flags               | 3    | Fragmentació: Indica **D**on't fragment i **M**ore fragments |
| Fragment Offset     | 13   | Fragmentació: Offset del missatge en el datagrama original   |
| Time to Live (TTL)  | 8    | Número de routers que pot passar el missatge                 |
| Protocol            | 8    | Protocol encapsulat. TCP, UDP, etc...                        |
| Header Checksum     | 16   | Or exclusiva de tots els camps (detecta 50% dels errors)     |
| Source Address      | 32   | Adreça d'origen                                              |
| Destination Address | 32   | Adreça de destí                                              |
| Options             | 24   | Record Route, Loose Source Routing, Strict Source Routing    |
| Padding             | xxx  | Padding que calgui per arribar a 32 bits                     |

## Fragmentació IP
Separar missatges en datagrames menors.

La mida total sempre serà `20 bytes header + mida datagrama`.

- La podem necessitar:
   - Router:
     Quan dues xarxes amb Maximum Transfer Unit (MTU) diferents es connecten.
   - Host:
     Quan utilitzem UDP. Els segments TCP són <= MTU.

Els datagrames es reconstrueixen a la destinació.

- Necessitem saber:
  - Identification (16 bits)
  - Flags (3 bits)
    - **D**on't fragment: MTU path discovery.
    - **M**ore fragments: El missatge ha acabat de transmetre's.
  - Offset (13 bits): Posició del fragment en el datagrama original, de 8 en 8 bytes.
    - `mida fragment - 20 / 8` 8-byte-words (octets)

> FI VIDEO 5

## Protocol ICMP
Protocol associat al protocol IP.  
S'utilitza per diagnostic i missatges d'error, pot ser generat per IP, TCP/UDP i aplicacions.

S'encapsula en un datagrama IP (`protocol = 1`).

Un missatge ICMP no en pot generar un altre, per evitar bucles.

- Missatges:
   - Query
     - Porten un identificador (Type i Code) que indica si és request o reply.
   - Error

### Format
| Nom       | Bits | Descripció                          |
| --------- | ---- | ----------------------------------- |
| Type      | 8    | Tipus de missatge                   |
| Code      | 8    | Codi de l'error                     |
| Checksum  | 16   | Or llògica del missatge ICMP        |
| Contingut | 32   | Contingut de l'error, pot no ser-hi |

A més, els missatges d'error porten l'Internet Header + 64 bits del missatge original.

### Missatges comuns

| Type | Code | query/error | Nom                             | Descripció                                                    |
| ---- | ---- | ----------- | ------------------------------- | ------------------------------------------------------------- |
| 0    | 0    | query       | echo reply                      | Respon un `echo request`                                      |
| 3    | 0    | error       | network unreachable             | La xarxa no està a la Routing Table                           |
|      | 1    | error       | host unreachable                | L'ARP no pot resoldre l'adreça                                |
|      | 2    | error       | protocol unreachable            | IP no pot entregar el datagrama                               |
|      | 3    | error       | port unreachable                | TCP/UDP no pot entregar el datagrama (no existeix el port)    |
|      | 4    | error       | fragmentation needed but DF set | MTU path discovery                                            |
| 4    | 0    | error       | source quench                   | El router està congestionat                                   |
| 5    | 0    | error       | redirect for network            | Paquet reencaminat                                            |
| 8    | 0    | query       | echo request                    | Petició per resposta (ping)                                   |
| 11   | 0    | error       | TTL=0 during transit            | Enviat pel router quan el TTL d'un missatge és 0 (traceroute) |

### MTU Path Discovery
Redueix la fragmentació de la xarxa adaptant la mida MTU dels paquets.

Es posa **D**on't **F**ragment a 1 i es va actualitzant la mida dels datagrames que s'envien basat en la resposta.  
Es basa en l'error 3-4 (`fragmentation needed but DF set`).

La mida MTU final sempre serà la més petita que s'hagi trobat.

> FI VIDEO 6

## Protocol DNS
Tradueix noms a adreces IP.

> `rogent.ac.upc.edu` => `147.83.31.7`

- Per missatges curts utilitza UDP, per llargs TCP
- Well-known port: 53
 
> ```bash
> # Pregunta
> 147.83.34.125.1333 > 147.83.32.3.53: 53040+ A? www.foo.org
> # Resposta
> 147.83.32.3.53 > 147.83.34.125.1333: 53040 1/2/2 www.foo.org A 198.133.219.10
> ```
> ```bash
> # Pregunta
> [PC] > [SERVIDOR].53: [IDENTIFICADOR]+ A? [PAGINA]
> # Resposta
> [SERVIDOR].53 > [PC]: [IDENTIFICADOR] 1/2/2 [PAGINA] A [DIRECCIO IP PAGINA]
> ```

> FI VIDEO 7

## Protocol DHCP
Configura dinàmicament un host en una xarxa (necessites un servidor DHCP).

- La configuració pot ser:
  - **Dinàmica**: El host està configurat durant un temps específic (leasing time)
  - **Automàtica**: Leasing time ilimitat
  - **Manual IP**: Les adreces IP s'assignen a MAC específiques

### Missatges DHCP

| Nom          | Descripció                                                                          |
| ------------ | ----------------------------------------------------------------------------------- |
| DHCPDISCOVER | El client fa un broadcast per trobar un servidor DHCP                               |
| DHCPOFFER    | El servidor respon el DHCPDISCOVER amb una IP                                       |
| DHCPREQUEST  | El client fa (a, b o c):                                                            |
|              | (a) Accepta els paràmetres del servidor                                             |
|              | (b) Confirma que l'adreça que té actualment és correcta (ex. després d'un reboot)   |
|              | (c) Exté el leasing time                                                            |
| DHCPACK      | El servidor envia paràmetres de configuració                                        |
| DHCPNAK      | El servidor indica que l'adreça del client és incorrecta (ex. leasing time expired) |
| DHCPDECLINE  | El client indica que l'adreça que el servidor li dona ja està en ús                 |
| DHCPRELEASE  | El client demana que se'l tregui de la xarxa                                        |
| DHCPINFORM   | El client demana només els paràmetres de configuració local                         |

#### Fields

| Field   | Octets   | Descripció                                             |
| ------- | -------- | ------------------------------------------------------ |
| op      | 1        | Tipus del missatge. `1 = BOOTREQUEST`, `2 = BOOTREPLY` |
| xid     | 4        | Id utilitzat per la comunicació client-servidor        |
| ciaddr  | 4        |                                                        |
| yiaddr  | 4        | La IP del client, setejada amb DHCPOFFER               |
| chaddr  | 16       | MAC del client                                         |
| options | variable | Paràmetres opcionals                                   |

### Com funciona
- Missatge UDP
  - Port servidor: 67
  - Port client: 68

1. El client fa un DHCPDISCOVER (broadcast)
2. El servidor respon amb un DHCPOFFER (broadcast)
3. El client accepta amb un DHCPREQUEST (broadcast)
4. I finalment el servidor envia la IP amb DHCPACK (broadcast)
5. Aqui el client ja té la IP configurada
  
- Abans que la configuració finalitzi, el client envia un DHCPREQUEST demanant que se li extengui la configuració
- El servidor respon amb un DHCPACK (broadcast)

## Mecanisme NAT (Network Address Translation)
Permet accedir des d'una adreça privada (internal) a una adreça publica (internet, external).  
El NAT es fa des del router.  

Modifica la capçalera IP de cada datagrama.

Es representa amb una taula d'encaminament:
- Inside: Adreces privades
- Outside: Adreça pública del router
- Foreign: Adreça pública d'internet
- Port NAT: Port virtual del router que permet saber on enviar els paquets rebuts d'internet

| Inside Address/port       | Outside Address/port      | Foreign/remote             |
| ------------------------- | ------------------------- | -------------------------- |
| C1/P1 (Computer 1/Port 1) | R/PNAT (Router, Port NAT) | I1/80 (Internet 1/Port 80) |

### DNAT (Destination NAT)
Permet connexions externes a servidors interns (adreces privades).

Cal fer una entrada manual al NAT indicant que tot el que rebi a l'adreça pública ho redirigeixi a l'adreça privada (alias).

## Algorismes d'enrutament
Afegeixen entrades a les taules d'enrutament.

### Routing Information Protocol (RIP)
Mesura la distàcnia per a arribar a la destinació en salts (*hops*).  
És 1 si està directament connectat, i >= 2 si no.

S'utilitza el port 520 pel broadcast.

El router envia un missatge RIP cada 30 segons als veïns.  
Si un veí no envia cap missatge en 180 segons, es considera caigut (*down).

El número màxim de salts és 16, que es considera infinit.

#### Solució al *Count to Infinity*
Si hi ha algun bucle en la xarxa, el RIP podria anar augmentant els hops fins a l'infinit.

Per a evitar-ho s'utilitza la tècnica de *Split horizon*, que elimina de les taules d'enrutament totes les entrades que ja estiguin contingudes en els gateway dels routers de la xarxa.

