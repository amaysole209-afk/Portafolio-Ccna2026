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
# Tabla A. Dispositivos intermedios (Routers y Switches)

| Dispositivo / Interfaz | VLAN | Segmento de red base | Dirección IP a calcular / configurar | Máscara de subred | Gateway por defecto |
|---|---:|---|---|---|---|
| R1-Core (G0/0/0.10) | 10 | 192.168.10.0/24 | 192.168.10.254 | 255.255.255.0 | No aplica |
| R1-Core (G0/0/0.20) | 20 | 192.168.20.0/24 | 192.168.20.254 | 255.255.255.0 | No aplica |
| R1-Core (G0/0/0.30) | 30 | 192.168.30.0/24 | 192.168.30.254 | 255.255.255.0 | No aplica |
| R1-Core (G0/0/0.99) | 99 | 192.168.99.0/24 | 192.168.99.254 | 255.255.255.0 | No aplica |
| SW-Core (SVI VLAN 99) | 99 | 192.168.99.0/24 | 192.168.99.1 | 255.255.255.0 | 192.168.99.254 |
| SW-Lab1 (SVI VLAN 99) | 99 | 192.168.99.0/24 | 192.168.99.2 | 255.255.255.0 | 192.168.99.254 |
| SW-Lab2 (SVI VLAN 99) | 99 | 192.168.99.0/24 | 192.168.99.3 | 255.255.255.0 | 192.168.99.254 |

# Tabla B. Dispositivos finales (Computadoras)

| Dispositivo final | Puerto del switch | VLAN | Dirección IP / CIDR | Gateway por defecto |
|---|---|---:|---|---|
| PC-Gestión-1 | SW-Core Fa0/9 | 99 | 192.168.99.10/24 | 192.168.99.254 |
| PC-Admin-Lab1-1 | SW-Lab1 Fa0/1 | 10 | 192.168.10.1/24 | 192.168.10.254 |
| PC-Admin-Lab1-2 | SW-Lab1 Fa0/2 | 10 | 192.168.10.2/24 | 192.168.10.254 |
| PC-Admin-Lab1-3 | SW-Lab1 Fa0/3 | 10 | 192.168.10.3/24 | 192.168.10.254 |
| PC-Alumnos-Lab1-1 | SW-Lab1 Fa0/4 | 20 | 192.168.20.1/24 | 192.168.20.254 |
| PC-Alumnos-Lab1-2 | SW-Lab1 Fa0/5 | 20 | 192.168.20.2/24 | 192.168.20.254 |
| PC-Alumnos-Lab1-3 | SW-Lab1 Fa0/6 | 20 | 192.168.20.3/24 | 192.168.20.254 |
| PC-Direccion-Lab1-1 | SW-Lab1 Fa0/7 | 30 | 192.168.30.1/24 | 192.168.30.254 |
| PC-Admin-Lab2-1 | SW-Lab2 Fa0/1 | 10 | 192.168.10.4/24 | 192.168.10.254 |
| PC-Admin-Lab2-2 | SW-Lab2 Fa0/2 | 10 | 192.168.10.5/24 | 192.168.10.254 |
| PC-Admin-Lab2-3 | SW-Lab2 Fa0/3 | 10 | 192.168.10.6/24 | 192.168.10.254 |
| PC-Alumnos-Lab2-1 | SW-Lab2 Fa0/4 | 20 | 192.168.20.4/24 | 192.168.20.254 |
| PC-Alumnos-Lab2-2 | SW-Lab2 Fa0/5 | 20 | 192.168.20.5/24 | 192.168.20.254 |
| PC-Alumnos-Lab2-3 | SW-Lab2 Fa0/6 | 20 | 192.168.20.6/24 | 192.168.20.254 |
| PC-Direccion-Lab2-1 | SW-Lab2 Fa0/7 | 30 | 192.168.30.2/24 | 192.168.30.254 |

# Datos adicionales

| VLAN | Nombre | Función |
|---:|---|---|
| 10 | Administración | Computadoras administrativas |
| 20 | Laboratorios | Computadoras de alumnos |
| 30 | Dirección | Computadoras de dirección |
| 99 | Gestión | Administración de switches |
| 111 | Nativa | VLAN nativa de enlaces troncales |
| 999 | Blackhole | Puertos no utilizados y apagados |

**Máscara de subred:** 255.255.255.0 (/24)

**Puertas de enlace:**
- VLAN 10: 192.168.10.254
- VLAN 20: 192.168.20.254
- VLAN 30: 192.168.30.254
- VLAN 99: 192.168.99.254
