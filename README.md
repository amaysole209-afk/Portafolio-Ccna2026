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

 3.-Asignar nombre a los dispositivos con las iniciales SARV
En este paso asigné nombres personalizados a los routers y switches, agregando mis iniciales SARV al final para identificar cada dispositivo.

Router-R1-Core-SARV

Router>enable
Router#configure terminal
Enter configuration commands, one per line.  End with CNTL/Z.
Router(config)#hostname R1-Core-SARV
R1-Core-SARVL(config)#end

Switch Central-SW-Core-SARV

Switch>enable
Switch#configure terminal
Enter configuration commands, one per line.  End with CNTL/Z.
Switch(config)#hostname SW-Core-SARV
SW-Core-SARV(config)#end

Switch 1-SW-Lab1-SARV

Switch>enable
Switch#configure terminal
Enter configuration commands, one per line.  End with CNTL/Z.
Switch(config)#hostname SW-Lab1-SARV
SW-Lab1-SARVL(config)end

Switch 2-SW-Lab2-SARV

Switch>enable
Switch#configure terminal
Enter configuration commands, one per line.  End with CNTL/Z.
Switch(config)#hostname SW-Lab2-SARV
SW-Lab2-SARVL(config)end

4.-Configuracion básica de sw y router de contraseña y mensaje
En este paso configuré las contraseñas de seguridad en los routers y switches utilizando `cisco123` para el acceso al modo privilegiado, la consola y las líneas VTY. También activé el cifrado de las contraseñas con el comando `cisco123` y configuré el mensaje MOTD **“ACCESO RESTRINGIDO”** como advertencia al ingresar.

Contraseña Privilegeado use:
enable
config
enable secret cisco123
service password-encryption
banner motd #ACCESO RESTRINGIDO

Para configurar una contraseña en la consola use:

line console 0
password cisco122
login
exit
Contraseña de acceso remoto use:

line vty 0 4
password cisco1232
login
exit

5.-Crear Vlans

configure terminal
vlan 10
 name Administracion
exit
vlan 20
 name Laboratorios
exit
vlan 30
 name Direccion
exit
vlan 99
 name Gestion
exit
vlan 111
 name Nativa
exit
vlan 999
 name Blackhole
exit
end

Con este comando verifique si se crearon y debe ver las VLAN 10, 20, 30, 99, 111 y 999 con sus respectivos nombres:

show vlan brief  o tambien sh vlan brief 

6.-Asignar los puertos a las VLANS.

°SW-Lab1-SARV

enable
configure terminal

interface range fa0/1-3
switchport mode access
switchport access vlan 10
exit

interface range fa0/4-6
switchport mode access
switchport access vlan 20
exit

interface range fa0/7
switchport mode access
switchport access vlan 30
exit

end

°SW-Lab2-SARV

enable
configure terminal

interface range fa0/1-3
switchport mode access
switchport access vlan 10
exit

interface range fa0/4-6
switchport mode access
switchport access vlan 20
exit

interface range fa0/7
switchport mode access
switchport access vlan 30
exit

end
SW-Core-SARV
En este caso, el switch central tiene una PC de gestión conectada al puerto Fa0/9, y ese puerto debe pertenecer a la VLAN 99 (Gestión).

enable
configure terminal
interface fastEthernet 0/9
switchport mode access
switchport access vlan 99
no shutdown
exit
end
FOTO DE PACKET TRACER

7.- Verificar la configuracion de la VLANs

En SW-Core-SARV: Se verificó la creación de las VLAN y la asignación de los puertos. Se comprobó que el puerto Fa0/9 pertenece a la VLAN 99, destinada a la PC de gestión.
imagen

En SW-Lab1-SARV: Se verificó la creación de las VLAN y la asignación de los puertos correspondientes.
Imagen

En SW-Core-SARV: : Se comprobó que las VLAN estén creadas y que los puertos estén asignados correctamente.
IMAGEN
8.- Habilitar los enlaces troncales.
SW-Core-SARV

enable
configure terminal

interface Gig0/1
switchport mode trunk
switchport trunk native vlan 111
switchport trunk allowed vlan 10,20,30,99,111
no shutdown
exit

interface Fa0/24
switchport mode trunk
switchport trunk native vlan 111
switchport trunk allowed vlan 10,20,30,99,111
no shutdown
exit

interface Fa0/23
switchport mode trunk
switchport trunk native vlan 111
switchport trunk allowed vlan 10,20,30,99,111
no shutdown
exit

end


SW-Lab1-SARV

enable
configure terminal
interface fa0/24
switchport mode trunk
switchport trunk native vlan 111
switchport trunk allowed vlan 10,20,30,99,111
no shutdown
exit
end


SW-Core-SARV

enable
configure terminal
interface fa0/23
switchport mode trunk
switchport trunk native vlan 111
switchport trunk allowed vlan 10,20,30,99,111
no shutdown
exit
end


9.- Verificar la configuración de los enlaces troncales
imagen de los 3 switches

10.-Guardar la configuración: escribe este código en la CLI de cada switch (SW-Lab1 y SW-Lab2): 

enable
copy running-config startup-config
Destination filename [startup-config]?
[OK]

11.-Configurar la subinterfaces en el router.

enable
configure terminal
interface gigabitEthernet0/0
no shutdown
exit
interface gigabitEthernet0/0.10
encapsulation dot1Q 10
ip address 192.168.10.1 255.255.255.0
exit
interface gigabitEthernet0/0.20
encapsulation dot1Q 20
ip address 192.168.20.1 255.255.255.0
exit
interface gigabitEthernet0/0.30
encapsulation dot1Q 30
ip address 192.168.30.1 255.255.255.0
exit
interface gigabitEthernet0/0.99
encapsulation dot1Q 99
ip address 192.168.99.1 255.255.255.0
exit
interface gigabitEthernet0/0.111
encapsulation dot1Q 111 native
ip address 192.168.111.1 255.255.255.0
exit
end

IMAGEN

12.-Asignar direccionamiento IP y encapsulamiento Dot1Q

enable
configure terminal
interface gigabitEthernet0/0
no shutdown
exit
interface gigabitEthernet0/0.10
encapsulation dot1Q 10
ip address 192.168.10.1 255.255.255.0
exit
interface gigabitEthernet0/0.20
encapsulation dot1Q 20
ip address 192.168.20.1 255.255.255.0
exit
interface gigabitEthernet0/0.30
encapsulation dot1Q 30
ip address 192.168.30.1 255.255.255.0
exit
interface gigabitEthernet0/0.99
encapsulation dot1Q 99
ip address 192.168.99.1 255.255.255.0
exit
interface gigabitEthernet0/0.111
encapsulation dot1Q 111 native
ip address 192.168.111.1 255.255.255.0
exit
end

IMAGEN

13.-Verificar conectividad con Ping

IMAGENES DE LOS PINGNS


14.-Diario de Aprendizaje y Troubleshooting

¿Cuál fue el mayor reto técnico que enfrentaste en esta unidad?
Fue configurar las subinterfaces del router con Dot1Q porque tenia q relacionar bien cada VLANS con direccion ip y lograr que todas las computadoras pudieran comunicarse (Hacer ping)

Bitácora de Errores
Error 1: Fue que al asignar nombres a los switches me equivoque de nombres
Soluccion1: Tuve que hacer de nuevo el codigo para asignar el nombre fue que investigue y al darme cuenta era el mismo codigo
Error 2: No sabia cual era la contraseña que puse a mi switch 1
Solución2: Busque las fotos q tome cuando puse la contraseña y fue que la encontre ,pero primero no me agarraba y fue que la puse mal 
















