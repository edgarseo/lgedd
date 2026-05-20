
# SSH


1. Construcción de la Topología Física

- **Añadir el Router:**
    - Ve al menú inferior izquierdo de dispositivos (**Network Devices** -> **Routers**).
    - Selecciona el modelo **2911** o **4331** y arrástralo al área de trabajo.
- **Añadir los Switches:**
    - En el mismo menú, ve a **Switches**.
    - Arrastra dos switches modelo **2960** (uno para la RED_1 y otro para la RED_2).
- **Añadir los Equipos de Usuario (PCs):**
    - Ve al menú **End Devices** -> **End Devices**.
    - Arrastra dos **PC** para la RED_1 y dos **PC** para la RED_2.
- **Añadir el Portátil de Gestión:**
    - En **End Devices**, arrastra un **Laptop** cerca del router.
- **Conexiones de Cableado:**
    - Ve al menú de conexiones (icono del rayo).
    - Usa **Cable Directo (Copper Straight-Through)** para conectar:
        - Los PCs de la RED_1 a los puertos `FastEthernet` del Switch 1.
        - Los PCs de la RED_2 a los puertos `FastEthernet` del Switch 2.
        - El puerto `GigabitEthernet 0/0` del Router al Switch 1.
        - El puerto `GigabitEthernet 0/1` del Router al Switch 2.
    - Usa **Cable de Consola (azul celeste)** para conectar:
        - El puerto **RS-232** del portátil al puerto **Console** del Router.

# Creación de redes

```
Router> ena
Router# conf t

! Configuración de la interfaz para la RED_1 (Clase B)
Router(config)# int fa0/0
Router(config-if)# ip address 172.16.0.1 255.255.0.0
Router(config-if)# no shutdown
Router(config-if)# exit

! Configuración de la interfaz para la RED_2 (Clase C)
Router(config)# int fa1/0
Router(config-if)# ip address 192.168.1.1 255.255.255.0
Router(config-if)# no shutdown
Router(config-if)# exit
Router(config)# end
Router# wr
```

## 2. Desde Consola (terminal), introduce los comandos para la configuración básica del Router: nombre del host, aviso (banner), contraseña del modo privilegiado y contraseña del acceso por la línea de consola. Sal de la configuración del router y cierra el Terminal.


```
Router> enable
Router# configure terminal
Router(config)# hostname RT1
RT1(config)# banner motd #SOLO ACCESO AUTORIZADO#
RT1(config)# enable secret class
RT1(config)# line console 0
RT1(config-line)# password cisco
RT1(config-line)# login
RT1(config-line)# end
RT1#exit
```


## 3. Vuelve a entrar por Consola y visualiza, en el archivo de ejecución, las contraseñas del modo privilegiado y de la línea de consola. Sal de la configuración del router

*Recuerda que has configurado dos contraseñas distintas, una para acceder por consola y otra para acceder al modo privilegiado. Debe pedirte las dos en este paso.*


```
RT1# show running-config | include enable
RT1# show running-config | include password
RT1# exit
```

Verás que la contraseña del modo privilegiado está encriptada, pero que la contraseña de la línea de consola está en texto plano y se puede leer perfectamente.


## 4. Desde CLI, guarda la configuración.

```
RT1# copy running-config startup-config
```



# TELNET

## 1. Desde Consola, configura “telnet” como contraseña de vty para las líneas 0 a 4 (telnet). Sal del modo de configuración en línea y cierra la conexión por consola.

```
RT1(config)# line vty 0 4
RT1(config-line)# password telnet
RT1(config-line)# login
RT1(config-line)# end
RT1#exit
```



## 2. Accede a la configuración del router desde uno de los PC’s mediante Telnet

```
Desktop → Telnet / SSH Client → Connect
Connection Type → Selecciona Telnet
Host Name or (IP address) → Puerta de Enlace de la red (interfaz del router)
```


## 3. Desde Telnet, visualiza las contraseñas de acceso por consola y por telnet, encripta todas las contraseñas de texto no cifrado y comprueba que se han cifrado.

```
RT1# show running-config | include password
RT1# configure terminal
RT1(config)# service password-encryption
RT1(config)# do show running-config | include password
```

## 4.  Desde Telnet, guarda la configuración.

```
RT1# copy running-config startup-config
```




# SSH

## 1. Accede a la configuración del router desde uno de los PC’s mediante Telnet

```
Desktop → Telnet / SSH Client → Connect
Connection Type → Selecciona Telnet
Host Name or (IP address) → Puerta de Enlace de la red (interfaz del router)
```


## 2. Desde Telnet, Introduce los comandos para configurar el acceso por SSH a RT. Configurar acceso SSH, con el usuario “admin” y la contraseña “Admin123”

```
RT1(config)# ip domain-name tunombre.com //PON TU NOMBRE
RT1(config)# crypto key generate rsa //Generar claves (elige 1024)
RT1(config)# username admin privilege 15 secret Admin123
RT1(config)# ip ssh version 2
```





# DMZ

Tarea 1: Topología y Configuración de Interfaces

1. Montaje Físico y Cableado

Conecta los equipos utilizando los puertos exactos especificados en el documento (p. 2):

- **Red Interna:** Conecta `RT1` (Fa0/0) a `SW1` (Fa0/24) (p. 2). Luego `SW1` (Fa0/1) a `PC1`, y `SW1` (Fa0/2) a `PC2` (p. 2).
- **DMZ:** Conecta `RT1` (Fa1/0) a `SW2` (Fa0/24) (p. 2). Luego `SW2` (Fa0/1) a `SRV1`, y `SW2` (Fa0/2) a `SRV2` (p. 2).
- **Entre Routers:** Conecta `RT1` (Fa4/0) con un cable cruzado hacia `RT2` (Fa4/0) (p. 2).
- **Red Externa:** Conecta `RT2` (Fa0/0) directamente a `PC3` (p. 2).

2. Direccionamiento IP en Dispositivos Finales

Configura las IPs estáticas de manera manual en la pestaña **Desktop -> IP Configuration** de cada equipo (p. 2):

- **PC1:** IP `192.168.1.2` | Máscara `255.255.255.0` | Puerta de enlace: `192.168.1.1` (p. 2)
- **PC2:** IP `192.168.1.3` | Máscara `255.255.255.0` | Puerta de enlace: `192.168.1.1` (p. 2)
- **SRV1:** IP `192.168.2.10` | Máscara `255.255.255.0` | Puerta de enlace: `192.168.2.1` (p. 2)
- **SRV2:** IP `192.168.2.20` | Máscara `255.255.255.0` | Puerta de enlace: `192.168.2.1` (p. 2)
- **PC3:** IP `192.168.3.30` | Máscara `255.255.255.0` | Puerta de enlace: `192.168.3.1` (p. 2)

### PARA LA INF FA4/0 QUE DE COLOR GRIS DE RT1 A RT2 CABLE MULTI MODO Y DE RT2 A PC3 CABLE ------

3. Configuración de Interfaces de los Routers (CLI)

Para evitar que se apaguen al reiniciar la práctica, introduce los siguientes comandos desde la pestaña **CLI** de cada router (p. 3):

**En RT1:**

```
Router> enable
Router# configure terminal
Router(config)# hostname RT1

RT1(config)# interface FastEthernet 0/0
RT1(config-if)# ip address 192.168.1.1 255.255.255.0
RT1(config-if)# no shutdown

RT1(config)# interface FastEthernet 1/0
RT1(config-if)# ip address 192.168.2.1 255.255.255.0
RT1(config-if)# no shutdown

RT1(config)# interface FastEthernet 4/0
RT1(config-if)# ip address 200.200.200.2 255.255.255.0
RT1(config-if)# no shutdown
RT1(config-if)# exit

```


**En RT2:**


```
Router> enable
Router# configure terminal
Router(config)# hostname RT2

RT2(config)# interface FastEthernet 4/0
RT2(config-if)# ip address 200.200.200.1 255.255.255.0
RT2(config-if)# no shutdown

RT2(config)# interface FastEthernet 0/0
RT2(config-if)# ip address 192.168.3.1 255.255.255.0
RT2(config-if)# no shutdown
RT2(config-if)# exit
```



Tareas 2 y 3: Pruebas Iniciales y Enrutamiento Estático

Tarea 2: Verificación previa (p. 3)

Haz un ping desde **PC1** a **SRV1** (debe funcionar porque están conectados al mismo router `RT1`) (p. 3). Haz un ping desde **PC1** a **PC3** (debe fallar, ya que los routers aún no conocen los caminos hacia las otras redes) (p. 3).

Tarea 3: Configuración de Rutas por Defecto (p. 3)

Aplica el comando `ip route` para enlazar ambas redes (p. 3).

- **En RT1:** Todo el tráfico desconocido debe enviarse hacia la IP de la interfaz del router vecino `RT2` (p. 3).

```
RT1(config)# ip route 0.0.0.0 0.0.0.0 200.200.200.1
```

**En RT2:** Todo el tráfico de regreso hacia las redes internas y DMZ debe apuntar a la interfaz de `RT1` (p. 3).

```
RT2(config)# ip route 0.0.0.0 0.0.0.0 200.200.200.2
```


Tarea 4: Verificación de Conectividad Total (p. 3)

Realiza un ping desde **PC3** hacia **PC1**, **SRV1** y **SRV2** (p. 3). En este punto, todos los pings deben responder de manera exitosa porque la red aún no está protegida (p. 3). _(¡Guarda una copia de seguridad del archivo aquí!)_ (p. 3)


Tarea 5: Configuración de Seguridad (ACLs)

Para cumplir los requisitos de filtrado, utilizaremos una **Lista de Control de Acceso Extendida (ACL)** (p. 4). La colocaremos en el router principal (`RT1`), en su interfaz conectada a Internet, filtrando el tráfico entrante (p. 2).

Ejecuta las siguientes reglas en la línea de comandos de **RT1**:


```
RT1(config)# ip access-list extended SEGURIDAD_DMZ

! 1. Permitir respuestas de tráfico que se originaron en la Red Interna o DMZ (Establish)
RT1(config-ext-nacl)# permit tcp any any established
RT1(config-ext-nacl)# permit icmp any any echo-reply

! 2. Restringir el acceso desde la Red Externa permitiendo ÚNICAMENTE tráfico web (puerto 80) a SRV2
RT1(config-ext-nacl)# permit tcp 192.168.3.0 0.0.0.255 host 192.168.2.20 eq 80

! 3. Denegar de forma implícita el resto de accesos no autorizados desde el exterior
RT1(config-ext-nacl)# exit

! 4. Aplicar la lista en la interfaz que recibe el tráfico de Internet (Fa4/0) en modo entrada (in)
RT1(config)# interface FastEthernet 4/0
RT1(config-if)# ip access-group SEGURIDAD_DMZ in
RT1(config-if)# end
RT1# write memory

```


Tarea 6: Pruebas de Conectividad Finales

Realiza las siguientes comprobaciones para validar las políticas de seguridad (p. 4):

1. **Desde PC1 o PC2 (Red Interna):** Abre el navegador web o la terminal y accede a `192.168.2.10` (SRV1) y `192.168.2.20` (SRV2) (pp. 2, 4). El acceso debe estar operativo (p. 4).
2. **Desde PC1 o PC2 (Red Interna):** Haz un ping a `192.168.3.30` (PC3) (pp. 2, 4). El ping responderá correctamente (p. 4).
3. **Desde PC3 (Red Externa):** Abre el **Web Browser**, escribe la IP `192.168.2.20` (SRV2) y pulsa Ir (pp. 2, 4). La página web debe cargar con éxito (p. 4).
4. **Desde PC3 (Red Externa):** Intenta hacer un ping a **PC1**, **PC2** o **SRV1** (pp. 2, 4). Todos los intentos deben fallar (Request timed out), confirmando el blindaje de la red (p. 4).


# WAN Y NAT

Tarea 1: Construcción de la Topología Física y Cableado

Sigue rigurosamente las conexiones de puertos que indica tu documento (p. 2):

1. **Desplegar Routers:** Arrastra 3 routers genéricos (**PT-Router**). Nómbralos como `Router-Central`, `Router-Secundario` e `ISP` (p. 2).
    - _Nota de fibra/serial:_ Asegúrate de que `Router-Central` y `Router-Secundario` tengan tarjetas de interfaz Serial antes de cablear.
2. **Desplegar Switches y Dispositivos Finales:**
    - Coloca un switch en la Sede Central conectado a **PC1**, **PC2** y el servidor **SRV1** (p. 2).
    - Coloca otro switch en la Sede Secundaria conectado a **PC3**, **PC4** y **PC5** (p. 2).
    - Coloca el portátil **LAP1** en la zona exterior (p. 2).
3. **Realizar las Conexiones exactas (p. 2):**
    - **Sede Central:** Conecta la interfaz `Fa0/0` del `Router-Central` hacia su switch (p. 2).
    - **Enlace de Internet:** Conecta la interfaz `Fa4/0` del `Router-Central` al puerto `Fa4/0` del router `ISP` (pp. 2-3).
    - **Conexión WAN entre Sucursales:** Conecta un **Cable Serial DCE (reloj)** desde el puerto `Serial2/0` de `Router-Central` hacia el puerto `Serial2/0` de `Router-Secundario` (p. 2).
    - **Sede Secundaria:** Conecta la interfaz `Fa0/0` del `Router-Secundario` hacia su switch (p. 2).
    - **Red Externa:** Conecta la interfaz `Fa0/0` del `ISP` hacia el portátil **LAP1** (p. 3).

---

Tarea 2: Configuración del Direccionamiento IP (Host y Servidores)

Configura los parámetros manuales en cada terminal desde la pestaña **Desktop -> IP Configuration** (p. 3):

- **PC1:** IP `192.168.10.11` | Máscara `255.255.255.0` | Gateway: `192.168.10.1` (p. 3)
- **PC2:** IP `192.168.10.12` | Máscara `255.255.255.0` | Gateway: `192.168.10.1` (p. 3)
- **SRV1 (Web):** IP `192.168.10.100` | Máscara `255.255.255.0` | Gateway: `192.168.10.1` (p. 3)
- **PC3:** IP `192.168.20.11` | Máscara `255.255.255.0` | Gateway: `192.168.20.1` (p. 3)
- **PC4:** IP `192.168.20.12` | Máscara `255.255.255.0` | Gateway: `192.168.20.1` (p. 3)
- **PC5:** IP `192.168.20.13` | Máscara `255.255.255.0` | Gateway: `192.168.20.1` (p. 3)
- **LAP1:** IP `100.100.100.30` | Máscara `255.255.255.0` | Gateway: `100.100.100.1` (p. 3)

---

Tarea 3: Configuración de Interfaces y Enrutamiento en Routers

Aplica de forma estricta los siguientes bloques de comandos en la pestaña **CLI** de cada router. _(Ten en cuenta que la máscara `/29` equivale a `255.255.255.248` y la `/30` a `255.255.255.252` (p. 3))._

1. Configuración de Router-Central

```
Router> enable
Router# configure terminal
Router(config)# hostname Router-Central

! Interfaces locales y WAN
Router-Central(config)# interface FastEthernet 0/0
Router-Central(config-if)# ip address 192.168.10.1 255.255.255.0
Router-Central(config-if)# no shutdown

Router-Central(config)# interface FastEthernet 4/0
Router-Central(config-if)# ip address 200.200.200.2 255.255.255.248
Router-Central(config-if)# no shutdown

! Configuración del Reloj en el extremo DCE de la WAN
Router-Central(config)# interface Serial 2/0
Router-Central(config-if)# ip address 10.0.0.1 255.255.255.252
Router-Central(config-if)# clock rate 64000
Router-Central(config-if)# no shutdown
Router-Central(config-if)# exit

! Enrutamiento Estático
Router-Central(config)# ip route 0.0.0.0 0.0.0.0 200.200.200.1
Router-Central(config)# ip route 192.168.20.0 255.255.255.0 10.0.0.2

```


2. Configuración de Router-Secundario

```
Router> enable
Router# configure terminal
Router(config)# hostname Router-Secundario

Router-Secundario(config)# interface FastEthernet 0/0
Router-Secundario(config-if)# ip address 192.168.20.1 255.255.255.0
Router-Secundario(config-if)# no shutdown

Router-Secundario(config)# interface Serial 2/0
Router-Secundario(config-if)# ip address 10.0.0.2 255.255.255.252
Router-Secundario(config-if)# no shutdown
Router-Secundario(config-if)# exit

! Ruta estática por defecto hacia Central
Router-Secundario(config)# ip route 0.0.0.0 0.0.0.0 10.0.0.1
```

3. Configuración del Router ISP

```
Router> enable
Router# configure terminal
Router(config)# hostname ISP

Router(config)# interface FastEthernet 4/0
Router(config-if)# ip address 200.200.200.1 255.255.255.248
Router(config-if)# no shutdown

Router(config)# interface FastEthernet 0/0
Router(config-if)# ip address 100.100.100.1 255.255.255.0
Router(config-if)# no shutdown

! Configuración del entorno de Internet simulado (Loopback)
ISP(config)# interface loopback 0
ISP(config-if)# ip address 8.8.8.8 255.255.255.255
ISP(config-if)# exit

! Ruta de regreso a la red pública asignada
ISP(config)# ip route 200.200.200.0 255.255.255.248 fastEthernet 4/0

```


Tarea 5: Personalización del Servidor Web (SRV1)

1. Haz clic en **SRV1** (p. 6).
2. Ve a la pestaña **Services** -> submenú **HTTP** (p. 6).
3. Asegúrate de que los botones **HTTP** y **HTTPS** estén marcados en **On** (p. 6).
4. Busca el archivo `index.html` en la lista y haz clic en **Edit** (p. 6).
5. Modifica el código HTML del documento para añadir una línea visible con tu **Nombre y Apellidos** (p. 6). Guarda los cambios.

---

Tarea 6: Protocolo de Verificación Final (Pruebas)

Ejecuta el banco de pruebas oficial para garantizar el funcionamiento del NAT (p. 6):

1. **Comunicación Inter-Sede:** Desde el terminal de **PC2**, haz `ping 192.168.20.12` (PC4) (p. 6). Debe haber respuesta limpia.
2. **Navegación de Internet:** Desde **PC1** o **PC3**, abre la terminal y haz `ping 8.8.8.8` (p. 6). Debe responder de inmediato (gracias a la traducción NAT con sobrecarga) (p. 5).
3. **Visualización remota Web (Externa):** Abre el **Web Browser** de **LAP1** e ingresa en la barra de direcciones la IP pública: `http://200.200.200.2` (p. 6). Debe abrir la página web mostrando tus datos (p. 6).
4. **Auditoría de Traducciones:** Ve al modo privilegiado de `Router-Central` y ejecuta:

```
Router-Central# show ip nat translations
```


## WAN y NAT (DHCP desde Router)

Tarea 1: Construcción de la Topología y Cableado

Sigue rigurosamente las conexiones de puertos indicadas (Práctica ... p. 2):

1. **Desplegar Routers:** Arrastra 3 routers genéricos (**PT-Router**). Cámbiales el nombre exacto a `Router-Central`, `Router-Secundario` e `ISP` (Práctica ... p. 2).
2. **Desplegar Switches y Dispositivos Finales:**
    - Coloca un switch en la Sede Central y conéctale el **PC1**, **PC2** y el servidor **SRV1** (Práctica ... p. 2).
    - Coloca otro switch en la Sede Secundaria y conéctale el **PC3**, **PC4** y **PC5** (Práctica ... p. 2).
    - Coloca el portátil **LAP1** en la zona exterior (Práctica ... p. 2).
3. **Realizar las Conexiones exactas:**
    - **Router-Central:** Conecta la interfaz `Fa0/0` al switch de la Sede Central (Práctica ... p. 2). Conecta la interfaz `Fa4/0` al puerto `Fa4/0` del `ISP` (Práctica ... p. 2).
    - **Enlace WAN:** Conecta un **Cable Serial DCE (reloj)** desde el puerto `Serial2/0` de `Router-Central` hacia el puerto `Serial2/0` de `Router-Secundario` (Práctica ... p. 2).
    - **Router-Secundario:** Conecta la interfaz `Fa0/0` al switch de la Sede Secundaria (Práctica ... p. 2).
    - **Red Externa:** Conecta la interfaz `Fa0/0` del `ISP` directamente al portátil **LAP1** usando un cable cruzado (Práctica ... pp. 2-3).

---

Tarea 2: Configuración del Direccionamiento IP en Equipos

Configura manualmente los parámetros en la pestaña **Desktop -> IP Configuration** de cada terminal (Práctica ... p. 3):

- **PC1:** IP `192.168.10.11` | Máscara `255.255.255.0` | Puerta de enlace: `192.168.10.1` (Práctica ... p. 3)
- **PC2:** IP `192.168.10.12` | Máscara `255.255.255.0` | Puerta de enlace: `192.168.10.1` (Práctica ... p. 3)
- **SRV1 (Web):** IP `192.168.10.100` | Máscara `255.255.255.0` | Puerta de enlace: `192.168.10.1` (Práctica ... p. 3)
- **PC3:** IP `192.168.20.11` | Máscara `255.255.255.0` | Puerta de enlace: `192.168.20.1` (Práctica ... p. 3)
- **PC4:** IP `192.168.20.12` | Máscara `255.255.255.0` | Puerta de enlace: `192.168.20.1` (Práctica ... p. 3)
- **PC5:** IP `192.168.20.13` | Máscara `255.255.255.0` | Puerta de enlace: `192.168.20.1` (Práctica ... p. 3)
- **LAP1:** IP `100.100.100.30` | Máscara `255.255.255.0` | Puerta de enlace: `100.100.100.1` (Práctica ... p. 3)

---

Tarea 3: Configuración de Interfaces y Enrutamiento en los Routers

Entra en la pestaña **CLI** de cada router y aplica los siguientes bloques de comandos básicos y de enrutamiento (Práctica ... pp. 3-4).  
_(Nota técnica: la máscara `/29` equivale a `255.255.255.248` y la `/30` a `255.255.255.252` (Práctica ... p. 3))._

1. Configuración de Router-Central

```
Router> enable
Router# configure terminal
Router(config)# hostname Router-Central

! Configurar interfaces físicas
Router-Central(config)# interface FastEthernet 0/0
Router-Central(config-if)# ip address 192.168.10.1 255.255.255.0
Router-Central(config-if)# no shutdown

Router-Central(config)# interface FastEthernet 4/0
Router-Central(config-if)# ip address 200.200.200.2 255.255.255.248
Router-Central(config-if)# no shutdown

! Configurar interfaz WAN (Extremo DCE con Reloj)
Router-Central(config)# interface Serial 2/0
Router-Central(config-if)# ip address 10.0.0.1 255.255.255.252
Router-Central(config-if)# clock rate 64000
Router-Central(config-if)# no shutdown
Router-Central(config-if)# exit

! Enrutamiento Estático
Router-Central(config)# ip route 0.0.0.0 0.0.0.0 200.200.200.1
Router-Central(config)# ip route 192.168.20.0 255.255.255.0 10.0.0.2

```


2. Configuración de Router-Secundario

```
Router> enable
Router# configure terminal
Router(config)# hostname Router-Secundario

Router-Secundario(config)# interface FastEthernet 0/0
Router-Secundario(config-if)# ip address 192.168.20.1 255.255.255.0
Router-Secundario(config-if)# no shutdown

Router-Secundario(config)# interface Serial 2/0
Router-Secundario(config-if)# ip address 10.0.0.2 255.255.255.252
Router-Secundario(config-if)# no shutdown
Router-Secundario(config-if)# exit

! Ruta estática por defecto hacia Central
Router-Secundario(config)# ip route 0.0.0.0 0.0.0.0 10.0.0.1

```


3. Configuración del Router ISP

```
Router> enable
Router# configure terminal
Router(config)# hostname ISP

Router(config)# interface FastEthernet 4/0
Router(config-if)# ip address 200.200.200.1 255.255.255.248
Router(config-if)# no shutdown

Router(config)# interface FastEthernet 0/0
Router(config-if)# ip address 100.100.100.1 255.255.255.0
Router(config-if)# no shutdown

! Configurar Internet simulado via Loopback
ISP(config)# interface loopback 0
ISP(config-if)# ip address 8.8.8.8 255.255.255.255
ISP(config-if)# exit

! Ruta de regreso a las IPs públicas asignadas
ISP(config)# ip route 200.200.200.0 255.255.255.248 fastEthernet 4/0

```


Tarea 4: Configurar NAT y PAT (En Router-Central)

```
Router-Central# configure terminal

! Definir interfaces internas y externas para NAT
Router-Central(config)# interface FastEthernet 0/0
Router-Central(config-if)# ip nat inside

Router-Central(config)# interface Serial 2/0
Router-Central(config-if)# ip nat inside

Router-Central(config)# interface FastEthernet 4/0
Router-Central(config-if)# ip nat outside
Router-Central(config-if)# exit

! Crear la ACL para identificar el tráfico privado que se traducirá
Router-Central(config)# access-list 1 permit 192.168.10.0 0.0.0.255
Router-Central(config)# access-list 1 permit 192.168.20.0 0.0.0.255

! Habilitar NAT con sobrecarga (PAT)
Router-Central(config)# ip nat inside source list 1 interface FastEthernet 4/0 overload

! Redirección de puertos (Port Forwarding) para el servidor web público
Router-Central(config)# ip nat inside source static tcp 192.168.10.100 80 200.200.200.2 80
Router-Central(config)# end
Router-Central# write memory

```

Tarea 5: Configurar Servidor Web (SRV1)

1. Haz clic sobre **SRV1** (Práctica ... p. 6).
2. Ve a la pestaña **Services** -> sección **HTTP** (Práctica ... p. 6).
3. Activa las casillas **HTTP** y **HTTPS** marcando **On** (Práctica ... p. 6).
4. Busca el archivo `index.html`, haz clic en **Edit**, e introduce tu **Nombre y Apellidos** dentro del código HTML (Práctica ... p. 6). Guarda el archivo (Práctica ... p. 6).

---

Tarea 6: Pruebas de Verificación Obligatorias

Lanza las siguientes comprobaciones de conectividad desde las terminales (Práctica ... p. 6):

1. **Conexión entre sedes:** Desde **PC2** haz `ping 192.168.20.12` (PC4) y desde **PC3** haz `ping 192.168.10.11` (PC1) (Práctica ... p. 6).
2. **Acceso a Internet:** Desde **PC1**, **PC3** o **SRV1** haz `ping 8.8.8.8` (debe responder exitosamente) (Práctica ... p. 6).
3. **Navegador Interno:** Desde **PC4** abre el navegador e ingresa a `http://192.168.10.100` (Práctica ... p. 6).
4. **Navegador Externo:** Desde **LAP1** abre el navegador e ingresa a la IP pública `http://200.200.200.2` (Práctica ... p. 6).


# VTP (VLAN Trunking Protocol)


Tarea 1: Construcción de la Topología y Cableado

Despliega los siguientes equipos en el lienzo de Packet Tracer (Practica11... p. 1):

1. **Añadir Switches:**
    - Un switch multicapa modelo **3560** y renombralo como `SW-CORE` (Practica11... p. 1).
    - Dos switches modelo **2960** y renombralos como `SW1` y `SW2` (Practica11... p. 1).
2. **Añadir Equipos:** Cuatro **PC** independientes (Practica11... p. 1).
3. **Conexiones Físicas (Cable Directo):**
    - Del puerto `Gig0/1` de `SW-CORE` al puerto `Gig0/1` de `SW1` (Practica11... pp. 1, 3).
    - Del puerto `Gig0/2` de `SW-CORE` al puerto `Gig0/1` de `SW2` (Practica11... pp. 1, 4).
    - De `SW1`: Puerto `Fa0/10` a **PC1** y puerto `Fa0/20` a **PC2** (Practica11... p. 1).
    - De `SW2`: Puerto `Fa0/10` a **PC3** y puerto `Fa0/20` a **PC4** (Practica11... p. 1)



Tarea 2: Configuración del Switch Principal (SW-CORE)

Este dispositivo actuará como el **Servidor VTP**, centralizando la creación de VLANs (Practica11... p. 1). Abre su pestaña **CLI** y ejecuta:


```
Switch> enable
Switch# configure terminal 
Switch(config)# hostname SW-CORE 
SW-CORE(config)# enable secret cisco

! Configurar el protocolo VTP en modo Servidor
SW-CORE(config)# vtp domain EMPRESA
SW-CORE(config)# vtp mode server
SW-CORE(config)# vtp password cisco123

! Crear la base de datos de VLANs
SW-CORE(config)# vlan 10
SW-CORE(config-vlan)# name Administracion 
SW-CORE(config-vlan)# exit
SW-CORE(config)# vlan 20 
SW-CORE(config-vlan)# name Ventas 
SW-CORE(config-vlan)# exit

! Configurar enlaces troncales hacia los switches de acceso
SW-CORE(config)# interface range GigabitEthernet0/1-2 
SW-CORE(config-if-range)# switchport mode trunk
SW-CORE(config-if-range)# no shutdown 
SW-CORE(config-if-range)# end
SW-CORE# write memory

```


Tarea 3: Configuración del Switch de Acceso 1 (SW1)

Este switch recibirá las VLANs automáticamente por VTP (Practica11... p. 5). Abre su pestaña **CLI** y ejecuta (Practica11... p. 2):


```
Switch> enable
Switch# configure terminal 
Switch(config)# hostname SW1
SW1(config)# enable secret cisco

! Vincular al dominio VTP en modo Cliente
SW1(config)# vtp domain EMPRESA
SW1(config)# vtp mode client
SW1(config)# vtp password cisco123

! Configurar enlace troncal hacia el núcleo
SW1(config)# interface GigabitEthernet0/1
SW1(config-if)# switchport mode trunk 
SW1(config-if)# no shutdown
SW1(config-if)# exit

! Asignar puertos de acceso a sus respectivas VLANs
SW1(config)# interface FastEthernet0/10 
SW1(config-if)# switchport mode access 
SW1(config-if)# switchport access vlan 10
SW1(config-if)# no shutdown 
SW1(config-if)# exit

SW1(config)# interface FastEthernet0/20 
SW1(config-if)# switchport mode access 
SW1(config-if)# switchport access vlan 20 
SW1(config-if)# no shutdown
SW1(config-if)# end
SW1# write memory

```


Tarea 4: Configuración del Switch de Acceso 2 (SW2)

Repite el proceso en el segundo cliente de acceso (Practica11... p. 3). Abre su pestaña **CLI** y ejecuta (Practica11... pp. 3-4):

```
Switch> enable
Switch# configure terminal 
Switch(config)# hostname SW2
SW2(config)# enable secret cisco

! Vincular al dominio VTP en modo Cliente
SW2(config)# vtp domain EMPRESA
SW2(config)# vtp mode client
SW2(config)# vtp password cisco123

! Configurar enlace troncal hacia el núcleo
SW2(config)# interface GigabitEthernet0/1
SW2(config-if)# switchport mode trunk 
SW2(config-if)# no shutdown
SW2(config-if)# exit

! Asignar puertos de acceso a sus respectivas VLANs
SW2(config)# interface FastEthernet0/10 
SW2(config-if)# switchport mode access 
SW2(config-if)# switchport access vlan 10
SW2(config-if)# no shutdown 
SW2(config-if)# exit

SW2(config)# interface FastEthernet0/20 
SW2(config-if)# switchport mode access 
SW2(config-if)# switchport access vlan 20 
SW2(config-if)# no shutdown
SW2(config-if)# end
SW2# write memory
```


Tarea 5: Configuración de Direcciones IP en los PCs

Entra de forma manual en la pestaña **Desktop -> IP Configuration** de cada ordenador (Practica11... p. 5):

- **PC1 (VLAN 10 en SW1):** IP `192.168.10.10` | Máscara `255.255.255.0` | Gateway: Dejar en blanco (Practica11... p. 5).
- **PC2 (VLAN 20 en SW1):** IP `192.168.20.10` | Máscara `255.255.255.0` | Gateway: Dejar en blanco (Practica11... p. 5).
- **PC3 (VLAN 10 en SW2):** IP `192.168.10.20` | Máscara `255.255.255.0` | Gateway: Dejar en blanco (Practica11... p. 5).
- **PC4 (VLAN 20 en SW2):** IP `192.168.20.20` | Máscara `255.255.255.0` | Gateway: Dejar en blanco (Practica11... p. 5).

Tarea 6: Auditoría y Pruebas obligatorias

Valida que el protocolo de sincronización haya completado su ciclo operativo (Practica11... pp. 5-6):

1. **Diagnóstico VTP:** En **SW1** y **SW2**, ejecuta `show vtp status` en modo privilegiado para cerciorarte de que están en modo cliente bajo el dominio EMPRESA (Practica11... pp. 2, 4-5).
2. **Validar Propagación:** Ejecuta `show vlan brief` en los switches cliente (Practica11... p. 5). Deben listar de forma automática las VLANs 10 (Administracion) y 20 (Ventas) creadas originalmente solo en el Core (Practica11... pp. 2, 5).
3. **Comprobación de Comunicación Local:** Abre el **Command Prompt** de **PC1** y realiza `ping 192.168.10.20` (PC3) (Practica11... p. 6). La traza debe responder exitosamente debido a que comparten la misma VLAN (Practica11... p. 6).
4. **Aislamiento de Tráfico:** Desde **PC1**, lanza un `ping 192.168.20.10` (PC2) (Practica11... p. 6). El entorno de red debe arrojar **Time out**, ya que al no existir un enrutador o switch de capa 3 operativo para Inter-VLAN routing, las redes se mantienen totalmente separadas (Practica11... p. 6).





# Router on a stick


Paso 1: Conexión Física del Router

1. Ve al menú de dispositivos y añade un router (el modelo **2911** o **ISR4331** funcionará perfectamente). Nómbralo como `RT-INTERVLAN`.
2. Selecciona un **Cable Directo (Copper Straight-Through)**.
3. Conecta el puerto **fa0/0** del router a un puerto fast libre del switch principal, por ejemplo, el puerto **fa0/1** de `SW-CORE` (p. 1).



Paso 2: Configurar el Enlace Troncal en el SW-CORE

Para que el router reciba el tráfico de ambas VLANs, el puerto del switch conectado al router debe configurarse obligatoriamente en modo troncal (Trunk) (p. 2).

Entra al CLI de `SW-CORE` y ejecuta:

```
Router> enable
Router# configure terminal

! 1. ¡MUY IMPORTANTE! Encender la interfaz física principal (sin asignarle IP)
Router(config)# interface fastEthernet 0/0
Router(config-if)# no shutdown
Router(config-if)# exit

! 2. Configurar subinterfaz para VLAN 10
Router(config)# interface fastEthernet 0/0.10
Router(config-subif)# encapsulation dot1q 10
Router(config-subif)# ip address 192.168.10.1 255.255.255.0
Router(config-subif)# exit

! 3. Configurar subinterfaz para VLAN 20
Router(config)# interface fastEthernet 0/0.20
Router(config-subif)# encapsulation dot1q 20
Router(config-subif)# ip address 192.168.20.1 255.255.255.0
Router(config-subif)# exit

! 4. Guardar la configuración de forma permanente
Router(config)# end
Router# write memory

```



3. Recordatorio Crítico del Switch

Para que las subinterfaces que acabas de crear capturen los paquetes, el puerto del switch donde conectaste el cable `fa0/0` del router (por ejemplo, el `fa0/24`) debe estar configurado como **Trunk**:


```
En switch (SW-CORE):

! Configurar el puerto que conecta al router como troncal

Switch(config)# interface fastEthernet 0/1  
Switch(config-if)# switchport trunk encapsulation dot1q 
Switch(config-if)# switchport mode trunk 
Switch(config-if)# no shutdown
Switch(config-if)# exit
Switch(config)# end
Switch# wr
```



Paso 4: Configurar el Default Gateway en los PCs

Para que los ordenadores sepan a dónde enviar los paquetes cuando quieran comunicarse con otra red, debes rellenar el campo **Default Gateway** que habías dejado en blanco (p. 5).

Haz clic en cada PC, ve a **Desktop -> IP Configuration** y añade la IP del router correspondiente a su VLAN (p. 5):

- **PC1 (VLAN 10):** Default Gateway ➔ `192.168.10.1` (p. 5)
- **PC2 (VLAN 20):** Default Gateway ➔ `192.168.20.1` (p. 5)
- **PC3 (VLAN 10):** Default Gateway ➔ `192.168.10.1` (p. 5)
- **PC4 (VLAN 20):** Default Gateway ➔ `192.168.20.1` (p. 5)

---

Paso 5: Pruebas de Verificación Final

Una vez que todas las luces del nuevo enlace cambien a color verde, realiza las siguientes pruebas desde la terminal de comandos (_Command Prompt_):

1. **Ping Inter-VLAN:** Desde el **PC1** (VLAN 10), ejecuta un ping hacia el **PC2** (VLAN 20): `ping 192.168.20.10` (pp. 5-6).
2. **Resultado esperado:** A diferencia de la fase anterior, **el ping ahora debe responder con éxito** (p. 6). _(Es normal que el primer paquete falle por la resolución ARP del router, los siguientes responderán perfectamente)._




# SWITCH MULTICAPA


```
Con esta configuración, el switch 3560 actuará como router entre las dos VLANs,

permitiendo que los dispositivos en la VLAN 10 (192.168.10.0/24) puedan comunicarse con los dispositivos en la VLAN 20 (192.168.20.0/24) y viceversa.

! Primero, habilitamos el enrutamiento IP en el switch

Switch(config)# ip routing

1. Activar la SVI para la VLAN 10 y asignarle su IP de gestión/gateway
   
SW-CORE(config)# interface vlan 10
SW-CORE(config-if)# ip address 192.168.10.1 255.255.255.0
SW-CORE(config-if)# no shutdown
SW-CORE(config-if)# exit

1. Activar la SVI para la VLAN 20 y asignarle su IP de gestión/gateway
   
SW-CORE(config)# interface vlan 20
SW-CORE(config-if)# ip address 192.168.20.1 255.255.255.0
SW-CORE(config-if)# no shutdown
SW-CORE(config-if)# exit
…….

! Guardar la configuración

Switch(config)# end

Switch# write memory
```



# VLAN, DHCP y Subnetting

## OPCIONAL
Tarea 1: Configuración Básica del Switch Multicapa (SW1)

Abre la pestaña **CLI** de tu switch multicapa 3560 y ejecuta estos comandos básicos de seguridad y personalización (pp. 1, 3):

```
Switch> enable
Switch# configure terminal

! Cambiar el nombre del dispositivo
Switch(config)# hostname SW1

! Securizar el modo privilegiado (contraseña obligatoria: cisco)
SW1(config)# enable secret cisco

! Configurar el mensaje de advertencia obligatorio
SW1(config)# banner motd #ACCESO RESTRINGIDO#
SW1(config)# exit
SW1#

```


Tarea 2: Creación de VLANs y Asignación de Puertos

Crea las tres VLANs requeridas y asocia los rangos de puertos FastEthernet indicados en la guía (pp. 1, 4):

```
SW1# configure terminal

SW1# ip routing

! 1. Crear la base de datos de VLANs
SW1(config)# vlan 10
SW1(config-vlan)# name USUARIOS
SW1(config-vlan)# exit

SW1(config)# vlan 20
SW1(config-vlan)# name IMPRESORAS
SW1(config-vlan)# exit

SW1(config)# vlan 30
SW1(config-vlan)# name SERVIDORES
SW1(config-vlan)# exit

2. Asignar los puertos fa0/1 a fa0/10 a la VLAN 10

conf t
interface range fa0/1 - 10
switchport mode access
switchport access vlan 10
exit
2. Asignar los puertos fa0/11 a fa0/15 a la VLAN 20
interface range fa0/11 - 15
switchport mode access
switchport access vlan 20
exit


3. Asignar los puertos fa0/16 a fa0/20 a la VLAN 30
   
interface range fa0/16 - 20
switchport mode access
switchport access vlan 30
exit
end


```



Tarea 3: Enrutamiento Inter-VLAN (SVIs) y DHCP Relay

Habilita el enrutamiento de capa 3 por hardware y configura las IPs calculadas de las puertas de enlace (_Gateways_) para cada subred (`/26` equivale a `255.255.255.192`) (pp. 4-5):


```
! Habilitar de forma explícita el enrutamiento IP en el switch multicapa
SW1(config)# ip routing

! Configurar Gateway para la VLAN 10 (Subred 0)
SW1(config)# interface vlan 10
SW1(config-if)# ip address 192.168.0.1 255.255.255.192
SW1(config-if)# description Gateway para USUARIOS
SW1(config-if)# no shutdown
SW1(config-if)# exit

! Configurar Gateway para la VLAN 20 (Subred 1)
SW1(config)# interface vlan 20
SW1(config-if)# ip address 192.168.0.65 255.255.255.192
SW1(config-if)# description Gateway para IMPRESORAS
SW1(config-if)# no shutdown
SW1(config-if)# exit

! Configurar Gateway para la VLAN 30 (Subred 2)
SW1(config)# interface vlan 30
SW1(config-if)# ip address 192.168.0.129 255.255.255.192
SW1(config-if)# description Gateway para SERVIDORES
SW1(config-if)# no shutdown
SW1(config-if)# exit

! 7. Configuración de DHCP Relay (ip helper-address) en la VLAN 10
! (Apunta a la IP estática que le asignaremos al SrvDHCP: 192.168.0.130)
SW1(config)# interface vlan 10
SW1(config-if)# ip helper-address 192.168.0.130
SW1(config-if)# end

! ¡GUARDADO CRÍTICO OBLIGATORIO!
SW1# copy running-config startup-config

```


Tarea 4: Configuración Estática de Servidores e Impresora

Entra en la pestaña **Desktop -> IP Configuration** de los siguientes dispositivos de forma estática (pp. 4, 6):

- **PRT1 (Impresora - VLAN 20):**
    - IP Address: `192.168.0.66`
    - Subnet Mask: `255.255.255.192`
    - Default Gateway: `192.168.0.65`
- **SrvDHCP (Servidor DHCP - VLAN 30):**
    - IP Address: `192.168.0.130`
    - Subnet Mask: `255.255.255.192`
    - Default Gateway: `192.168.0.129`
    - DNS Server: `8.8.8.8`
- **SrvWEB (Servidor Web - VLAN 30):**
    - IP Address: `192.168.0.131`
    - Subnet Mask: `255.255.255.192`
    - Default Gateway: `192.168.0.129`
    - DNS Server: `8.8.8.8`



Tarea 5: Configuración del Servicio DHCP en SrvDHCP

1. Haz clic en el servidor **SrvDHCP** (pp. 2, 6).
2. Ve a **Services** -> **DHCP** (p. 6).
3. Marca la casilla **Service** en **On** (p. 6).
4. Rellena los datos exactos calculados para la **Red_Usuarios** (Subred 0) (p. 6):
    - **Pool Name:** `Red_Usuarios`
    - **Gateway:** `192.168.0.1`
    - **DNS Server:** `8.8.8.8`
    - **Start IP Address:** `192.168.0.2`
    - **Subnet Mask:** `255.255.255.192`
    - **Maximum Number of Users:** `61` _(Rango útil disponible del .2 al .62)_ (pp. 4, 6).
5. Haz clic en el botón **Save** (o **Add**)


Tarea 6: Verificación y Entrega

1. Entra a **PC0** y **PC1**, ve a **IP Configuration** y activa la casilla **DHCP** (p. 7).
2. Comprueba que obtienen una IP válida en el rango `192.168.0.x` con máscara `255.255.255.192` (p. 4). _(Si te sale una IP 169.254.x.x, adelanta el tiempo simulado con el botón de flechas rápidas `>>` en la esquina inferior izquierda hasta que sincronice)_ (p. 7).
3. Abre el **Command Prompt** de **PC0** y haz `ping 192.168.0.131` (SrvWEB). Debe responder con éxito gracias al enrutamiento del switch multicapa (p. 6).



# RIPv2

Tarea 1: Resolución de la Tabla de Encaminamiento de RT1

Para completar la tabla de **RT1**, debemos considerar las redes que tiene conectadas directamente (Distancia Administrativa = 0) y las que aprende mediante el protocolo dinámico **RIPv2** (Distancia Administrativa = 120) (pp. 1-2).

La métrica en RIP corresponde estrictamente al **número de routers (saltos)** que se deben atravesar para llegar al destino (p. 2).

|Red destino|Máscara|Tipo|Distancia Adm. / Métrica|Siguiente salto|Interfaz de salida|
|---|---|---|---|---|---|
|**192.168.10.0**|/24|**C**|- / -|Enlace directo|FastEthernet 0/0 (p. 1)|
|**10.0.12.0**|/30|**C**|- / -|Enlace directo|Serial 2/0 (p. 1)|
|**192.168.20.0**|/24|**R**|**120 / 1**|`10.0.12.2` (p. 1)|Serial 2/0|
|**10.0.23.0**|/30|**R**|**120 / 1**|`10.0.12.2` (p. 1)|Serial 2/0|
|**192.168.30.0**|/24|**R**|**120 / 2**|`10.0.12.2` (p. 1)|Serial 2/0|
|**10.0.34.0**|/30|**R**|**120 / 2**|`10.0.12.2` (p. 1)|Serial 2/0|
|**192.168.40.0**|/24|**R**|**120 / 3**|`10.0.12.2` (p. 1)|Serial 2/0|



Tarea 2: Respuestas a las Preguntas Adicionales

1. **¿Cuántos saltos hay desde RT1 hasta la red 192.168.40.0/24?** (p. 2)
    - **Respuesta:** Hay **3 saltos** (métrica RIP = 3) (p. 2). El paquete debe atravesar RT2, luego RT3 y finalmente RT4 para alcanzar esa red LAN de destino (p. 1).
2. **Si la interfaz Se2/0 de RT2 falla, ¿a qué redes perdería acceso RT1?** (p. 2)
    - **Respuesta:** RT1 perdería acceso a **todas las redes remotas de la topología**, es decir: `192.168.20.0/24`, `10.0.23.0/30`, `192.168.30.0/24`, `10.0.34.0/30` y `192.168.40.0/24` (p. 2). Esto se debe a que la topología es completamente lineal y el único camino de salida de RT1 es a través de ese enlace hacia RT2 (p. 1).
3. **Camino que seguiría un paquete desde 192.168.10.5 hasta 192.168.40.10:** (p. 2)
    - **Respuesta:** El flujo físico exacto del paquete es:  
        `PC (LAN1) ➔ RT1 (Fa0/0) ➔ RT1 (Se2/0) ➔ RT2 (Se2/0) ➔ RT2 (Se3/0) ➔ RT3 (Se2/0) ➔ RT3 (Se3/0) ➔ RT4 (Se2/0) ➔ RT4 (Fa0/0) ➔ PC (LAN4)` (p. 1).



Tarea 3: Implementación en Cisco Packet Tracer

Aplica paso a paso estos bloques de comandos en la pestaña **CLI** de cada router para implementar la lógica dinámica requerida (p. 3):

1. Configuración del Router RT1

```
Router> enable
Router# configure terminal
Router(config)# hostname RT1

! Configuración del protocolo de enrutamiento RIPv2
RT1(config)# router rip
RT1(config-router)# version 2
RT1(config-router)# network 192.168.10.0
RT1(config-router)# network 10.0.12.0
RT1(config-router)# no auto-summary
RT1(config-router)# passive-interface FastEthernet 0/0
RT1(config-router)# end
RT1# write memory
```


2. Configuración del Router RT2

```
Router> enable
Router# configure terminal
Router(config)# hostname RT2

RT2(config)# router rip
RT2(config-router)# version 2
RT2(config-router)# network 192.168.20.0
RT2(config-router)# network 10.0.12.0
RT2(config-router)# network 10.0.23.0
RT2(config-router)# no auto-summary
RT2(config-router)# passive-interface FastEthernet 0/0
RT2(config-router)# end
RT2# write memory
```


3. Configuración del Router RT3
```
Router> enable
Router# configure terminal
Router(config)# hostname RT3

RT3(config)# router rip
RT3(config-router)# version 2
RT3(config-router)# network 192.168.30.0
RT3(config-router)# network 10.0.23.0
RT3(config-router)# network 10.0.34.0
RT3(config-router)# no auto-summary
RT3(config-router)# passive-interface FastEthernet 0/0
RT3(config-router)# end
RT3# write memory
```


4. Configuración del Router RT4

```
Router> enable
Router# configure terminal
Router(config)# hostname RT4

RT4(config)# router rip
RT4(config-router)# version 2
RT4(config-router)# network 192.168.40.0
RT4(config-router)# network 10.0.34.0
RT4(config-router)# no auto-summary
RT4(config-router)# passive-interface FastEthernet 0/0
RT4(config-router)# end
RT4# write memory

```



Tarea 4: Validación en Packet Tracer

1. Espera aproximadamente **30 o 60 segundos** en el simulador para permitir que los routers intercambien de forma completa sus tablas RIP actualizadas.
2. Accede al modo privilegiado de **RT1** y ejecuta el comando de auditoría (p. 4)

```
RT1# show ip route
```


1. Verifica que en tu pantalla aparezcan las rutas marcadas con la letra **R** y que los valores coincidan exactamente con la tabla que completamos en la Tarea 1 (pp. 2, 4).