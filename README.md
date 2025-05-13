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

