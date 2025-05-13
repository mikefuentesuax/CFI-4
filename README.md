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


