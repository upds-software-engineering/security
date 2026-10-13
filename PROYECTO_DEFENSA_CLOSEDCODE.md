# PROYECTO DE DEFENSA: SISTEMAS INFORMÁTICOS Y SEGURIDAD INTEGRAL
**Grupo:** ClosedCode  
**Fecha de Entrega y Defensa:** 14 de Octubre de 2026  
**Modalidad de Defensa:** Exposición Continua y Coordinada (Secuencial sin sorteo)  
**Herramienta Oficial de Diagramación:** Draw.io (Exportación en SVG / PNG de alta resolución)

---

## ÍNDICE GENERAL DEL PROYECTO
- [1. CASO DE ESTUDIO BASE: "AGRO-INDUSTRIAL CORPORATION (AIC S.A.)"](#1-caso-de-estudio-base-agro-industrial-corporation-aic-sa)
- [2. LINEAMIENTOS Y CRITERIOS DE CALIDAD TÉCNICA](#2-lineamientos-y-criterios-de-calidad-técnica)
- [3. ESPECIFICACIÓN DE ENTREGABLES Y DIAGRAMAS DRAW.IO](#3-especificación-de-entregables-y-diagramas-drawio)
- [4. REPARTO DETALLADO, GUIONES Y CASOS PRÁCTICOS POR INTEGRANTE](#4-reparto-detallado-guiones-y-casos-prácticos-por-integrante)
  - [Módulo 1: El Sistema Informático — Luis Rocha Vela](#módulo-1-el-sistema-informático--luis-rocha-vela)
  - [Módulo 2: Seguridad Física y Recursos — Jhoel Alvaro Cruz Zurita](#módulo-2-seguridad-física-y-recursos--jhoel-alvaro-cruz-zurita)
  - [Módulo 3: Seguridad de Red y Perímetro — Freddy Emmanuel Ponce Quiroga](#módulo-3-seguridad-de-red-y-perímetro--freddy-emmanuel-ponce-quiroga)
  - [Módulo 4: Seguridad de Servicios, Identidad y Usuarios — Eliazar Russeu Campos Vistas](#módulo-4-seguridad-de-servicios-identidad-y-usuarios--eliazar-russeu-campos-vistas)
  - [Módulo 5: Seguridad de Contenidos y Criptografía — Carlos Andre Soruco Paz](#módulo-5-seguridad-de-contenidos-y-criptografía--carlos-andre-soruco-paz)
- [5. GUION DE TRANSICIONES ENTRE EXPOSITORES](#5-guion-de-transiciones-entre-expositores)
- [6. CRONOGRAMA DE PREPARACIÓN (13 Y 14 DE OCTUBRE)](#6-cronograma-de-preparación-13-y-14-de-octubre)

---

## 1. CASO DE ESTUDIO BASE ÚNICO: EQUIFAX INC. (DATA BREACH & INFRAESTRUCTURA)

Para que el proyecto se base en **un único caso de estudio integral que cubra el 100% del temario**, tomamos el incidente corporativo más auditado y documentado por el gobierno de los Estados Unidos: **La Brecha de Seguridad y Arquitectura de Equifax (2017)**.

### Enlaces Oficiales al Caso de Estudio Completo (Documentación de Acceso Público):
1. **Reporte Oficial del Congreso de EE.UU. (Comité de Supervisión de la Cámara de Representantes):**
   - **Documento:** *The Equifax Data Breach: Majority Staff Report (115th Congress)*
   - **Enlace Oficial (GovInfo / GPO):** [The Equifax Data Breach Report en GovInfo](https://www.govinfo.gov/app/details/GOVPUB-Y4_G74_7-PURL-gpo191321)
   - **Descarga directa PDF:** [Equifax-Majority-Staff-Report.pdf](https://oversight.house.gov/wp-content/uploads/2018/12/Equifax-Report.pdf)
2. **Reporte Oficial del GAO (U.S. Government Accountability Office):**
   - **Documento:** *GAO-18-559: DATA PROTECTION - Actions Taken by Equifax and Federal Agencies*
   - **Enlace Oficial:** [GAO-18-559 Report Page](https://www.gao.gov/products/gao-18-559)

---

### Mapeo Exhaustivo: Cómo el Caso Equifax Cubre el 100% del Temario

El reporte oficial de más de 100 páginas analiza la infraestructura completa de Equifax y expone con nombres técnicos cada falla que coincide exactamente con los puntos de nuestro proyecto:

| Módulo del Temario | Conceptos Exigidos | Cómo se Evidencia en el Caso Real de Equifax |
| :--- | :--- | :--- |
| **1. El Sistema Informático** | Infraestructura, recursos de usuario/servicio/comunicación, servicios locales, remotos e híbridos. | Equifax operaba una infraestructura híbrida masiva: data centers centrales legados, servidores de disputa de crédito expuestos a internet (Apache Struts) conectados a bases de datos relacionales centrales (Sun/Solaris, Oracle, SQL) y servicios cloud para analítica crediticia. |
| **2. Seguridad Física y Perimetral** | Seguridad física, Data Center, climatización, recursos de red, IoT/periféricos. | El reporte detalla la sala de servidores y clusters de almacenamiento. Se analiza el control de activos físicos (*Asset Management*) y la falta de inventario que permitió que servidores físicos estuvieran desactualizados sin que nadie supiera quién era el dueño del hardware. |
| **2.4. Seguridad de la Red** | Segmentación (VLANs), Cortafuegos, DMZ, IDS/IPS, VPN. | **El fallo central:** El portal público estaba en la DMZ. Sin embargo, **la red interna no estaba segmentada**. Una vez que los atacantes vulneraron el servidor web en la DMZ, pudieron moverse libremente hacia la red interna (*lateral movement*) y consultar 48 bases de datos distintas porque no había firewalls internos ni aislamiento por VLANs. |
| **3. Seguridad de Servicios y Usuarios** | Tríada CIA, Autenticación, Autorización (RBAC), IAM. | **Pérdida absoluta de Confidencialidad e Integridad:** Los atacantes usaron consultas no autorizadas ejecutadas con las credenciales de servicio del servidor web. Equifax no aplicaba el principio de menor privilegio ni autenticación multifactor (MFA) entre servidores internos. |
| **3.4. Seguridad de Contenidos** | Cifrado, Firma Digital y **Esteganografía / Canales Ocultos**. | **1. Cifrado:** Los datos personales en reposo en las tablas de base de datos **no estaban cifrados**.<br>**2. Firma Digital / Certificados:** Equifax tenía un dispositivo de inspección profunda de tráfico para descifrar y auditar la red, pero **su certificado digital SSL estaba vencido desde hacía 9 meses**. Por eso el monitor estuvo "ciego" durante 76 días.<br>**3. Canales Encubiertos / Esteganografía:** Los atacantes exfiltraron gigabytes de datos empaquetándolos y camuflándolos a través de canales HTTPS encubiertos en pequeños lotes para no disparar alertas de tráfico anómalo. |

---

### Adaptación Anonimizada para la Defensa: "Enterprise Core S.A."
Para cumplir con la directiva de anonimización en nuestra presentación, tomamos toda la lección técnica y arquitectura real de Equifax y la presentamos bajo el nombre de **Enterprise Core S.A.** (una corporación que gestiona datos críticos, despachos transaccionales y servicios distribuidos), explicando cómo el diseño propuesto por el Grupo ClosedCode corrige y blinda cada una de las vulnerabilidades documentadas en la investigación del Congreso.
* **Giro de negocio:** Complejo agroindustrial y logístico con procesamiento en planta, balanzas de pesaje continuo, flota de transporte, oficinas administrativas centrales y enlace con sedes remotas.
* **Topología de Sedes:**
  1. **Sede Central (HQ / Edificio Administrativo):** Data Center principal, servidores ERP, base de datos centralizada, áreas de Finanzas, Recursos Humanos, Sistemas/Helpdesk y Dirección.
  2. **Planta Industrial / Básculas de Pesaje:** Entorno mixto IT/OT. Computadoras de despacho, básculas de camiones conectadas por convertidores serial-Ethernet, PLCs de tolvas, cámaras de CCTV industrial.
  3. **Sucursales Remotas / Puntos de Venta:** Estaciones ligeras conectadas mediante enlaces WAN / túneles VPN.
* **Segmentación de Red Lógica (Bloques RFC 1918):**
  - `10.10.10.0/24` $\to$ **VLAN 10: Gestión de Red y Monitoreo** (Switches, Firewalls, PDUs, Zabbix).
  - `10.10.20.0/24` $\to$ **VLAN 20: Servidores de Base de Datos y ERP** (Totalmente aislada, sin salida a internet).
  - `10.10.30.0/24` $\to$ **VLAN 30: Servidores de Aplicación y Servicios Locales** (Active Directory/LDAP, GLPI, Impresión).
  - `10.10.40.0/24` $\to$ **VLAN 40: DMZ (Zona Desmilitarizada)** (Nginx Reverse Proxy, Web externa).
  - `192.168.10.0/24` $\to$ **VLAN 100: Estaciones de Trabajo Administrativas**.
  - `192.168.20.0/24` $\to$ **VLAN 200: Operaciones de Planta / Balanzas / IT-OT**.
  - `172.16.50.0/24` $\to$ **VLAN 500: Red Wi-Fi Invitados** (Aislada por completo, solo salida HTTP/HTTPS).

---

## 2. LINEAMIENTOS Y CRITERIOS DE CALIDAD TÉCNICA

1. **Cero tono genérico de IA:**
   - Queda prohibido el uso de definiciones de diccionario vacías (*"Un cortafuegos es una pared que protege..."*).
   - Hablar como ingenieros de infraestructura: usar términos de ingeniería (`Handshake TLS 1.3`, `Default-Drop en Firewall`, `802.1Q Trunking`, `UPS doble conversión con bypass`, `RBAC`, `Tokens JWT`).
2. **Anonimización Estricta:**
   - No usar nombres de clientes, nombres de jefaturas ni IPs públicas reales.
   - Usar nomenclatura técnica normalizada (`srv-db-01`, `srv-app-02`, `fw-core-hq`, `sw-dist-planta`).
3. **Estándar de Diagramas Draw.io:**
   - Todo diagrama debe ser claro, con iconografía formal de redes/sistemas (cisco/aws/generic network).
   - Incluir leyenda de puertos/protocolos y límites de seguridad (zonas de confianza: Trusted, DMZ, Untrusted).

---

## 3. ESPECIFICACIÓN DE ENTREGABLES Y DIAGRAMAS DRAW.IO

Cada módulo debe contar con su lámina principal apoyada en un diagrama formal en Draw.io:

| # Diagrama | Archivo Draw.io sugerido | Contenido Obligatorio | Responsable |
| :--- | :--- | :--- | :--- |
| **D1** | `01_arquitectura_sistema_aic.drawio` | Arquitectura en 3 capas: Recursos de usuario, servicios locales/híbridos/cloud y troncales de comunicación redundantes. | Luis Rocha |
| **D2** | `02_seguridad_fisica_datacenter.drawio` | Layout del Data Center: Esclusas biométricas, racks con cerradura, pasillo frío/caliente, UPS + ATS + Grupo generador. | Jhoel Cruz |
| **D3** | `03_topologia_red_perimetro_dmz.drawio` | Topología de Red: Internet $\to$ NGFW $\to$ DMZ $\to$ Core Switch L3 $\to$ VLANs segmentadas y túnel VPN IPsec con Planta. | Freddy Ponce |
| **D4** | `04_flujo_identidad_iam_rbac.drawio` | Flujo de autenticación multifactor (MFA), validación con LDAP/Active Directory y asignación de privilegios RBAC. | Eliazar Campos |
| **D5** | `05_criptografia_firma_esteganografia.drawio` | Comparativa técnica: Handshake TLS 1.3, ciclo de firma digital (par asimétrico) y técnica de esteganografía LSB en imagen PNG. | Carlos Soruco |

---

## 4. REPARTO DETALLADO, GUIONES Y CASOS PRÁCTICOS POR INTEGRANTE

---

### Módulo 1: El Sistema Informático — Luis Rocha Vela
* **Duración:** 4 a 5 minutos.
* **Puntos del temario cubiertos:**
  * 1.1 El contexto informático
  * 1.2 La infraestructura del sistema (1.2.1 Recursos de usuario, 1.2.2 Recursos de servicio, 1.2.3 Recursos de comunicación)
  * 1.3 Los servicios del sistema (1.3.1 Locales, 1.3.2 Remotos, 1.3.3 Híbridos)
  * 1.4 La estructura y operativa (1.4.1 Diseño de infraestructura, 1.4.2 Operativa de servicios, 1.4.3 Seguridad base)

#### Guion y Defensa en Vivo:
* **Contexto de AIC S.A.:** 
  *"Nuestra organización opera en un entorno de alta demanda donde una interrupción en el sistema de recepción o facturación detiene el transporte de materia prima. Por ello, la infraestructura se diseñó con redundancia activa."*
* **Desglose de Recursos (1.2):**
  * *Usuario:* Laptops corporativas estandarizadas, terminales rugerizadas para balanzas en planta y terminales móviles con acceso limitado.
  * *Servicio:* Clúster de hipervisores en rack con almacenamiento centralizado SAN/NAS redundante, corriendo máquinas virtuales para ERP, gestión de incidencias (GLPI) y bases de datos transaccionales.
  * *Comunicación:* Enlace principal por fibra óptica monomodo dedicado y enlace de respaldo automático por microondas inalámbrico para tolerar cortes físicos de fibra en carretera.
* **Modelo de Servicios (1.3):**
  * *Locales:* Base de datos de producción y sistemas de pesaje en báscula (deben seguir operando al 100% incluso si se cae internet).
  * *Remotos:* Suite de ofimática en la nube (correo corporativo M365) y almacenamiento en frío en AWS S3.
  * *Híbridos:* Conexión persistente mediante túnel seguro para replicación de respaldos nocturnos fuera de sitio y sincronización de paneles de Business Intelligence.
* **Operativa y Seguridad del Sistema (1.4):**
  * Arquitectura desacoplada en tres capas (Presentación/Frontend, Lógica de Negocio/APIs y Persistencia en BBDD) para evitar acceso directo de los usuarios a las tablas críticas.

---

### Módulo 2: Seguridad Física y Recursos — Jhoel Alvaro Cruz Zurita
* **Duración:** 4 a 5 minutos.
* **Puntos del temario cubiertos:**
  * 2.1 Conceptos básicos de seguridad física
  * 2.2 Seguridad física del sistema (Data Center, controles ambientales)
  * 2.3 Seguridad de los recursos (2.3.1 Usuarios, 2.3.2 Servicios, 2.3.3 Comunicaciones, 2.3.4 Internet de las Cosas / IoT)

#### Guion y Defensa en Vivo:
* **Controles Físicos en Data Center (2.1 y 2.2):**
  * *"La seguridad lógica no sirve de nada si un atacante o un descuido físico puede desconectar un cable o robar un disco duro."*
  * Acceso perimetral en capas: Control de ingreso por esclusa con doble autenticación (tarjeta de proximidad RFID + huella biométrica). Racks cerrados bajo llave física con apertura restringida solo a administradores autorizados.
  * Monitoreo ambiental: Sistema de climatización de precisión en configuración N+1 (manteniendo 20°C a 22°C y humedad controlada del 45-50%).
  * Supresión de incendios: Detección temprana VESDA y extinción por inundación de gas limpio (FM-200 / Novec 1230), el cual apaga el fuego por desplazamiento térmico sin mojar ni dejar residuos en las placas electrónicas.
  * Energía ininterrumpida: Banco de UPS online de doble conversión (cero milisegundos de tiempo de transferencia) respaldado por grupo electrógeno con encendido automático mediante conmutador ATS.
* **Protección de Recursos y Dispositivos de Campo (2.3):**
  * *Estaciones de usuario:* Bloqueo de puertos USB por directiva para prevenir fugas de datos o ataques de *BadUSB*. Guayas de seguridad física Kensington en estaciones de áreas de atención al público.
  * *Comunicaciones:* Canalizaciones y bandejas de cableado estructurado bajo llave, gabinetes intermedios (IDF) sellados en planta.
  * *IoT y Básculas:* Aislamiento de básculas industriales, sensores e impresoras fiscales. Desactivación de interfaces web inseguras y cambio forzoso de contraseñas de fábrica para evitar que actúen como puente hacia la red corporativa.

---

### Módulo 3: Seguridad de Red y Perímetro — Freddy Emmanuel Ponce Quiroga
* **Duración:** 5 minutos.
* **Puntos del temario cubiertos:**
  * 2.4 La seguridad de la red:
    * 2.4.1 Segmentación de la red (VLANs y enrutamiento inter-VLAN filtrado)
    * 2.4.2 Redes inalámbricas (WPA3-Enterprise, autenticación 802.1X)
    * 2.4.3 El cortafuegos (Next-Generation Firewall - NGFW)
    * 2.4.4 Redes privadas virtuales (VPN IPsec Site-to-Site y VPN SSL para teletrabajo)
    * 2.4.5 Detección y prevención de intrusos (IDS/IPS)
    * 2.4.6 Zonas Desmilitarizadas (DMZ y arquitectura de publicación inversa)

#### Guion y Defensa en Vivo:
* **Segmentación de Red (2.4.1 y 2.4.2):**
  * *"En AIC S.A. aplicamos la política de Red de Confianza Cero (Zero Trust). El hecho de estar conectado físicamente a un puerto de red en la oficina no da visibilidad a los servidores."*
  * El switch core L3 aplica etiquetado 802.1Q. Las VLANs de administración (`VLAN 100`) no tienen comunicación directa con la VLAN de servidores de base de datos (`VLAN 20`).
  * En Wi-Fi: se prohíbe el uso de contraseñas compartidas preestablecidas. La red interna utiliza WPA3-Enterprise con 802.1X contra Active Directory; la red de visitantes (`VLAN 500`) está completamente aislada, con limitación de ancho de banda y bloqueo de tráfico peer-to-peer.
* **El Cortafuegos y la DMZ (2.4.3 y 2.4.6):**
  * El firewall NGFW opera con política estricta de *Default-Drop* (todo lo que no está explícitamente permitido está denegado).
  * La DMZ aloja los servicios accesibles desde el exterior (como el portal web de seguimiento o Nginx). Si el servidor web sufriera un ataque, el firewall le bloquea categóricamente cualquier intento de conexión hacia la red interna (`LAN`), permitiendo únicamente responder a peticiones legítimas de consulta a la API interna.
* **VPN e IDS/IPS (2.4.4 y 2.4.5):**
  * La comunicación entre la Planta Industrial y el Data Center Central viaja por un túnel IPsec Site-to-Site con cifrado AES-256-GCM.
  * Para teletrabajo o soporte externo se utiliza VPN SSL con obligatoriedad de MFA.
  * El motor IDS/IPS (Snort/Suricata integrado en el NGFW) inspecciona el tráfico en tiempo real bloqueando escaneos de puertos maliciosos (Nmap), ataques de fuerza bruta por SSH/RDP y firmas de vulnerabilidades conocidas.

---

### Módulo 4: Seguridad de Servicios, Identidad y Usuarios — Eliazar Russeu Campos Vistas
* **Duración:** 4 a 5 minutos.
* **Puntos del temario cubiertos:**
  * 3.1 La tríada de seguridad (Confidencialidad, Integridad, Disponibilidad)
  * 3.2 La seguridad de los usuarios (3.2.1 Autenticación, 3.2.2 Autorización, 3.2.3 Gestión de Identidad / IAM)
  * 3.3 Seguridad en servicios y comunicaciones (Hardening y ciclo de vida de credenciales)

#### Guion y Defensa en Vivo:
* **La Tríada de Seguridad en la Práctica Real (3.1):**
  * *Disponibilidad:* Balanceo de carga y réplica activa de base de datos para que el sistema de pesaje nunca se detenga.
  * *Integridad:* Validaciones a nivel de base de datos (restricciones de clave foránea, triggers de auditoría inmutables) y hashes de control para verificar que los registros de peso no sean adulterados.
  * *Confidencialidad:* Cifrado de datos y segmentación estricta de vistas: un operador de báscula puede registrar peso de camión, pero jamás consultar los estados financieros ni las cuentas por pagar.
* **Gestión de Identidad y Control de Acceso (3.2 y 3.3):**
  * *Autenticación:* Fin de las contraseñas simples. Se exige longitud mínima de 12 caracteres, complejidad y verificación en dos pasos (2FA/MFA) mediante aplicaciones basadas en tiempo (TOTP como Google/Microsoft Authenticator).
  * *Autorización basada en roles (RBAC):* Principio del menor privilegio (*Least Privilege*). Los permisos se otorgan a roles definidos (`Operador_Báscula`, `Auditor_Contable`, `Admin_Sistemas`), no a usuarios individuales de forma desordenada.
  * *Gestión del Ciclo de Vida (IAM):* Integración con LDAP / Directorio Activo centralizado. Cuando un empleado es dado de baja (*Offboarding*), su cuenta se deshabilita en el servidor central y automáticamente pierde acceso al correo, la VPN, el ERP y las estaciones locales, evitando cuentas huérfanas activas.

---

### Módulo 5: Seguridad de Contenidos y Criptografía — Carlos Andre Soruco Paz
* **Duración:** 4 a 5 minutos.
* **Puntos del temario cubiertos:**
  * 3.4 La seguridad de los contenidos:
    * 3.4.1 El cifrado (En reposo y en tránsito)
    * 3.4.2 La firma digital (Certificados digitales, no repudio y sellado de tiempo)
    * 3.4.3 La esteganografía (Fundamentos, riesgo de exfiltración encubierta y detección)

#### Guion y Defensa en Vivo:
* **Cifrado en Tránsito y Reposo (3.4.1):**
  * *"La información debe ser ilegible para cualquier tercero no autorizado, tanto cuando viaja por un cable como cuando está guardada en un disco."*
  * *En tránsito:* Uso exclusivo de TLS 1.3 con certificados X.509 válidos. Se bloquean explícitamente protocolos obsoletos (SSLv3, TLS 1.0, 1.1) y métodos en texto plano (HTTP, Telnet, FTP).
  * *En reposo:* Cifrado de disco completo con BitLocker / LUKS en laptops portátiles utilizando chip de seguridad TPM 2.0 (si se extravía la laptop, los datos son inaccesibles). Cifrado de copias de seguridad con algoritmo AES-256 antes de salir al almacenamiento secundario.
* **Firma Digital y No Repudio (3.4.2):**
  * Mecanismo: Se genera el hash SHA-256 del documento y se cifra con la clave privada del emisor. El receptor valida la autenticidad e integridad utilizando la clave pública contenida en el certificado digital.
  * Aplicación real en AIC S.A.: Autorización digital de órdenes de despacho y firmas de manifiestos de carga, garantizando que el documento no fue alterado en tránsito y que el autor no pueda repudiar su emisión.
* **Esteganografía: La Amenaza Invisible (3.4.3):**
  * Explicación técnica: Ocultamiento de información confidencial dentro de archivos portadores aparentemente normales (imágenes PNG/JPEG, audios o videos) sin alterar perceptiblemente su aspecto mediante la técnica de Modificación del Bit Menos Significativo (LSB - *Least Significant Bit*).
  * Caso de ataque / Exfiltración: Un empleado desleal extrae un archivo CSV con precios confidenciales y lista de proveedores, lo inyecta dentro de la fotografía institucional del logotipo corporativo y lo envía por correo electrónico personal burlando filtros de palabras clave.
  * Contramedidas de defensa: Sistemas DLP (Data Loss Prevention) y pasarelas de seguridad que eliminan metadatos, recalculan compresión de imágenes en el proxy perimetral y analizan anomalías de entropía estadística en los archivos exportados.

---

## 5. GUION DE TRANSICIONES ENTRE EXPOSITORES

Para mantener una sincronía perfecta durante la defensa, cada expositor concluirá dando paso formal a su compañero:

1. **Luis $\to$ Jhoel:**  
   *"Habiendo establecido la arquitectura de hardware y los servicios que sustentan la operación de nuestra organización, cedo la palabra a Jhoel Cruz, quien detallará cómo protegemos físicamente estas instalaciones y los recursos de campo."*
2. **Jhoel $\to$ Freddy:**  
   *"Con el Data Center resguardado y los controles de acceso físico en marcha, el siguiente frente crítico es la red lógica. Freddy Ponce explicará la arquitectura de segmentación, DMZ y firewalls perimetrales."*
3. **Freddy $\to$ Eliazar:**  
   *"Una vez blindado el perímetro y canalizado el tráfico, el foco pasa a quienes operan dentro del sistema. Eliazar Campos abordará la gestión de identidad, control de acceso RBAC y la preservación de la tríada de seguridad."*
4. **Eliazar $\to$ Carlos:**  
   *"Incluso con usuarios autenticados, el contenido de la información debe ser inviolable. Carlos Soruco cerrará nuestra exposición explicando los mecanismos de cifrado, la validez de la firma digital y los vectores de ataque por esteganografía."*
5. **Cierre de Carlos:**  
   *"Con esto concluimos la presentación de la arquitectura de seguridad integral de AIC S.A. Quedamos a disposición del docente para la ronda de preguntas."*

---

## 6. CRONOGRAMA DE PREPARACIÓN (13 Y 14 DE OCTUBRE)

| Fecha / Hora | Actividad | Meta Concreta |
| :--- | :--- | :--- |
| **13-Oct (12:00)** | Consolidación de Diapositivas | Documento de presentación unificado con el texto exacto por lámina. |
| **13-Oct (18:00)** | Integración de Diagramas Draw.io | Exportación de los 5 diagramas en alta calidad e inserción en las diapositivas. |
| **13-Oct (21:30)** | Ensayo General de Tiempos | Cronometrar la exposición completa (meta: 20-22 minutos en total, 4-5 min por persona). |
| **14-Oct (Mañana)** | Generación de Copias de Respaldo | Guardar presentación en formato nativo, exportar en PDF y cargar en pendrive de contingencia. |
| **14-Oct (Clase)** | Defensa Presencial | Ejecución coordinada de la presentación ante el tribunal/docente. |
