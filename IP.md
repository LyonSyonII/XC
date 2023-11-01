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
| tot 0 | tot 0  | Identifica un host (DHCP)                             | ` 0.   0.  0.  0 ` |
| tot 1 | tot 1  | Broadcast a la xarxa, adreça destí en DHCP            | `255.255.255.255` |
|  127  |  xxx   | host loopback: comunicació entre processos amb TCP/IP | `127.xxx.xxx.xxx` |

## Adreces privades:
Aquestes adreces s'ignoren si s'esperava una adreça global.

| classe |             rang              | num |
| :----: | :---------------------------: | :-: |
|   A    | ` 10.  0.0.0 ~  10.  0.  0.0` |  1  |
|   B    | `172. 16.0.0 ~ 172. 31.  0.0` | 16  |
|   C    | `192.168.0.0 ~ 192.168.255.0` | 256 |

## Subnetting
Xarxes més petites dins d'una altra (Subxarxes).  
Utilitza part dels bits del hostid.

>  **210.50.30.0/26**  
   El `/26` és la màscara que s'aplica, que significa el número d'uns de la màscara.  
   Seria equivalent a `255.255.255.255.192`.
