# Portafolio-Ccna2026
1.-Crear el diagrama y cablear acorde a la topología
Diagrama de la topología
   
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
Imagen de la topología con cables

2.-Crear la tabla de direccionamiento.
| VLAN | Nombre | Dirección de red | Máscara de subred | Prefijo | Uso |
|---:|---|---|---|---|---|
| 10 | Administración | 192.168.10.0 | 255.255.255.0 | /24 | Equipos de Administración |
| 20 | Laboratorios | 192.168.20.0 | 255.255.255.0 | /24 | Equipos de Laboratorios |
| 30 | Dirección | 192.168.30.0 | 255.255.255.0 | /24 | Equipos de Dirección |
| 99 | Gestión | 192.168.99.0 | 255.255.255.0 | /24 | Administración de switches mediante SVI |
| 111 | Nativa | No aplica | No aplica | No aplica | VLAN nativa de los enlaces troncales |
| 999 | Blackhole | No aplica | No aplica | No aplica | VLAN para puertos no utilizados y apagados |
