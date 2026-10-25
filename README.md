# Portafolio-Ccna2026
Crear el diagrama y cablear acorde a la topología
1. Diagrama de la topología
   
```text
                 [ R1-Core-SARV (SARV) ]
                           |
                           | G0/0
                           | Trunk 802.1Q
                           | Router-on-a-Stick
                           | VLANs 10, 20, 30, 99
                           | VLAN 111 nativa
                           |
                    [ SW-Core-SARV ]
                       /          \
                      /            \
              (Trunk)                (Trunk)
           VLAN 111 nativa        VLAN 111 nativa
                  /                    \
                 /                      \
       [ SW-Lab1-SARV ]          [ SW-Lab2-SARV ]
          Edificio A                 Edificio B


Dispositivos en SW-Lab1-SARV:       Dispositivos en SW-Lab2-SARV:

  ├── VLAN 10: 3 PCs Admin            ├── VLAN 10: 3 PCs Admin
  │   Fa0/1 - Fa0/3                   │   Fa0/1 - Fa0/3
  │                                   │
  ├── VLAN 20: 3 PCs Alumnos          ├── VLAN 20: 3 PCs Alumnos
  │   Fa0/4 - Fa0/6                   │   Fa0/4 - Fa0/6
  │                                   │
  └── VLAN 30: 1 PC Dirección         └── VLAN 30: 1 PC Dirección
      Fa0/7                               Fa0/7
  └── VLAN 99: 1 PC Gestión
      Puerto Fa0/9

![image alt][https://github.com/amaysole209-afk/Portafolio-Ccna2026/blob/c23315a6ce7fdc8a40318484e67c5aaef65c0e76/Topologias.png]
