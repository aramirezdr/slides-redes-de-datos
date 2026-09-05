---
theme: default
title: Unidad 1 — Fundamentos y Diseño de Data Center
info: |
  Unidad 1 — Redes de Datos
  Especialización en Gestión de Redes de Datos
  Universidad Nacional de Colombia
  Duración total: 10 horas
author: Universidad Nacional de Colombia
date: 2026
class: text-center
highlighter: shiki
lineNumbers: false
mdc: true
---

# Unidad 1

## Fundamentos y Diseño de Data Center

### Redes de Datos

**Especialización en Gestión de Redes de Datos**

Universidad Nacional de Colombia

<div class="abs-br m-6 text-sm opacity-70">
Duración total: 10 horas
</div>

---
layout: intro
---

# Estructura de la Unidad

| Bloque | Duración | Tema |
|---|---:|---|
| 1 | 1 h 30 min | Evolución y componentes |
| 2 | 1 h 30 min | Arquitecturas de red |
| 3 | 1 h 30 min | Capacidad y sobresuscripción |
| 4 | 1 h 30 min | Estándares y disponibilidad |
| 5 | 1 h 30 min | Direccionamiento IP y VXLAN |
| 6 | 2 h 30 min | Caso integrador y evaluación |

> **Total:** 10 horas de trabajo académico.

---

# Resultados de aprendizaje

Al finalizar la unidad, el estudiante podrá:

<v-clicks>

- Explicar la evolución de los centros de datos
- Diferenciar cómputo, red, almacenamiento e infraestructura física
- Comparar arquitecturas de tres capas y Spine–Leaf
- Calcular sobresuscripción y disponibilidad con supuestos explícitos
- Distinguir estándares, clasificaciones y certificaciones
- Identificar dominios de falla y fallas de modo común
- Diseñar un direccionamiento IP escalable
- Explicar underlay, overlay, VXLAN, VTEP y EVPN

</v-clicks>

---

# Metodología de trabajo

<div class="grid grid-cols-2 gap-5 text-left">

<div class="border rounded-lg p-4">

### Análisis

- Exposición guiada
- Discusión crítica
- Casos reales

</div>

<div class="border rounded-lg p-4">

### Diseño

- Talleres cuantitativos
- Diseño de arquitecturas
- Trabajo colaborativo

</div>

<div class="border rounded-lg p-4">

### Validación

- Actividades prácticas
- Defensa técnica
- Retroalimentación

</div>

<div class="border rounded-lg p-4">

### Criterio central

Cada decisión debe justificar sus supuestos, riesgos y *trade-offs*.

</div>

</div>

---

# Evaluación de la unidad

<div class="grid grid-cols-2 gap-x-10 text-left text-sm">

<div>

- Corrección técnica: **25%**
- Justificación arquitectónica: **20%**
- Capacidad, escalabilidad y disponibilidad: **15%**
- Seguridad y segmentación: **15%**

</div>

<div>

- Dominios de falla y pruebas: **10%**
- Documentación y trazabilidad: **10%**
- Automatización, IPAM y observabilidad: **5%**

</div>

</div>

---
layout: section
---

# Bloque 1

## Evolución y componentes

### Duración: 1 h 30 min

---

# El centro de datos como sistema

```mermaid
flowchart LR
  APP[Aplicaciones] --> CMP[Cómputo]
  APP --> NET[Red]
  APP --> STO[Almacenamiento]
  CMP --> PHY[Infraestructura física]
  NET --> PHY
  STO --> PHY
  PHY --> OPS[Operación y seguridad]
  OPS --> APP
```

La calidad del servicio depende de la interacción entre infraestructura, software, personas y procesos.

---

# Evolución histórica

```mermaid
timeline
  title Evolución de los centros de datos
  1960-1980 : Computación centralizada y mainframes
  1990-2000 : Cliente-servidor, Ethernet y x86
  2000-2010 : Virtualización y consolidación
  2010-2020 : Nube, APIs y automatización
  Actualidad : Híbrido, edge, IA y cargas distribuidas
```

> Las etapas son un modelo didáctico: se superponen y no representan fronteras absolutas.

---

# De la centralización a la nube

| Etapa | Aporte principal | Reto frecuente |
|---|---|---|
| Mainframe | Cómputo centralizado | Costo y dependencia del sistema central |
| Cliente-servidor | Distribución de aplicaciones | Proliferación de servidores |
| Virtualización | Consolidación y movilidad | Sobreconsolidación y operación |
| Nube | Aprovisionamiento por software | Gobierno y dependencia de servicios |
| Híbrido / edge / IA | Cargas distribuidas | Latencia, energía y complejidad |

---

# Componentes del centro de datos

<div class="grid grid-cols-2 gap-4 text-left text-sm">

<div class="border rounded-lg p-3">

### Cómputo

Servidores rack, blade, hiperconvergencia, GPU, DPU y aceleradores.

</div>

<div class="border rounded-lg p-3">

### Red

Leaf, spine, firewalls, balanceadores, WAN, Internet y gestión fuera de banda.

</div>

<div class="border rounded-lg p-3">

### Almacenamiento

SAN, NAS, object storage, iSCSI, Fibre Channel y NVMe over Fabrics.

</div>

<div class="border rounded-lg p-3">

### Infraestructura física

Energía, UPS, generadores, refrigeración, racks, cableado y seguridad física.

</div>

</div>

---

# Actividad 1

## Análisis de un centro de datos

En equipos de 3 o 4 personas:

1. Seleccionen un centro de datos real o una instalación conocida.
2. Identifiquen cómputo, red, almacenamiento e infraestructura física.
3. Determinen la etapa evolutiva predominante.
4. Identifiquen dos riesgos operativos y una oportunidad de mejora.

<div class="mt-6 text-sm opacity-75">
Tiempo sugerido: 25 minutos.
</div>

---

# Cierre del bloque 1

- El centro de datos es un sistema de sistemas.
- La evolución responde a capacidad, disponibilidad, flexibilidad y costo.
- La infraestructura física y lógica debe diseñarse de forma integrada.

> **Pregunta:** ¿Qué condiciones justificarían mantener una carga en una instalación propia en vez de migrarla a nube pública?

---
layout: section
---

# Bloque 2

## Arquitecturas de red

### Duración: 1 h 30 min

---

# Arquitectura de tres capas

```mermaid
flowchart TB
  CORE[Core] --> D1[Distribution 1]
  CORE --> D2[Distribution 2]
  D1 --> A1[Access 1]
  D1 --> A2[Access 2]
  D2 --> A3[Access 3]
  D2 --> A4[Access 4]
  A1 --> S1[Servidores]
  A2 --> S2[Servidores]
  A3 --> S3[Servidores]
  A4 --> S4[Servidores]
```

<div class="grid grid-cols-3 gap-4 mt-4 text-sm text-left">
<div><b>Acceso</b><br>Conecta equipos finales.</div>
<div><b>Distribución</b><br>Agregación, políticas y routing.</div>
<div><b>Núcleo</b><br>Conectividad de alta capacidad.</div>
</div>

---

# Arquitectura Spine–Leaf

```mermaid
flowchart TB
  S1[Spine 1] --- L1[Leaf 1]
  S1 --- L2[Leaf 2]
  S1 --- L3[Leaf 3]
  S2[Spine 2] --- L1
  S2 --- L2
  S2 --- L3
  S3[Spine 3] --- L1
  S3 --- L2
  S3 --- L3
  L1 --> R1[Rack A]
  L2 --> R2[Rack B]
  L3 --> R3[Rack C]
```

Cada leaf se conecta con cada spine en el fabric básico.

---

# Qué aporta Spine–Leaf

<div class="grid grid-cols-2 gap-5 text-left">

<div class="border rounded-lg p-4">

### Data plane

- Múltiples rutas mediante ECMP
- Caminos con número de saltos predecible
- Mejor adaptación a tráfico East–West

</div>

<div class="border rounded-lg p-4">

### Operación

- Underlay IP en capa 3
- Escalamiento horizontal condicionado por capacidad
- Menor dependencia de STP en el underlay

</div>

</div>

> No garantiza por sí mismo una red no bloqueante ni latencia constante.

---

# Tres capas y Spine–Leaf

| Criterio | Tres capas | Spine–Leaf |
|---|---|---|
| Modelo | Acceso, distribución, núcleo | Leaf y spine |
| Tráfico frecuente | North–South | East–West |
| Multipath | Depende del diseño | ECMP en underlay L3 |
| Escalabilidad | Jerárquica | Horizontal |
| Latencia | Puede variar | Saltos más predecibles |
| Uso común | Campus y redes heredadas | Fabrics de data center |

---

# Underlay y overlay

```mermaid
flowchart LR
  H1[Host A] --> L1[VTEP Leaf A]
  L1 -->|IP / ECMP| SP[Spine]
  SP --> L2[VTEP Leaf B]
  L2 --> H2[Host B]
  L1 -. VXLAN .-> L2
```

| Plano | Función |
|---|---|
| Underlay | Red IP física entre dispositivos y VTEPs |
| Overlay | Red lógica independiente de la topología física |
| VTEP | Encapsula y desencapsula tráfico VXLAN |
| EVPN | Plano de control frecuentemente basado en MP-BGP |

---

# Actividad 2

## Comparación de arquitecturas

En grupos:

1. Diseñen una arquitectura de tres capas para 100 servidores.
2. Diseñen un fabric Spine–Leaf para los mismos 100 servidores.
3. Comparen trayectorias, capacidad, escalabilidad y operación.
4. Identifiquen dos dominios de falla en cada alternativa.

<div class="mt-5 text-sm opacity-75">Tiempo sugerido: 30 minutos.</div>

---

# Cierre del bloque 2

- La arquitectura debe responder al perfil de tráfico y al crecimiento esperado.
- Spine–Leaf favorece rutas ECMP y tráfico East–West.
- Underlay y overlay separan conectividad física y segmentación lógica.

---
layout: section
---

# Bloque 3

## Capacidad y sobresuscripción

### Duración: 1 h 30 min

---

# Capacidad de un leaf

## Escenario ilustrativo

Un leaf tiene:

- 44 puertos de servidor de 25 Gb/s.
- 4 uplinks de 100 Gb/s.

$$
\text{Capacidad de servidores}
= 44 \times 25
= 1100\ \text{Gb/s}
$$

$$
\text{Capacidad de uplinks}
= 4 \times 100
= 400\ \text{Gb/s}
$$

---

# Cálculo de sobresuscripción

$$
\text{Sobresuscripción}
= \frac{\text{capacidad agregada hacia servidores}}{\text{capacidad agregada de uplinks}}
$$

## Ejemplo

$$
\text{Sobresuscripción}
= \frac{1100}{400}
= 2.75:1
$$


> La relación aceptable depende de tráfico, picos, criticidad, QoS, SLA y patrón de aplicaciones.

---

# Taller cuantitativo

<div class="grid grid-cols-2 gap-6 text-left">

<div class="border rounded-lg p-4">

### Ejercicio 1

- 32 puertos de 25 Gb/s
- 4 uplinks de 100 Gb/s

Calcule la sobresuscripción.

</div>

<div class="border rounded-lg p-4">

### Ejercicio 2

- 48 puertos de 10 Gb/s
- 4 uplinks de 40 Gb/s

Calcule la sobresuscripción.

</div>

</div>

<div class="mt-6 text-sm opacity-75">Tiempo sugerido: 20 minutos.</div>

---

# Actividad 3

## Diseño de capacidad

En grupos, propongan un diseño para 200 servidores de 25 Gb/s con conectividad dual-homed:

- Número de leafs, spines y enlaces.
- Capacidad hacia servidores y uplinks por leaf.
- Sobresuscripción esperada.
- Crecimiento máximo sin ampliar spines.
- Supuestos necesarios para evaluar tolerancia a fallas.

<div class="mt-5 text-sm opacity-75">Tiempo sugerido: 30 minutos.</div>

---

# Cierre del bloque 3

- La sobresuscripción se calcula con capacidad, no solo con puertos.
- El cálculo debe incluir velocidad, redundancia y patrón de tráfico.
- Todo diseño debe indicar sus supuestos y margen de crecimiento.

---
layout: section
---

# Bloque 4

## Estándares y disponibilidad

### Duración: 1 h 30 min

---

# Conceptos que no deben confundirse

| Concepto | Naturaleza | Finalidad |
|---|---|---|
| ANSI/TIA-942 | Estándar técnico | Infraestructura de data center |
| TIA-942 Rating | Clasificación | Niveles de infraestructura |
| Certificación TIA-942 | Evaluación | Conformidad frente a requisitos |
| Uptime Tier | Clasificación propietaria | Topología y resiliencia esperada |
| ISO/IEC 27001 | Sistema de gestión | Seguridad de información |
| ITIL | Marco de prácticas | Gestión de servicios TI |

> Los Ratings TIA-942 y los Tiers Uptime no son equivalentes automáticamente.

---

# Uptime Institute Tier Standard

| Tier | Descripción general |
|---|---|
| Tier I | Infraestructura básica |
| Tier II | Componentes redundantes |
| Tier III | Infraestructura mantenible concurrentemente |
| Tier IV | Infraestructura tolerante a fallas |

Un Tier no es una garantía de disponibilidad de extremo a extremo para una aplicación.

---

# Disponibilidad: modelo simplificado

La disponibilidad simplificada de un componente reparable es:

$$
A = \frac{MTBF}{MTBF + MTTR}
$$

> Donde:
> - MTBF: tiempo medio entre fallas.
> - MTTR: tiempo medio de reparación o recuperación.

Ejemplo: 
Con MTBF = 8.760 horas y MTTR = 4 horas:

$$
A=\frac{8760}{8760+4}=0.999543
$$

**Disponibilidad aproximada: 99,9543%, equivalente a cerca de 4 horas de indisponibilidad anual.**

> El modelo no representa fallas comunes, dependencias, mantenimiento, software o errores humanos.

---

# Modelos de redundancia

| Modelo | Significado |
|---|---|
| N | Capacidad mínima para la carga |
| N+1 | Capacidad requerida más una unidad adicional |
| 2N | Dos rutas independientes, cada una con capacidad total |
| 2N+1 | Dos rutas completas más una unidad adicional |

La decisión depende del impacto al negocio, costo, mantenimiento, eficiencia y riesgo residual.

---

# Ejemplo de N+1

Una carga de **300 kW** se soporta con cuatro UPS de **100 kW**:

<div class="grid grid-cols-2 gap-6 text-left">

<div>

### Operación normal

- 4 UPS activos
- 75 kW por UPS
- Carga total: 300 kW

</div>

<div>

### Falla de un UPS

- 3 UPS restantes
- 100 kW por UPS
- Carga total soportada: 300 kW

</div>

</div>

Este es un ejemplo de capacidad **N+1**.

---

# Dominios de falla

<div class="grid grid-cols-2 gap-4 text-left text-sm">

<div class="border rounded-lg p-3"><b>Físicos</b><br>Rack, fila, sala, edificio, región.</div>
<div class="border rounded-lg p-3"><b>Eléctricos y mecánicos</b><br>PDU, UPS, circuito, generador, chiller.</div>
<div class="border rounded-lg p-3"><b>Lógicos</b><br>Switch, VTEP, DNS, controlador, clúster, VLAN/VNI.</div>
<div class="border rounded-lg p-3"><b>Operativos</b><br>Cambios, credenciales, automatización, software y error humano.</div>

</div>

> La redundancia reduce fallas individuales, pero no elimina fallas de modo común.

---

# RTO y RPO

<div class="grid grid-cols-2 gap-6 text-left">

<div class="border rounded-lg p-5">

## RTO

Tiempo máximo **objetivo** para restaurar un servicio tras una interrupción.

</div>

<div class="border rounded-lg p-5">

## RPO

Máxima pérdida de datos **aceptable**, expresada como tiempo.

</div>

</div>

<div class="mt-6 text-left">

Estos objetivos deben derivarse de un **Análisis de Impacto al Negocio (BIA)**; no de valores genéricos por tipo de aplicación.

</div>

---

# Actividad 4

## Análisis de resiliencia

En equipos:

1. Diferencien Tier III, Rated-3 y una certificación.
2. Comparen N+1 y 2N para una carga crítica.
3. Propongan RTO y RPO para pagos, ERP, portal interno y archivo histórico.
4. Justifiquen las decisiones con impacto, costo y riesgo.

<div class="mt-5 text-sm opacity-75">Tiempo sugerido: 30 minutos.</div>

---

# Cierre del bloque 4

- Un estándar, una clasificación y una certificación no son equivalentes.
- La disponibilidad depende de componentes técnicos y procesos operativos.
- RTO y RPO deben responder al impacto de negocio.

---
layout: section
---

# Bloque 5

## Direccionamiento IP y VXLAN

### Duración: 1 h 30 min

---

# Principios de direccionamiento

<v-clicks>

- Agregación de rutas y escalabilidad
- Separación por función, entorno, tenant o zona de seguridad
- Integración con DNS, DHCP, IPAM, automatización y monitoreo
- Crecimiento planificado y prevención de solapamientos
- Soporte IPv4 e IPv6 cuando sea aplicable
- Trazabilidad mediante una fuente de verdad gobernada

</v-clicks>

> Un sistema IPAM o CMDB debe registrar prefijos, VLAN/VNI, dispositivos, interfaces y asignaciones.

---

# Convenciones de host IPv4

## Ejemplo para una red `/24`

| Rango | Uso convencional posible |
|---|---|
| `.1` | Gateway virtual o interfaz de gateway |
| `.2–.9` | Infraestructura o servicios reservados |
| `.10–.49` | Servidores de aplicación |
| `.50–.99` | DHCP o asignaciones dinámicas |
| `.100–.109` | Direcciones virtuales de servicios |
| `.110–.200` | Hosts estáticos o reservas |

> La dirección de broadcast depende del prefijo; no se determina solo por el último octeto.

---

# VXLAN, VNI y VTEP

```mermaid
flowchart LR
  H1[Host en VNI 10010] --> V1[VTEP Leaf A]
  V1 -->|UDP/VXLAN sobre IP| V2[VTEP Leaf B]
  V2 --> H2[Host en VNI 10010]
```

- VXLAN encapsula tráfico de segmentos lógicos sobre una red IP.
- El VNI tiene 24 bits: permite aproximadamente 16 millones de identificadores.
- EVPN puede proporcionar el plano de control para MAC, IP, VTEP y segmentos.

---

# Requisitos operativos del overlay

<div class="grid grid-cols-2 gap-5 text-left text-sm">

<div>

### Underlay

- Conectividad IP entre VTEPs
- ECMP y convergencia
- MTU suficiente para encapsulación
- Observabilidad de rutas y enlaces

</div>

<div>

### Overlay

- Segmentación mediante VNI
- Control plane EVPN cuando aplique
- Políticas de seguridad distribuidas
- Trazabilidad de MAC, IP y endpoints

</div>

</div>

---

# Actividad 5

## Plan IP e integración overlay

En grupos:

1. Propongan prefijos IPv4 e IPv6 para underlay, loopbacks y segmentos de servicio.
2. Definan rangos para gestión, web, aplicación, base de datos, respaldo y almacenamiento.
3. Identifiquen dos riesgos de solapamiento y cómo prevenirlos.
4. Expliquen qué datos deben mantenerse en IPAM.

<div class="mt-5 text-sm opacity-75">Tiempo sugerido: 30 minutos.</div>

---

# Cierre del bloque 5

- El direccionamiento debe facilitar agregación, operación y crecimiento.
- VXLAN aporta encapsulación y EVPN puede aportar control plane.
- IPAM, automatización y observabilidad son requisitos operativos.

---
layout: section
---

# Bloque 6

## Caso integrador y evaluación

### Duración: 2 h 30 min

---

# Caso integrador

## Diseño de un fabric inicial

Una organización requiere conectar **200 servidores dual-homed**.

<div class="grid grid-cols-2 gap-5 text-left text-sm mt-4">

<div class="border rounded-lg p-4">

### Requisitos

- Dos interfaces de 25 Gb/s por servidor
- Crecimiento del 30%
- Tolerancia a falla de un enlace Leaf–Spine
- Sobresuscripción máxima objetivo de 3:1

</div>

<div class="border rounded-lg p-4">

### Recursos

- Leaf: 48 × 25 Gb/s y 8 × 100 Gb/s
- Spine: 32 × 100 Gb/s
- Underlay: eBGP u OSPF
- Segmentos: gestión, web, app, BD, backup y storage

</div>

</div>

---

# Tareas de diseño I

1. Definir el número de leafs, spines y enlaces necesarios.
2. Calcular capacidad hacia servidores y uplinks por leaf.
3. Calcular la sobresuscripción por leaf.
4. Determinar el crecimiento posible sin modificar el número de spines.

> Expliciten supuestos de puertos, velocidades, dual-homing y reserva de capacidad.

---

# Tareas de diseño II

5. Proponer prefijos IPv4 e IPv6 para underlay, loopbacks y servicios.
6. Identificar dominios de falla físicos, eléctricos, lógicos y operativos.
7. Justificar EVPN multihoming, MLAG u otra opción de conectividad.
8. Definir métricas: pérdida, latencia, utilización, errores, convergencia, BGP y disponibilidad.

---

# Entregables

<div class="grid grid-cols-2 gap-x-10 text-left text-sm">

<div>

- Diagrama lógico y físico
- Tabla de puertos y capacidad
- Plan IP documentado

</div>

<div>

- Matriz de dominios de falla
- Justificación arquitectónica: máximo 1.500 palabras
- Plan de pruebas de falla y recuperación

</div>

</div>

<div class="mt-6 text-sm opacity-75">
Trabajo en clase: 60 minutos. Defensa técnica: 10–12 minutos por grupo.
</div>

---

# Rúbrica de evaluación

| Dimensión | Peso |
|---|---:|
| Corrección técnica | 25% |
| Justificación y trade-offs | 20% |
| Capacidad, escalabilidad y disponibilidad | 15% |
| Seguridad y segmentación | 15% |
| Dominios de falla y pruebas | 10% |
| Documentación y trazabilidad | 10% |
| Automatización, IPAM y observabilidad | 5% |

---

# Ideas clave

<v-clicks>

- Un centro de datos es un sistema de sistemas
- La arquitectura responde a tráfico, negocio y operación
- Spine–Leaf favorece ECMP y tráfico East–West
- VXLAN encapsula; EVPN puede controlar el overlay
- Redundancia no equivale automáticamente a disponibilidad
- IPAM, automatización y observabilidad son capacidades operativas
- Las decisiones deben declarar supuestos, riesgos y trade-offs

</v-clicks>

---

# Referencias recomendadas

<div class="text-left text-sm leading-6">

- Uptime Institute — *Tier Standard: Topology*
- ANSI/TIA-942-C — *Telecommunications Infrastructure Standard for Data Centers*
- IETF RFC 7348 — *Virtual eXtensible Local Area Network (VXLAN)*
- IETF RFC 7432 — *BGP MPLS-Based Ethernet VPN*
- ISO/IEC 22237 — *Data centre facilities and infrastructures*
- ISO/IEC 27001 — *Information security management systems*
- IETF RFC 1918 — *Address Allocation for Private Internets*
- IETF RFC 4193 — *Unique Local IPv6 Unicast Addresses*

</div>

---
layout: end
---

# Pregunta de discusión

¿Qué arquitectura propondría para una organización con:

- Tráfico East–West predominante
- Crecimiento esperado del 50%
- Disponibilidad crítica
- Presupuesto limitado
- Equipo operativo pequeño

<div class="mt-8 text-sm opacity-70">
Universidad Nacional de Colombia · Redes de Datos · Unidad 1
</div>
