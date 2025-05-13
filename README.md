# CFI-4
https://github.com/mikefuentesuax/CFI-4.git
# Paso 1: Diseño y Modelado de la Arquitectura de Comunicación

## Análisis de Modelos OSI y TCP/IP para la Integración de Servicios

Para el diseño de la red de comunicaciones de la ciudad inteligente, es fundamental comprender la funcionalidad de los modelos de referencia OSI (Open Systems Interconnection) y TCP/IP (Transmission Control Protocol/Internet Protocol). Estos modelos proporcionan un marco conceptual para la comunicación en red, organizando las complejas interacciones en capas con funciones específicas.

### Modelo OSI:
Consta de siete capas (Física, Enlace de Datos, Red, Transporte, Sesión, Presentación y Aplicación), cada una responsable de una parte específica del proceso de comunicación.

### Modelo TCP/IP:
Un modelo más práctico y utilizado en la implementación de Internet y redes modernas, que se compone de cuatro capas (Acceso a la Red, Internet, Transporte y Aplicación).

La integración de estos modelos para soportar los diversos servicios de la ciudad inteligente se realizará de la siguiente manera:

- **Capa de Acceso a la Red (TCP/IP) / Capas Física y Enlace de Datos (OSI):**
  - Tecnologías: Ethernet, Wi-Fi, 5G/LTE, LoRaWAN
  - Criterios: ancho de banda, alcance y movilidad
  - Ejemplos: fibra óptica, acceso ciudadano, sensores IoT

- **Capa de Internet (TCP/IP) / Capa de Red (OSI):**
  - Función: direccionamiento lógico (IPv4/IPv6), enrutamiento
  - Protocolos: OSPF, BGP

- **Capa de Transporte (TCP/IP y OSI):**
  - TCP para servicios confiables (gobierno, archivos, bases de datos)
  - UDP para tiempo real (video vigilancia, alertas)

- **Capa de Aplicación (TCP/IP) / Capas Sesión, Presentación y Aplicación (OSI):**
  - Protocolos: HTTPS, RTSP/RTP, SIP, VoIP, MQTT, CoAP, SNMP, DASH, HLS, DNS

## Diseño Lógico y Segmentación de la Ciudad

Zonas:

- **Zona Gubernamental:** Alta seguridad y confiabilidad
- **Zona de Seguridad Pública y Emergencias:** Baja latencia, alta disponibilidad
- **Zona de Transporte y Monitoreo Ambiental:** Alta capacidad y bidireccionalidad
- **Zona de Servicios Multimedia para el Ciudadano:** Ancho de banda y disponibilidad
- **Infraestructura Central:** Servidores, routers de núcleo, gestión de red

## Interconexión de Dispositivos

- **Routers:** Capa 3, enrutamiento entre segmentos
- **Switches:** Capa 2, conectividad local, PoE
- **Puntos de Acceso Inalámbrico (APs):** Wi-Fi, IoT
- **Servidores:** Aplicaciones, DNS, video vigilancia, IoT
- **Dispositivos Finales:** PCs, cámaras, sensores, semáforos, pantallas

Topología híbrida:
- Estrella (dispositivos a switches)
- Malla/Anillo (infraestructura central)
- Fibra óptica (troncales)
- Cobre/inalámbrico (finales)


Claro, aquí tienes los Pasos 2 y 3 nuevamente, en formato Markdown, fieles al texto original y bien estructurados:


---

# Paso 2: Capa Física – Cálculos y Selección de Tecnologías

## Cálculo de la Capacidad de los Enlaces

La capacidad máxima teórica de un canal de comunicación está limitada por su ancho de banda y la relación señal a ruido (SNR). Podemos calcular esta capacidad utilizando la fórmula de Shannon-Hartley:

C = B × log2(1 + SNR_lineal)

SNR_lineal = 10^(SNR(dB)/10)

### Ejemplo Práctico: Enlace Inalámbrico Crítico

Parámetros:

- B = 300 MHz = 300×10⁶ Hz  
- SNR(dB) = 20 dB

Conversión y Cálculo:

- SNR_lineal = 10^(20/10) = 100  
- C = 300×10⁶ × log₂(101) ≈ 1.9974×10⁹ bps = 1.9974 Gbps

**Conclusión:** El enlace soportaría aproximadamente 1.9974 Gbps, suficiente para video HD y servicios simultáneos.

## Selección de Técnicas de Modulación

### Opciones:

- **BPSK**: 1 bit/s/Hz – Alta robustez, baja eficiencia
- **QPSK**: 2 bits/s/Hz – Equilibrado
- **16-QAM**: 4 bits/s/Hz – Alta eficiencia, menos robusto

### Aplicación:

- **Enlaces Cableados** (Ethernet, fibra): se pueden usar técnicas de orden superior como 64-QAM o 256-QAM.
- **Enlaces Inalámbricos** (Wi-Fi, 5G/LTE): modulación adaptativa con QPSK hasta 256-QAM.
- **Enlaces IoT de bajo consumo** (LoRaWAN): FSK o chirp spread spectrum por su eficiencia energética.

## Evaluación de la Eficiencia del Encapsulamiento

Ejemplo con paquete de aplicación de 1500 bytes:

- Cabecera Ethernet: 14 bytes  
- Preámbulo + SFD: 8 bytes  
- FCS: 4 bytes  
- **Total de sobrecarga:** 26 bytes

### Cálculo de Eficiencia:

Eficiencia = 1500 / (1500 + 26) ≈ 0.983

**Resultado:** ~98.3% del ancho de banda se dedica a datos útiles.

**Implicación:** Optimizar MTU y evitar cabeceras innecesarias es clave, especialmente en enlaces limitados.


---

# Paso 3: Capa de Red – Direccionamiento, Subneteo y Enrutamiento

## Diseño del Esquema de Direccionamiento IP

Esquema basado en IPv4 privadas (10.0.0.0/8), con segmentación por zonas:

- **Zona Gubernamental**: 10.0.0.0/24  
- **Seguridad Pública y Emergencias**: 10.0.1.0/24  
- **Transporte y Monitoreo Ambiental**: 10.0.2.0/24  
- **Servicios Multimedia al Ciudadano**: 10.0.3.0/24  
- **Infraestructura Central**: 10.0.10.0/24

### Ejemplo: Zona Gubernamental (10.0.0.0/24)

- Dirección de Red: 10.0.0.0  
- Máscara: 255.255.255.0  
- Broadcast: 10.0.0.255  
- Rango de Hosts: 10.0.0.1 – 10.0.0.254

### Otros Segmentos:

- **10.0.1.0/24**: Seguridad y Emergencias  
- **10.0.2.0/24**: Transporte y Monitoreo  
- **10.0.3.0/24**: Multimedia  
- **10.0.10.0/24**: Núcleo y servidores

**Nota:** Segmentación con /24 por escalabilidad. Espacio 10.0.0.0/8 permite crecimiento sin IPs públicas.

## Enrutamiento y Rutas Óptimas

Se implementará **enrutamiento dinámico** (ej. OSPF) para asegurar conectividad eficiente.

### Algoritmo de Dijkstra (Ejemplo):

Topología simplificada:

[Router Seguridad] --(2)--> [Router Núcleo 1] --(1)--> [Router Emergencias] [Router Seguridad] --(3)--> [Router Núcleo 2] --(2)--> [Router Emergencias]

#### Cálculo:

- Ruta óptima: Seguridad → Núcleo 1 → Emergencias (costo 3)

**Protocolo dinámico** como OSPF se encargará de estos cálculos de forma automática.

## Enrutamiento por Inundación como Respaldo

- Método de respaldo: reenvío por todas las interfaces (excepto origen)
- Costoso, pero útil en casos críticos
- **Controles necesarios:** TTL, identificadores de paquete para evitar bucles
- Activación temporal hasta recuperación del enrutamiento principal


---


# Paso 4: Capa de Transporte – Selección de Protocolos y Cálculo del Tamaño de Ventana

La capa de transporte es responsable de proporcionar servicios de transporte de datos de extremo a extremo entre las aplicaciones que se ejecutan en los diferentes dispositivos de la red. Los dos protocolos principales que operan en esta capa son **TCP (Transmission Control Protocol)** y **UDP (User Datagram Protocol)**.

## Selección de Protocolos de Transporte

La elección entre TCP y UDP depende de los requisitos específicos de cada servicio en términos de fiabilidad, orden de entrega y latencia.

### TCP (Transmission Control Protocol)

Protocolo orientado a la conexión que proporciona una entrega de datos fiable, ordenada y con control de errores. Establece una conexión antes de la transferencia de datos, garantiza que los paquetes lleguen en el mismo orden en que fueron enviados y retransmite los paquetes perdidos.

**Adecuado para:**

- **Transferencia de Archivos (FTP/SFTP):** Asegura que los datos se reciban correctamente.
- **Actualizaciones de Bases de Datos:** Garantiza que todas las actualizaciones se apliquen de manera fiable y en orden.
- **Navegación Web Segura (HTTPS):** Asegura la correcta carga de páginas y la integridad de los datos.

### UDP (User Datagram Protocol)

Protocolo sin conexión que proporciona entrega de datos no fiable y sin orden. No establece conexión previa ni garantiza la entrega de paquetes.

**Adecuado para:**

- **Streaming de Cámaras de Seguridad:** Baja latencia es preferible a entrega perfecta.
- **Alertas de Tráfico:** Entrega rápida es más importante que la fiabilidad total.
- **VoIP (Voz sobre IP):** Prefiere baja latencia sobre retransmisión.

## Cálculo del Tamaño de Ventana en TCP

El tamaño de la ventana TCP controla la cantidad de datos que el emisor puede enviar antes de recibir una confirmación (ACK). Su valor óptimo maximiza el rendimiento sin sobrecargar la red.

**Fórmula:**

Ventana_óptima = Ancho de banda × RTT

### Ejemplo Práctico:

- Ancho de banda: 100 Mbps = 100 × 10⁶ bps  
- RTT: 50 ms = 0.05 s

**Cálculo:**

- Ventana_óptima = 100 × 10⁶ × 0.05 = 5 × 10⁶ bits  
- Convertido a bytes: 5 × 10⁶ / 8 = 625,000 bytes = **625 KB**

**Con MSS (Maximum Segment Size) = 1500 bytes:**

Número de segmentos = 625,000 / 1500 ≈ 416.67

**Conclusión:** El emisor puede tener ~416 segmentos en tránsito para aprovechar totalmente el ancho de banda sin esperar confirmaciones individuales. En la práctica, este valor está limitado por buffers, congestión y configuración

---

# Paso 5: Capa de Aplicación – Servicios, Multiplexación y Multimedia

La capa de aplicación es la capa más cercana al usuario final, proporcionando los servicios de red a las aplicaciones. En esta capa operan diversos protocolos que facilitan la comunicación para los diferentes servicios de la ciudad inteligente.

## Implementación de Servicios y Resolución de Nombres

Para la correcta funcionalidad de la red, se requiere la implementación de varios servicios esenciales:

- **DNS (Domain Name System):**
  - Traduce nombres de dominio a direcciones IP.
  - Se implementarán servidores DNS redundantes.
  - Ejemplo: www.ciudadinteligente.gob.es.

- **FTP/SFTP (File Transfer Protocol/Secure File Transfer Protocol):**
  - Transferencia segura de archivos entre organismos.
  - Preferencia por SFTP debido al cifrado.

- **HTTP/HTTPS (Hypertext Transfer Protocol/HTTP Secure):**
  - Portales web para acceso ciudadano.
  - HTTPS garantiza confidencialidad e integridad.

## Multiplexación

Permite que un único servidor atienda múltiples conexiones simultáneamente usando distintos puertos.

**Ejemplos de puertos:**

- HTTP: 80  
- HTTPS: 443  
- DNS: 53  
- FTP: 20 (datos) y 21 (control)  
- SFTP: 22

**Funcionamiento:**

El cliente indica IP y puerto; el servidor direcciona la solicitud a la aplicación correspondiente.

## Servicios Multimedia

Provisión eficiente de contenido multimedia es clave para seguridad y participación ciudadana.

### Streaming en Tiempo Real para Cámaras de Seguridad

- Protocolos: **RTSP + RTP sobre UDP**
- Baja latencia prioritaria, tolerancia a pérdida de paquetes.
- Alternativas sobre TCP: **HLS**, **DASH**

### Streaming en Tiempo Real de Eventos Públicos

- Protocolos: **HLS**, **DASH**
- Basados en HTTP/HTTPS, adaptativos.
- Fragmentos de video en diferentes calidades (bitrates).
- Cliente elige calidad según ancho de banda disponible.

## Adaptación de la Calidad del Contenido

- Cliente ajusta la calidad del video dinámicamente según condiciones de red.
- Evita interrupciones (buffering) y mejora la experiencia del usuario.
- Compatible con navegadores modernos y dispositivos móviles.

---

# Paso 6: Seguridad – Estrategias y Configuración

La seguridad es una prioridad fundamental en el diseño de la red de la ciudad inteligente, dada la criticidad de los servicios que soporta y la sensibilidad de la información que se transmite. Se implementará un enfoque de seguridad en capas para proteger la infraestructura contra diversas amenazas.

## Políticas y Medidas de Seguridad

Se diseñará un plan de seguridad integral que incluya las siguientes medidas:

### Uso de VPN (Virtual Private Network) para Interconexión de Segmentos Sensibles

- Asegura la confidencialidad e integridad de la comunicación entre segmentos críticos.
- Protocolos recomendados: **IPsec**, **OpenVPN**.
- Crea túneles cifrados a través de la red.

### Configuración de Firewalls

- Ubicados en puntos de entrada/salida de cada segmento y la infraestructura central.
- Inspeccionan tráfico y aplican reglas mediante listas de control de acceso (ACLs).
- Protegen contra accesos no autorizados, DoS y malware.

### Listas de Control de Acceso (ACLs)

- Configuradas en routers y switches.
- Controlan tráfico en capas 3 y 4 (IP y puertos TCP/UDP).
- Ejemplo: permitir solo tráfico necesario entre la zona de seguridad y el centro de emergencias.

### Sistemas de Detección y Prevención de Intrusiones (IDS/IPS)

- Monitorean tráfico para detectar patrones sospechosos o maliciosos.
- IPS puede bloquear o mitigar automáticamente amenazas.

## Cifrado y Autenticación

### Uso de TLS/SSL (Transport Layer Security / Secure Sockets Layer)

- Cifran comunicaciones críticas:
  - HTTPS para portales web
  - SFTP para transferencia de archivos
  - VPNs

### Implementación de RSA para Intercambio de Información Segura

- Criptografía asimétrica para cifrado y firma digital.
- Aplicación: autenticación de dispositivos, intercambio de claves VPN.

**Proceso simplificado:**

1. Elegir dos primos grandes `p`, `q`
2. Calcular `n = p × q`
3. Calcular `ϕ(n) = (p−1)(q−1)`
4. Elegir `e` tal que `1 < e < ϕ(n)` y `mcd(e, ϕ(n)) = 1`
5. Calcular `d` tal que `(d×e) mod ϕ(n) = 1`

- Clave pública: (n, e)  
- Clave privada: (n, d)  

**Cifrado:**  
`C = M^e mod n`  
**Descifrado:**  
`M = C^d mod n`

### Implementación de DNSSEC (Domain Name System Security Extensions)

- Protege contra DNS spoofing.
- Añade firmas digitales a los registros DNS.
- Permite a los clientes verificar autenticidad e integridad de respuestas DNS.
