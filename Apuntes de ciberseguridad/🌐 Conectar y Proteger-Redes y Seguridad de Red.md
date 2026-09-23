## 1. Introducción y estructura del curso

Objetivo: comprender la **arquitectura de red**, las **operaciones de red**, las **tácticas de intrusión**, los **protocolos**, los **cortafuegos**, las **VPN** y las prácticas de **hardening** (endurecimiento de seguridad).

### Módulos del curso

1. **Arquitectura de red** — conceptos básicos, amenazas y mecanismos de protección. _(en curso)_
2. **Operaciones de red** — protocolos de red, vulnerabilidades en la comunicación, cortafuegos.
3. **Protección contra intrusiones en la red** — tipos de ataques, detección y cierre de vulnerabilidades.
4. **Endurecimiento de seguridad (hardening)** — refuerzo de sistemas y desafíos en la nube.

---

## Módulo 1: Arquitectura de red

### ¿Qué es una red?

Grupo de dispositivos conectados que pueden comunicarse y compartir información o recursos (computadoras, celulares, impresoras, servidores, dispositivos IoT).

- **Dirección IP**: identifica lógicamente a un dispositivo dentro de una red.
- **Dirección MAC**: identificador físico único del hardware de red.

### Tipos de redes

- **[[LAN]]** (Local Area Network): área pequeña (casa, escuela, oficina). Ej. un celular conectado al WiFi de casa.
- **[[WAN]]** (Wide Area Network): área geográfica extensa (ciudad, país, el mundo). Internet es el ejemplo más común.

### Habilidades útiles para la seguridad de redes (perspectiva de Emmanuel, Ingeniero de Seguridad Ofensiva en Google)

- **Seguridad ofensiva**: simular el comportamiento de atacantes para encontrar vulnerabilidades antes que ellos.
- Habilidades técnicas clave:
    - Programación
    - Seguridad de plataformas y sistemas operativos
    - **Línea de comandos** (acceso desde el kernel hasta aplicaciones)
    - **Análisis de logs/registros** (detectar errores y comportamientos anómalos)
    - **Análisis de tráfico de red** (detectar tráfico sospechoso, datos sin cifrar, firewalls mal configurados)
- Habilidad blanda clave: **comunicación efectiva** con equipos de desarrollo y negocio.
- Consejo: mantener una actitud de **aprendizaje constante**.

### Herramientas de red

|Dispositivo|Función|
|---|---|
|**Concentrador (Hub)**|Envía la información a **todos** los dispositivos conectados. Menos eficiente y menos seguro (como una torre de radio).|
|**Conmutador (Switch)**|Envía la información solo al destinatario correcto (usa tabla de direcciones MAC). Opera en la capa de enlace de datos del modelo TCP/IP.|
|**[[Router]]**|Conecta redes distintas entre sí; dirige tráfico según dirección IP (capa de red del TCP/IP); muchos incluyen firewall integrado.|
|**Módem**|Conecta la red local con Internet a través del ISP (líneas telefónicas, cable coaxial, fibra óptica).|

**Flujo típico**: dispositivo → router (analiza dirección de destino) → módem → Internet → módem del destino → router del destino → dispositivo final.

### Componentes y dispositivos de red

- **Dispositivos de red**: almacenan información y ofrecen servicios; envían/reciben **paquetes de datos** (con dirección de origen y destino).
- **Ordenadores/dispositivos de escritorio**: tienen dirección MAC e IP únicas; se conectan por Ethernet o inalámbricamente.
- **[[Cortafuegos]] (Firewall)**: supervisa el tráfico entrante/saliente; primera línea de defensa; bloquea/permite tráfico según reglas; se sitúa entre la red interna y redes externas no confiables. _No es la única medida de protección._
- **Servidores**: ofrecen información/servicios a **clientes** (modelo cliente-servidor).
    - Servidores DNS (traducen dominios a IP)
    - Servidores de archivos
    - Servidores de correo electrónico
- **Concentradores y conmutadores**: dirigen tráfico en la red local (switch es más seguro y eficiente que hub).
- **Routers**: conectan redes distintas; analizan cabecera IP; pueden incluir firewall integrado.
- **Módems y puntos de acceso inalámbricos**:
    - El módem conecta la red con el ISP.
    - Un **punto de acceso inalámbrico** crea redes Wi-Fi (conjunto de estándares para comunicación inalámbrica).

### Diagramas de red en ciberseguridad

- Son "mapas" que muestran los dispositivos de una red y sus conexiones (routers, switches, servidores, computadoras), usando símbolos gráficos y líneas.
- Ayudan a analistas y administradores a **visualizar la arquitectura**, identificar vulnerabilidades y diseñar estrategias de protección.

---

## 🧠 Ideas clave para repasar (hasta ahora)

- [ ] Diferencia entre dirección IP y dirección MAC
- [ ] Diferencia entre LAN y WAN
- [ ] Diferencia entre hub, switch y router
- [ ] Función del módem vs. el router
- [ ] Qué es el modelo cliente-servidor
- [ ] Para qué sirven los diagramas de red en ciberseguridad

## 📌 Pendiente de completar

- [ ] Módulo 2: Operaciones de red (protocolos, cortafuegos)
- [ ] Módulo 3: Protección contra intrusiones en la red
- [ ] Módulo 4: Endurecimiento de seguridad (hardening) y nube