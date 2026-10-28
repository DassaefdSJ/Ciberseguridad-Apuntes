# Guía de comandos: Examen T2-3 Conmutación de Redes LAN (Tipo B)

Grupo 7F21 · Red base 172.16.0.0/16 · Cisco Packet Tracer

**Equipo a usar:** 1 router (modelo 1941, tiene `gi0/0`), 4 switches 2960-24TT (1 servidor VTP + 3 clientes; cada uno trae `Gi0/1` y `Gi0/2`), 1 Server (DHCP/TFTP) y PC.

---

## 0. Qué pide el examen y dónde está en esta guía

|Reactivo|Pts|Qué pide|Sección|
|---|---|---|---|
|1|9|VTP cliente-servidor, VLSM sobre 172.16.0.0/16, tabla (red, máscara, 1.ª asignable)|1|
|2|10|VLAN en el switch servidor, puertos Fa0/1-8, Fa0/10-15, Fa0/18-22, port-security en Fa0/1, 8, 18, 22 y **DHCP para cada VLAN en el servidor**|3 y 6|
|3|5|Mínimo 3 switches cliente, 2 VLAN en cada uno, 2 hosts por VLAN, mínimo 2 puertos por VLAN, port-security en Fa0/5, 10, 15 de cada cliente|4|
|4|5|SSH en VLAN 1 en todos los switches, usuarios del equipo + `mcruz` / `1231735A`, respaldos a servidor TFTP (cliente y servidor)|7 y 8|
|5|6|Pruebas de conectividad en PDF, nombre `Grupo_Actividad_Nombre completo del representante`|9|
|6|5|Router para conectividad en toda la red|5|

---

## 1. Reactivo 1: diseño VTP y tabla VLSM

**VTP:** SW-SERVER en modo _server_; SW-C1, SW-C2 y SW-C3 en modo _client_. Dominio: `ITESA`.

**Tabla de enrutamiento (la que se entrega, 3 filas):**

|Grupo|VLAN|No. hosts|Dirección de red|Máscara|1.ª asignable|
|---|---|---|---|---|---|
|Estudiantes|10|5500|172.16.0.0 /19|255.255.224.0|172.16.0.1|
|Docentes|20|2100|172.16.32.0 /20|255.255.240.0|172.16.32.1|
|Administrativos|30|900|172.16.48.0 /22|255.255.252.0|172.16.48.1|

**Cómo se calcula (por si te lo piden en el examen):**

- 5500 hosts → 2^13 = 8192 ≥ 5502 → 13 bits de host → /19.
- 2100 hosts → 2^12 = 4096 ≥ 2102 → 12 bits de host → /20.
- 900 hosts → 2^10 = 1024 ≥ 902 → 10 bits de host → /22.
- Se asigna de mayor a menor y cada bloque empieza donde termina el anterior: 172.16.0.0–31.255, luego 32.0–47.255, luego 48.0–51.255.

**Rangos completos (para tus apuntes):**

|Red|Última asignable|Broadcast|
|---|---|---|
|172.16.0.0/19|172.16.31.254|172.16.31.255|
|172.16.32.0/20|172.16.47.254|172.16.47.255|
|172.16.48.0/22|172.16.51.254|172.16.51.255|

**Red extra de administración (VLAN 1), fuera de la tabla del examen:** el reactivo 4 pide IP en la VLAN 1 para SSH, y esa VLAN no está en la tabla. Se usa el bloque siguiente, contiguo al último: **172.16.52.0/24** (255.255.255.0), gateway 172.16.52.1. Si tu maestro prefiere otra dirección, solo cambia ese bloque.

|Dispositivo|IP VLAN 1|
|---|---|
|Router (subinterfaz nativa)|172.16.52.1|
|SW-SERVER|172.16.52.2|
|SW-C1|172.16.52.3|
|SW-C2|172.16.52.4|
|SW-C3|172.16.52.5|

**Servidor DHCP/TFTP:** IP fija `172.16.0.6`, máscara `255.255.224.0`, gateway `172.16.0.1`.

---

## 2. Cableado

|Cable|Puerto A|Puerto B|
|---|---|---|
|Router ↔ servidor|Router gi0/0|SW-SERVER gi0/2|
|Servidor ↔ cliente 1|SW-SERVER gi0/1|SW-C1 gi0/1|
|Cliente 1 ↔ cliente 2|SW-C1 gi0/2|SW-C2 gi0/1|
|Cliente 2 ↔ cliente 3|SW-C2 gi0/2|SW-C3 gi0/1|
|Server DHCP/TFTP|Server|SW-SERVER fa0/2|

Los 2960 solo traen dos puertos Gigabit, por eso van en cadena. VTP llega hasta SW-C3 porque los clientes reenvían los anuncios por los troncales.

---

## 3. Reactivo 2: SW-SERVER

### 3.1 VTP, VLAN y troncales

```
enable
configure terminal
hostname SW-SERVER
vtp domain ITESA
vtp mode server
vlan 10
 name CLIENTES
vlan 20
 name EMPLEADOS
vlan 30
 name VENTAS
exit
vlan 40 
name PROVEEDORES
interface range gi0/1-2
 switchport mode trunk
end
```

|Comando|Para qué sirve|
|---|---|
|`vtp domain ITESA`|Nombre del dominio. Debe ser idéntico en los 4 switches (distingue mayúsculas).|
|`vtp mode server`|Este switch crea las VLAN y las reparte a los clientes.|
|`vlan 10` + `name`|Crea la VLAN. VTP reparte solo esto, **no** asigna puertos.|
|`switchport mode trunk`|El cable lleva todas las VLAN. Sin troncal no funciona VTP. En 2960 de Packet Tracer **no existe** `switchport trunk encapsulation`.|

### 3.2 Asignar puertos (según el examen)

```
configure terminal
interface range fa0/2-8
 switchport mode access
 switchport access vlan 10
interface range fa0/10-14
 switchport mode access
 switchport access vlan 20
interface range fa0/15-19
 switchport mode access
 switchport access vlan 30
 interface range fa0/20-23
 switchport mode access
 switchport access vlan 40
end
```

`switchport mode access` convierte el puerto en uno de una sola VLAN para una PC. Debe ir antes de port-security.

### 3.3 Protección por MAC (Fa0/1, Fa0/8, Fa0/18, Fa0/22)

```
configure terminal
interface range fa0/1, fa0/8, fa0/18, fa0/22
 switchport port-security
 switchport port-security maximum 1
 switchport port-security mac-address sticky
 switchport port-security violation shutdown
end
```

|Comando|Para qué sirve|
|---|---|
|`switchport port-security`|Activa la protección en el puerto.|
|`maximum 1`|Permite una sola MAC.|
|`mac-address sticky`|Aprende y guarda la MAC de la primera PC que transmita.|
|`violation shutdown`|Si conectan otra PC, el puerto se apaga (err-disabled).|

### 3.4 Hosts en SW-SERVER

|Puerto|VLAN|Conectar|
|---|---|---|
|fa0/2|10|Server DHCP/TFTP|
|fa0/1|10|PC|
|fa0/8|10|PC|
|fa0/10|20|PC|
|fa0/18|30|PC|
|fa0/22|30|PC|

Las PC de los puertos protegidos aprenden su MAC cuando envían el primer paquete (haz un ping).

**Comprobar:**

```
show vlan brief
show port-security interface fa0/1
show interfaces trunk
```

---

## 4. Reactivo 3: switches cliente (SW-C1, SW-C2, SW-C3)

Cada cliente usa **2 VLAN** distintas, con **mínimo 2 puertos por VLAN**, **2 hosts por VLAN** y port-security en **Fa0/5, Fa0/10 y Fa0/15**. Para que los tres puertos protegidos tengan una PC conectada:

|Switch|Fa0/1-5 → VLAN|Fa0/6-15 → VLAN|PC en|PC en|
|---|---|---|---|---|
|SW-C1|10|20|fa0/4 y fa0/5|fa0/10 y fa0/15|
|SW-C2|20|30|fa0/4 y fa0/5|fa0/10 y fa0/15|
|SW-C3|10|30|fa0/4 y fa0/5|fa0/10 y fa0/15|

### 4.1 SW-C1

```
enable
configure terminal
hostname SW-C1
vtp domain ITESA
vtp mode client
interface range gi0/1-2
 switchport mode trunk
end
```

**Comprueba antes de seguir:**

```
show vlan brief
show vtp status
```

Deben aparecer las VLAN 10, 20 y 30 sin haberlas creado. Si no aparecen: `show interfaces trunk` en ambos extremos y revisa que el dominio sea idéntico.

```
configure terminal
interface range fa0/1-5
 switchport mode access
 switchport access vlan 10
interface range fa0/6-15
 switchport mode access
 switchport access vlan 20
interface range fa0/5, fa0/10, fa0/15
 switchport port-security
 switchport port-security maximum 1
 switchport port-security mac-address sticky
 switchport port-security violation shutdown
end
```

### 4.2 SW-C2

```
enable
configure terminal
hostname SW-C2
vtp domain ITESA
vtp mode client
interface range gi0/1-2
 switchport mode trunk
exit
interface range fa0/1-5
 switchport mode access
 switchport access vlan 20
interface range fa0/6-15
 switchport mode access
 switchport access vlan 30
interface range fa0/5, fa0/10, fa0/15
 switchport port-security
 switchport port-security maximum 1
 switchport port-security mac-address sticky
 switchport port-security violation shutdown
end
```

### 4.3 SW-C3 (último de la cadena, solo `gi0/1`)

```
enable
configure terminal
hostname SW-C3
vtp domain ITESA
vtp mode client
interface gi0/1
 switchport mode trunk
exit
interface range fa0/1-5
 switchport mode access
 switchport access vlan 10
interface range fa0/6-15
 switchport mode access
 switchport access vlan 30
interface range fa0/5, fa0/10, fa0/15
 switchport port-security
 switchport port-security maximum 1
 switchport port-security mac-address sticky
 switchport port-security violation shutdown
end
```

Las PC se configuran en **DHCP**: _Desktop → IP Configuration → DHCP_.

---

## 5. Reactivo 6: router (router-on-a-stick)

```
enable
configure terminal
hostname R1
interface gi0/0
 no shutdown
exit
interface range gi0/1-2
 encapsulation dot1Q 10
 ip address 172.16.0.1 255.255.224.0
exit
interface range gi0/1-2
 encapsulation dot1Q 20
 ip address 172.16.32.1 255.255.240.0
 ip helper-address 172.16.0.6
exit
interface range gi0/1-2
 encapsulation dot1Q 30
 ip address 172.16.48.1 255.255.252.0
 ip helper-address 172.16.0.6
exit
interface range gi0/1-2
 encapsulation dot1Q 1 native
 ip address 172.16.50.1 255.255.255.0
end
write memory
```

|Comando|Para qué sirve|
|---|---|
|`no shutdown` en `gi0/0`|Sin él, todas las subinterfaces quedan caídas.|
|`encapsulation dot1Q N`|Esa subinterfaz atiende la VLAN N. El número debe coincidir con la VLAN.|
|`ip address`|Es el gateway de esa VLAN (la 1.ª asignable de la tabla).|
|`ip helper-address 172.16.0.6`|Reenvía los broadcast de DHCP al servidor, porque no cruzan el router. No hace falta en la VLAN 10, que comparte segmento con el servidor.|
|`dot1Q 1 native`|La VLAN 1 viaja sin etiqueta; esta subinterfaz atiende la red de administración.|

**Comprobar:** `show ip interface brief` debe mostrar las 4 subinterfaces en `up/up`.

Si usas un router 2811, la interfaz se llama `fa0/0`: cambia el nombre en todo el bloque.

---

## 6. Reactivo 2 (DHCP) y reactivo 4 (TFTP): el Server

En el dispositivo _Server_ de Packet Tracer:

**IP estática:** _Desktop → IP Configuration_ → `172.16.0.6` / `255.255.224.0` / gateway `172.16.0.1`.

**DHCP:** _Services → DHCP → On_. Borra o edita el pool `serverPool` y crea **un pool por VLAN** (presiona _Save_ o _Add_ en cada uno):

|Pool|Default Gateway|Start IP|Subnet Mask|Max users|
|---|---|---|---|---|
|VLAN10|172.16.0.1|172.16.0.10|255.255.224.0|50|
|VLAN20|172.16.32.1|172.16.32.10|255.255.240.0|50|
|VLAN30|172.16.48.1|172.16.48.10|255.255.252.0|50|

El Start IP en `.10` evita pisar la IP fija del servidor (172.16.0.6).

**TFTP:** _Services → TFTP → On_.

**Prueba:** una PC de cada VLAN debe recibir IP (`ipconfig` en _Command Prompt_).

---

## 7. Reactivo 4: SSH en la VLAN 1

Repite en **los 4 switches**, cambiando solo la IP de `interface vlan 1` (ver tabla de la sección 1).

```
configure terminal
ip domain-name itesa.local
username angel privilege 15 secret Angel123
username michelle privilege 15 secret Michelle123
username mcruz privilege 15 secret 1231735A
crypto key generate rsa
```

Cuando pregunte los bits, escribe `1024`. Después:

```
ip ssh version 2
interface vlan 1
 ip address 172.16.52.3 255.255.255.0
 no shutdown
exit
ip default-gateway 172.16.52.1
line vty 0 15
 transport input ssh
 login local
end
write memory
```

(Ese ejemplo es SW-C1: usa .2 en SW-SERVER, .4 en SW-C2 y .5 en SW-C3.)

|Comando|Para qué sirve|
|---|---|
|`ip domain-name` + `crypto key generate rsa`|SSH no arranca sin dominio ni llaves. Requiere haber puesto `hostname` antes.|
|`username ... secret`|Un usuario **por cada integrante del equipo** y el usuario extra `mcruz` con `1231735A` (la `A` en mayúscula). Cambia los nombres y claves de `angel` y `michelle` por los tuyos.|
|`interface vlan 1`|Es la dirección del propio switch para administrarlo.|
|`ip default-gateway`|Sin esto el switch no responde a quien venga de otra red.|
|`transport input ssh` + `login local`|Solo SSH, validando contra los usuarios locales.|

**Prueba desde una PC:** _Desktop → Command Prompt_

```
ssh -l mcruz 172.16.52.3
```

---

## 8. Reactivo 4: respaldos en el servidor TFTP

En **cada uno de los 4 switches** (y, de regalo, en el router):

```
write memory
copy running-config tftp
```

Responde a las preguntas así:

```
Address or name of remote host []? 172.16.0.6
Destination filename [SW-C1-confg]? (Enter, o escribe SW-C1-config)
```

Debe salir `!!` y `bytes copied`. Revisa en el Server (_Services → TFTP_) que aparezcan los archivos.

---

## 9. Reactivo 5: pruebas y PDF

Captura pantalla de cada prueba, pégalas en un documento con un título por cada una y expórtalo a PDF.

|Prueba|Comando o acción|
|---|---|
|Tabla VLSM|La tabla de la sección 1|
|VLAN y puertos|`show vlan brief` en los 4 switches|
|VTP|`show vtp status` en SW-SERVER y en un cliente|
|Troncales|`show interfaces trunk`|
|Port-security|`show port-security interface fa0/1` (servidor) y `fa0/5` (cliente)|
|DHCP|`ipconfig` en una PC de cada VLAN|
|Entre VLAN|`ping` de una PC VLAN 10 a una PC VLAN 20 en **otro switch**|
|Router|`show ip interface brief` en R1|
|SSH|`ssh -l mcruz 172.16.52.3`|
|TFTP|Salida de `copy running-config tftp` con `bytes copied`|

**Nombre del archivo:** `Grupo_Actividad_Nombre completo del representante`. Ejemplo: `7F21_Ev_T2_AHUMADA_JUAREZ_ANGEL_DE_JESUS.pdf`. Usa el nombre del representante de tu equipo.

---

## 10. Si algo falla

|Síntoma|Qué revisar|
|---|---|
|El cliente no ve las VLAN|`show interfaces trunk` en ambos switches; dominio VTP idéntico; `vtp mode client` aplicado.|
|La PC saca 169.254.x.x|Pool de DHCP guardado; puerto en la VLAN correcta; `ip helper-address` en la subinterfaz (VLAN 20 y 30).|
|No hay ping entre VLAN|`no shutdown` en `gi0/0` del router; `show ip interface brief` con subinterfaces `up/up`; troncal hacia el router.|
|`port-security` da error|Falta `switchport mode access` antes.|
|SSH no conecta|Falta `ip domain-name` o `crypto key generate rsa`; falta `ip default-gateway`; falta IP en `interface vlan 1`.|
|TFTP no responde|Server con TFTP en On y gateway `172.16.0.1`; ping al `172.16.0.6` desde el switch.|
|Puerto protegido apagado (err-disabled)|Conectaron otra PC: en el puerto, `shutdown` y luego `no shutdown`.|

---

## 11. Lista final antes de entregar

- [ ] Tabla VLSM con 3 filas, sin errores.
- [ ] SW-SERVER con VLAN, puertos y port-security en Fa0/1, 8, 18, 22.
- [ ] DHCP con un pool por VLAN en el Server.
- [ ] 3 switches cliente, 2 VLAN cada uno, 2 hosts por VLAN, port-security en Fa0/5, 10, 15.
- [ ] SSH en los 4 switches con los usuarios del equipo y `mcruz`.
- [ ] Respaldo TFTP de los 4 switches.
- [ ] Router con ping entre VLAN de switches distintos.
- [ ] PDF con todas las evidencias y el nombre correcto.