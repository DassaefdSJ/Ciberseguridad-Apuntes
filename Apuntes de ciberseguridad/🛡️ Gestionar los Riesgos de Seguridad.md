## 1. Introducción al curso

Temas centrales: definición de seguridad y responsabilidades del analista, habilidades necesarias, eventos históricos (LoveLetter, Morris), marcos y controles, la tríada [[CID (CIA)]], los [[8 dominios CISSP]], el [[NIST RMF]], auditorías internas y herramientas básicas de seguridad.

## 2-3. Los ocho dominios de seguridad CISSP (detalle)

1. **Gestión de Seguridad y Riesgos**: metas de seguridad, mitigación de riesgos, cumplimiento normativo, continuidad del negocio, regulaciones legales.
2. **Seguridad de los Activos**: almacenamiento, mantenimiento, retención y destrucción segura de datos (PII/SPII); control de acceso.
3. **Arquitectura de Seguridad e Ingeniería**: responsabilidad compartida; políticas que fomentan la notificación de problemas.
4. **Seguridad de las Comunicaciones y Redes**: redes seguras, gestión de conexiones inseguras (Bluetooth, Wi-Fi público).
5. **Gestión de Identidad y Acceso (IAM)**: identificación, autenticación, autorización, responsabilidad (logs de acceso).
6. **Evaluación y Pruebas de Seguridad**: pruebas de controles, análisis continuo, implementación de nuevos controles (ej. MFA).
7. **Operaciones de Seguridad**: investigación de incidentes, mitigación de ataques activos, forense digital.
8. **Seguridad del Desarrollo de Software**: seguridad integrada en todo el ciclo de vida (diseño, código, pen testing).

## 4. Resumen de los ocho dominios (síntesis)

- **Seguridad y gestión de riesgos** → incluye InfoSec (respuesta a incidentes, gestión de vulnerabilidades).
- **Seguridad de los recursos** → análisis de impacto y recuperación.
- **Arquitectura e ingeniería** → principios: responsabilidad compartida, mínimo privilegio, defensa en profundidad, fallar con seguridad, separación de funciones, confianza cero.
- **Comunicación y seguridad de red** → clave en entornos híbridos/remotos.
- **IAM** → principio de privilegio mínimo.
- **Evaluación y pruebas** → auditorías de sistemas.
- **Operaciones** → detección de intrusiones, forense, lecciones aprendidas.
- **Desarrollo de software seguro** → desde diseño hasta publicación.

## 5. Amenazas, riesgos y vulnerabilidades

- **Amenaza**: circunstancia/evento que puede afectar negativamente un activo (ej. ingeniería social, phishing).
- **Riesgo**: probabilidad de que una amenaza ocurra; afecta confidencialidad, integridad o disponibilidad.
    - **Bajo**: info pública, sin daño reputacional/financiero.
    - **Medio**: info no pública, daño moderado si se filtra.
    - **Alto**: info regulada (PII/SPII), impacto severo.
- **Vulnerabilidad**: debilidad explotable por una amenaza (firewall obsoleto, software sin actualizar, contraseñas débiles, personas).
- Riesgo = amenaza + vulnerabilidad.

## 6. Impactos clave

### Ransomware

Cifra datos y exige pago por la clave de descifrado; negociaciones suelen ocurrir en la [[dark web]].

### Capas de la web

- **Superficial**: accesible por navegadores comunes.
- **Profunda**: requiere autorización (ej. intranets).
- **Oscura**: acceso con software especial; asociada a actividad delictiva.

### Tres impactos principales

1. **Financiero** (interrupciones, costos de recuperación, sanciones)
2. **Robo de identidad** (venta/filtración de PII)
3. **Daño a la reputación** (pérdida de confianza del cliente)

## 7. Gestionar amenazas, riesgos y vulnerabilidades (caso práctico)

- Amenaza frecuente: configuraciones erróneas o exceso de privilegios (ej. permisos OAuth de un proveedor).
- Sistemas sin parches = riesgo constante.
- La colaboración entre equipos es clave para mitigar riesgos.

## 8. Marco de Gestión de Riesgos del NIST (RMF) — 7 pasos

1. **Preparar**: identificar y monitorear riesgos, controles preventivos.
2. **Categorizar**: evaluar impacto en CID.
3. **Seleccionar**: elegir y documentar controles (ej. playbooks).
4. **Implementar**: poner en marcha planes (ej. políticas de contraseñas).
5. **Evaluar**: verificar que los controles funcionen.
6. **Autorizar**: asumir responsabilidad, generar reportes.
7. **Monitorear**: supervisión continua y ajustes.

## 9. Gestionar amenazas, riesgos y vulnerabilidades comunes

### Estrategias de gestión de riesgos

- **Aceptación**: asumir el riesgo.
- **Evitación**: evitarlo por completo.
- **Transferencia**: delegarlo a terceros.
- **Mitigación**: reducir su impacto.
- Marcos usados: [[NIST RMF]], HITRUST.

### Amenazas comunes

- Amenazas internas (abuso de accesos autorizados).
- [[APT]] (acceso no autorizado prolongado).

### Factores de riesgo

Externos, internos, sistemas heredados, riesgos multiparte (proveedores), cumplimiento/licencias.

### Vulnerabilidades recientes (ejemplos)

- **ProxyLogon** (Microsoft Exchange)
- **ZeroLogon** (protocolo Netlogon)
- **Log4Shell** (ejecución remota de código Java)
- **PetitPotam** (manipulación de autenticación NTLM)
- Fallos de registro/monitoreo
- Falsificación de peticiones del lado del servidor (SSRF)

> Referencia: **OWASP Top 10** (2017 → 2021 añadió: diseño inseguro, fallos de integridad de software/datos, SSRF).

## 10. Marcos de Seguridad en las Organizaciones

- El **factor humano** es la mayor amenaza → los marcos también sirven para educar y concienciar al personal.
- Marcos orientan **prevención, detección y respuesta**.
- Rol del analista: comprender e implementar los planes de seguridad existentes.

## 11. Controles de Seguridad

Tres controles comunes:

1. **Cifrado**: texto plano → texto cifrado; protege confidencialidad (ej. números de seguridad social).
2. **Autenticación**: verifica identidad (básica: usuario/contraseña; avanzada: MFA con biometría).
3. **Autorización**: determina el nivel de acceso permitido.

Estos controles se relacionan directamente con la [[CID (CIA)|tríada CID]].

## 12. Relación entre Marcos y Controles

- **Marco de Ciberamenazas (CTF)**: gobierno de EE. UU.; lenguaje común para describir ciberamenazas.
- **ISO/IEC 27001**: estándar internacional para gestión de seguridad de la información (SGSI); controles opcionales.

### Tipos de controles de seguridad

- **Físicos**: puertas, vallas, CCTV, guardias, tarjetas de acceso.
- **Técnicos**: firewalls, MFA, antivirus.
- **Administrativos**: separación de funciones, autorización, clasificación de activos.

## 13-14. Tríada CID

- **Confidencialidad**: acceso solo a usuarios autorizados; principio de privilegio mínimo.
- **Integridad**: datos correctos y confiables; protocolos de verificación, firmas, sumas de verificación, cifrado.
- **Disponibilidad**: datos accesibles cuando se necesitan, respetando niveles de acceso.

**Ejemplo (banco)**: confidencialidad de datos financieros, integridad ante cambios sospechosos de gasto, disponibilidad de banca en línea.

## 15-16. Marcos del NIST

### NIST CSF (voluntario)

5 funciones:

1. **Identificar** – activos, sistemas, riesgos.
2. **Proteger** – medidas de protección.
3. **Detectar** – supervisión de incidentes.
4. **Responder** – contener el daño.
5. **Recuperar** – restaurar servicios.

**Ejemplo práctico**: alerta de estación comprometida → identificar → proteger (bloquear dispositivo) → detectar más actividad → responder (investigar origen) → recuperar (restaurar archivos).

### NIST SP 800-53

Controles de seguridad unificados para sistemas del gobierno federal de EE. UU. (y proveedores privados); mantiene la tríada CID.

## Principios de seguridad OWASP

1. **Minimizar la superficie de ataque**
2. **Principio de menor privilegio**
3. **Defensa en profundidad**
4. **Separación de funciones**
5. **Mantener la seguridad simple**
6. **Corregir problemas de seguridad correctamente** (causa raíz)
7. **Valores predeterminados seguros** (Secure Defaults)
8. **Fallar con seguridad** (Fail Securely)
9. **No confiar en servicios externos**
10. **Evitar la seguridad por oscuridad**

## 17-19. Auditorías de Seguridad

### Planificación

- **Alcance y objetivos**: personas, activos, políticas, tecnologías involucradas.
- **Evaluación de riesgos**: identificar amenazas/vulnerabilidades sobre activos.

### Completar la auditoría

1. **Evaluación de controles** (administrativos, técnicos, físicos)
2. **Evaluación de cumplimiento** (GDPR, PCI DSS, etc.)
3. **Comunicación de resultados** (riesgos, regulaciones, recomendaciones)

### Tipos de controles (por función)

- **Preventivos**: firewalls, políticas de contraseñas, separación de funciones.
- **Correctivos**: planes de recuperación ante desastres, antivirus, backups.
- **Detectivos**: IDS, CCTV.
- **Disuasorios**: iluminación, alarmas, cerraduras.

### Checklist de auditoría

Alcance → evaluación de políticas → evaluación de riesgos → plan de mitigación → comunicación de resultados.

## 20-22. Registros y herramientas [[SIEM]]

### Fuentes de logs

- **Firewall logs**: conexiones entrantes/salientes.
- **Network logs**: dispositivos en la red.
- **Server logs**: eventos de servicios (login, correo, archivos).

### Función de SIEM

Recopila y analiza logs, ofrece monitoreo en tiempo real, alertas automatizadas y **dashboards** visuales (gráficos, métricas de tiempo de respuesta, disponibilidad, tasa de fallos).

### Futuro de SIEM

- Migración a **nube** (cloud-hosted, cloud-native).
- Adaptación al crecimiento de IoT.
- Uso de IA/ML para detección de amenazas.
- **SOAR** (Security Orchestration, Automation and Response): automatiza respuestas sin intervención humana.
- Mayor interoperabilidad entre plataformas.

## 23. Accesibilidad y Seguridad (perspectiva de Parisa, VP de Ingeniería, Chrome)

- La seguridad debe diseñarse pensando en la accesibilidad (ej. no depender solo del color rojo para advertencias, por daltonismo).
- Soluciones inclusivas (ej. subtitulado cerrado) terminan beneficiando a todos los usuarios.
- Importancia de la investigación de usuarios y la diversidad de habilidades al probar mitigaciones de seguridad.

## 24-25. Herramientas SIEM y de ciberseguridad

### Tipos de despliegue SIEM

- **Self-hosted**: infraestructura propia, mayor control.
- **Cloud-hosted**: gestionado por el proveedor.
- **Híbrido**: combina ambos.

### Ejemplos

- **Splunk Enterprise** (self-hosted) / **Splunk Cloud**
- **Chronicle (Google SecOps)** (nativo de la nube)

### Código abierto vs. propietario

- **Abierto**: gratuito, personalizable, colaborativo (ej. Linux, Suricata).
- **Propietario**: soporte oficial, licencia de pago (ej. Splunk®, Chronicle).
- Mito: código abierto no es menos seguro; la revisión comunitaria ayuda a corregir vulnerabilidades rápido.

## 26. Mitos sobre ciberseguridad (perspectiva de Talya, Google)

1. No es necesario saber programar o hackear.
2. No se requiere ser genio en matemáticas.
3. No se requiere un título específico en ciberseguridad.
4. No se trabaja de forma aislada; hay colaboración constante.

## 27. Paneles de Splunk y Chronicle

### Splunk

- Panel de postura de seguridad (eventos 24h)
- Panel de resumen ejecutivo
- Panel de revisión de incidentes
- Panel de análisis de riesgos

### Chronicle

- Estadísticas empresariales (alertas, dominios sospechosos)
- Ingestión de datos y salud
- Coincidencias COI (indicadores de compromiso)
- Panel principal
- Detecciones de reglas
- Inicio de sesión de usuario

## 28-31. Playbooks (Manuales de Estrategias) y respuesta a incidentes

### 6 fases del playbook de respuesta a incidentes

1. **Preparación**: documentar procedimientos, roles, capacitación.
2. **Detección y análisis**: identificar y evaluar magnitud del incidente.
3. **Contención**: prevenir daños adicionales.
4. **Erradicación y recuperación**: eliminar artefactos, restaurar sistemas.
5. **Actividad posterior al incidente**: documentar, informar, aplicar lecciones.
6. **Coordinación**: reportar y compartir información.

### Tipos de playbooks

- Respuesta a incidentes
- Respuesta a vulnerabilidades
- Específicos por amenaza (ransomware, vishing, BEC)
- Adaptados a normativas locales

### Integración con SIEM

SIEM detecta → analista consulta playbook → evaluación/contención/erradicación/recuperación → actualización del playbook con lecciones aprendidas.

> Los playbooks son **documentos vivos**, deben actualizarse constantemente.

## 32. Diversidad de perspectivas en equipos de seguridad (Erin, Google)

- La diversidad de experiencias (periodismo, entretenimiento, etc.) ayuda a anticipar riesgos que una sola perspectiva no vería.
- Mejora la equidad y la inclusión en el diseño de productos seguros.

## 33. Playbooks + SIEM + [[SOAR]]

- **SIEM** detecta comportamiento inusual → el playbook indica cómo actuar.
- **SOAR** automatiza tareas repetitivas (ej. bloquear cuenta tras múltiples intentos fallidos) antes de que el analista intervenga con el playbook.
- Los playbooks (o _runbooks_) especifican **quién** hace **qué** y **cuándo**.

---

## 🧠 Ideas clave para repasar

- [ ] Diferencia entre amenaza, riesgo y vulnerabilidad
- [ ] Los 7 pasos del NIST RMF
- [ ] Las 5 funciones del NIST CSF (Identificar-Proteger-Detectar-Responder-Recuperar)
- [ ] Diferencia entre controles físicos, técnicos y administrativos
- [ ] Diferencia entre preventivo, correctivo, detectivo y disuasorio
- [ ] Las 6 fases de un playbook de respuesta a incidentes
- [ ] Diferencia entre SIEM y SOAR
- [ ] Capas de la web (superficial, profunda, oscura)

## 📚 Referencias del curso

- [Play It Safe: Manage Security Risks](https://www.coursera.org/learn/manage-security-risks?specialization=googlecybersecurity)
- [Foundations of Cybersecurity](https://www.coursera.org/learn/foundations-of-cybersecurity)
- [Assets, Threats, and Vulnerabilities](https://www.coursera.org/learn/assets-threats-and-vulnerabilities)
- [Sound the Alarm: Detection and Response](https://www.coursera.org/learn/sound-the-alarm-detection-and-response)
- [Put It to Work: Prepare for Cybersecurity Jobs](https://www.coursera.org/learn/prepare-for-cybersecurity-jobs)