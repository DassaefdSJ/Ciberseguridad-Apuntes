
## 1. Términos y conceptos clave

- **[[Cumplimiento normativo]]**: estándares internos y regulaciones externas que evitan multas y violaciones de seguridad.
- **[[Marcos de seguridad]]**: directrices para elaborar planes que mitiguen riesgos a datos y privacidad.
- **[[Controles de seguridad]]**: medidas diseñadas para reducir riesgos específicos.
- **Postura de seguridad**: capacidad de una organización para defender activos y reaccionar a cambios; a mayor fortaleza, menor riesgo.
- **Agente de amenaza**: persona o grupo que representa un riesgo (redes, apps, datos).
- **Amenaza interna**: empleado, ex empleado, proveedor o socio que representa un riesgo (a veces accidental).
- **Seguridad de red**: proteger la infraestructura de red contra accesos no autorizados.
- **Seguridad de la nube**: garantizar configuración correcta y acceso limitado a activos en la nube.
- **Programación**: automatizar tareas repetitivas, revisar tráfico web, alertar actividades sospechosas.

## 2. Competencias básicas del analista

- **Comunicación**: explicar riesgos a públicos técnicos y no técnicos.
- **Colaboración**: reconocer patrones de ataque y resolver problemas proactivamente.
- **Gestión del tiempo**: priorizar para minimizar daños.
- **Habilidades técnicas**:
    - Programación (Python, SQL)
    - [[SIEM]] (gestión de información y eventos de seguridad)
    - Informática forense
    - [[IDS]] (sistemas de detección de intrusiones)

## 3. Importancia de la ciberseguridad

- Protege la continuidad del negocio y la integridad ética de la organización.
- Datos sensibles a proteger:
    - **PII** (información personal identificable): nombre, fecha de nacimiento, dirección, correo, IP.
    - **SPII** (PII sensible): seguridad social, datos médicos/financieros, biométricos.
- El robo de PII/SPII puede derivar en **robo de identidad**.
- Se proyecta un crecimiento del sector >30% para 2030 (BLS, EE. UU.).

## 4. Ataques comunes

### 4.1 Phishing

- **BEC** (compromiso de correo empresarial)
- **Spear phishing** (dirigido a un usuario/grupo específico)
- **Whaling** (dirigido a ejecutivos)
- **Vishing** (por voz)
- **Smishing** (por SMS)

### 4.2 Software malicioso

- **Virus** (requiere acción del usuario)
- **Gusanos** (se propagan solos)
- **[[Ransomware]]** (encripta datos y exige pago)
- **Software espía** (recopila/vende información sin consentimiento)

### 4.3 Ingeniería social

- Phishing en redes sociales
- Ataque de "agujero de agua" (watering hole)
- USB baiting
- Ingeniería social física
- Tácticas: autoridad, intimidación, prueba social, escasez, confianza, urgencia.

## 5-6. Los ocho dominios de seguridad CISSP

1. Seguridad y gestión de riesgos
2. Seguridad de los recursos
3. Arquitectura e ingeniería de seguridad
4. Seguridad de la red y las comunicaciones
5. Gestión de identidades y accesos
6. Evaluación y pruebas de seguridad
7. Operaciones de seguridad
8. Seguridad del desarrollo de software

## 7. Tipos de ataque

- Descifrado de contraseñas (fuerza bruta, tablas rainbow)
- Ingeniería social
- Físico (USB, clonación de tarjetas, robo de dispositivos)
- IA antagónica
- Cadena de suministro
- Criptográfico (cumpleaños, colisión, degradación)

## 8. Actores de amenaza

|Tipo|Características|Motivación|
|---|---|---|
|**[[APT]]** (Amenaza Persistente Avanzada)|Organizados, respaldados por estados, evaden detección por mucho tiempo|Sabotaje, espionaje|
|**Amenazas internas**|Acceso ya autorizado, difíciles de detectar|Sabotaje, corrupción, venganza|
|**Hacktivistas**|Motivación ideológica; DDoS, filtraciones, defacement|Protesta, propaganda, cambio social|
|**White Hat**|Hackers éticos, legales|Mejorar seguridad|
|**Gray Hat**|No siempre reportan hallazgos|Demostrar fallos|
|**Black Hat**|Delincuentes informáticos|Dinero, daño, robo de datos|
|**Script Kiddies**|Usan herramientas de otros sin entenderlas|Variable|
|**Mercenarios**|Contratados|Dinero|
|**Vigilantes**|"Justicieros" digitales|Exponer criminales|

## 9-10. Marcos y diseño seguro

### Componentes de un marco de seguridad

1. Identificar y documentar objetivos (ej. cumplir GDPR)
2. Establecer directrices
3. Implementar procesos
4. Monitorear y comunicar resultados

### Tríada CIA (CID)

- **Confidencialidad**: acceso solo a usuarios autorizados (cifrado, autenticación).
- **Integridad**: datos correctos y confiables (encriptación, anti-manipulación).
- **Disponibilidad**: acceso garantizado (respaldos, redundancia, anti-DDoS).

### [[NIST CSF]] — Marco de Ciberseguridad del NIST

1. Identificar
2. Proteger
3. Detectar
4. Responder
5. Recuperarse

## 11. Controles, marcos y cumplimiento

- **Marcos y estándares**: NIST CSF, NIST RMF, CIS Controls, ISO.
- **Regulaciones principales**:
    - **GDPR** – datos de ciudadanos UE
    - **PCI DSS** – tarjetas de crédito
    - **HIPAA** – datos médicos (EE. UU.)
    - **FedRAMP** – nube gubernamental
    - **FERC-NERC** – infraestructura eléctrica
    - **SOC 1 / SOC 2** – auditorías organizacionales
- **Orden Ejecutiva 14028** (2021, EE. UU.): refuerza ciberseguridad en infraestructuras críticas.

## 12-13. Ética en ciberseguridad

- **Imparcialidad y confidencialidad**: actuar igual sin importar relaciones personales.
- **Uso responsable de accesos privilegiados**: no abusar del acceso (ej. no auto-otorgarse beneficios).
- **Principios éticos**:
    - Confidencialidad
    - Protección de la privacidad
    - Cumplimiento de la ley
- **Contraataques**:
    - EE. UU.: prohibidos para civiles (solo gobierno/militares).
    - Internacional: permitidos en algunos países si son proporcionados, aunque poco recomendados.

## 14-15. Herramientas para operaciones B2B

- **[[SIEM]]**: recopila/analiza logs, genera alertas, on-premise o en la nube.
- **Analizadores de protocolos de red (Packet Sniffers)**: capturan tráfico para detectar anomalías.
- **Playbooks**:
    - Cadena de custodia
    - Protección y preservación de evidencias
- **Programación**: Python (automatización), SQL (bases de datos).
- **Sistemas operativos**: Linux, macOS, Windows; CLI para administración.
- **Vulnerabilidades web**: ver [[OWASP Top 10]].
- **Software antivirus**: detecta y elimina malware.
- **[[IDS]]**: monitorea actividad y alerta intrusiones.
- **Encriptación**: convierte texto plano en cifrado (distinto de codificación).
- **Pruebas de penetración (Pen Testing)**: simulan ataques para hallar vulnerabilidades.

---

## 🧠 Ideas clave para repasar

- [ ] Diferencia entre PII y SPII
- [ ] Los 4 componentes de un marco de seguridad
- [ ] Los 8 dominios del CISSP
- [ ] Diferencia entre virus, gusano y ransomware
- [ ] Tríada CIA y sus implementaciones
- [ ] Diferencia entre White/Gray/Black Hat