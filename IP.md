# IP

- 32 bits
- > 147.83.24.28
- **netid**: Identifica xarxa
- **hostid**: Identifica host a la xarxa
- Cada IP identifica una interficie

## Classes:
| classe | netid | hostid |            rang             |
| :----: | :---: | :----: | :-------------------------: |
|   A    |   1   |   3    | ` 0.0.0.0 ~ 127.255.255.255`  |
|   B    |   2   |   2    | `128.0.0.0 ~ 191.255.255.255` |
|   C    |   3   |   1    | `192.0.0.0 ~ 223.255.255.255` |
|   D    |   -   |   -    | `224.0.0.0 ~ 239.255.255.255` |
|   E    |   -   |   -    | `240.0.0.0 ~ 255.255.255.255` |

## Adreces especials:
| netid | hostid | significat                                            | exemple           |
| :---: | :----: | :---------------------------------------------------- | :---------------- |
|  xxx  | tot 0  | Identifica una xarxa (Routing tables)                 | `192.168. 35.  0` |
|  xxx  | tot 1  | Broadcast a la xarxa                                  | `192.168. 35.255` |
| tot 0 | tot 0  | Identifica un host (DHCP)                             | ` 0.   0.  0.  0 `|
| tot 1 | tot 1  | Broadcast a la xarxa, adreça destí en DHCP            | `255.255.255.255` |
|  127  |  xxx   | host loopback: comunicació entre processos amb TCP/IP | `127.xxx.xxx.xxx` |

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
A => `/8`
B => `/16`
C => `/24`

> Dues subxarxes estrictament consecutives es poden agregar en un `/x - 1`.  
> `200.1.10.0/24 i 200.1.11.0/24 => 200.1.10.0/23`

> FI VIDEO 2