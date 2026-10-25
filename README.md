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

Tabla1.Direccionamiento IP del router R1-Core

| Dispositivo | Interfaz   | VLAN | Dirección IP    | Máscara de subred | Función                 |
|-------------|------------|-----:|-----------------|-------------------|-------------------------|
| R1-Core     | G0/0/0.10  | 10   | 192.168.10.254  | 255.255.255.0     | Gateway Administración  |
| R1-Core     | G0/0/0.20  | 20   | 192.168.20.254  | 255.255.255.0     | Gateway Laboratorios    |
| R1-Core     | G0/0/0.30  | 30   | 192.168.30.254  | 255.255.255.0     | Gateway Dirección       |
| R1-Core     | G0/0/0.99  | 99   | 192.168.99.254  | 255.255.255.0     | Gateway Gestión         |

Tabla2.Direccionamiento IP de los switches

| Dispositivo | Interfaz SVI | VLAN | Dirección IP  | Máscara de subred | Gateway        |
|-------------|--------------|-----:|---------------|-------------------|----------------|
| SW-Core     | VLAN 99      | 99   | 192.168.99.1  | 255.255.255.0     | 192.168.99.254 |
| SW-Lab1     | VLAN 99      | 99   | 192.168.99.2  | 255.255.255.0     | 192.168.99.254 |
| SW-Lab2     | VLAN 99      | 99   | 192.168.99.3  | 255.255.255.0     | 192.168.99.254 |


Tabla3.Segmentos de red y VLAN

| VLAN | Nombre         | Dirección de red          | Máscara       | Uso                              |
|------|----------------|---------------------------|---------------|----------------------------------|
| 10   | Administración | 192.168.10.0/24            | 255.255.255.0 | Computadoras de administración   |
| 20   | Laboratorios   | 192.168.20.0/24            | 255.255.255.0 | Computadoras de alumnos          |
| 30   | Dirección      | 192.168.30.0/24            | 255.255.255.0 | Computadoras de dirección        |
| 99   | Gestión        | 192.168.99.0/24            | 255.255.255.0 | Administración de switches       |
| 111  | Nativa         | Sin dirección IP asignada  | N/A           | VLAN nativa de enlaces troncales |
| 999  | Blackhole      | Sin dirección IP asignada  | N/A           | Puertos no utilizados y apagados |





