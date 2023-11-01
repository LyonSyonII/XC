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

Vídeos de repàs:
IP-1: https://youtu.be/lw8tITa5Cd8    (Adreçament IP)
IP-2: https://youtu.be/lgHit1Io54Y     (Subxarxes IP)
IP-3: https://youtu.be/TiLpbNlYz3o   (Talues d'encaminament)
IP-4: https://youtu.be/a8osS-fVkqI    (Protocol ARP)
IP-5: https://youtu.be/wWd2skddCuY (Capçalera IP)
IP-6: https://youtu.be/fnlAeTgdxBM    (Protocol ICMP) 
IP-7: https://youtu.be/FPl72YMMf1w  (DNS)
IP-8: https://youtu.be/5JbE1eWcg7c   (DHCP)
IP-9: https://youtu.be/-nXRVIb1u5s    (NAT) 

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