# 📊 Modelo BPMN - Agendamiento de Citas Médicas
## Clínica Salud Viva

Este documento contiene el diagrama BPMN del proceso de agendamiento de citas médicas para la Clínica Salud Viva, modelado según la notación BPMN 2.0.

---

## 🧠 Contexto del Proceso

La Clínica Salud Viva es una institución médica de tamaño medio que ofrece atención presencial y virtual. El proceso de agendamiento permite a los pacientes:
- Seleccionar especialidad médica
- Elegir médico disponible
- Agendar fecha y hora
- Recibir confirmación vía correo/SMS

---

## 🗺️ Diagrama BPMN Completo

### Proceso con Swimlanes (3 Carriles)

```mermaid
graph TB
    subgraph paciente["👤 Paciente"]
        direction LR
        A1((Inicio:<br/>Necesidad de<br/>atención médica)) --> A2["📱 Ingresar a<br/>plataforma de<br/>citas"]
        A2 --> A3["🏥 Seleccionar<br/>especialidad"]
        A3 --> A4["👨‍⚕️ Seleccionar<br/>médico"]
        A4 --> A5["📧 Recibir<br/>confirmación"]
        A5 --> A6((Fin:<br/>Cita agendada))
    end
    
    subgraph sistema["💻 Sistema de Citas"]
        direction TB
        B1((Recibir solicitud<br/>de agendamiento)) --> B2["📊 Consultar<br/>disponibilidad<br/>de médicos"]
        B2 --> B3{"🔍 ¿Médico<br/>disponible?"}
        B3 -->|Sí| B4["📅 Mostrar fechas<br/>y horarios<br/>disponibles"]
        B3 -->|No| B5["⚠️ Mostrar mensaje:<br/>Médico no disponible"]
        B5 --> B6["🔄 Sugerir otros<br/>médicos"]
        B6 -.Retornar.-> B2
        B4 --> B7["✅ Validar y<br/>reservar horario"]
        B7 --> B8{"💾 ¿Datos<br/>válidos?"}
        B8 -->|Sí| B9["📝 Registrar cita<br/>en base de datos"]
        B8 -->|No| B10["❌ Mostrar error<br/>de validación"]
        B10 -.Reintentar.-> B7
        B9 --> B11["📤 Enviar solicitud<br/>de notificación"]
        B11 --> B12((Cita registrada))
    end
    
    subgraph notificaciones["📬 Sistema de Notificaciones"]
        direction LR
        C1((Recibir solicitud<br/>de notificación)) --> C2["📋 Generar<br/>mensaje de<br/>confirmación"]
        C2 --> C3{"📨 Canal de<br/>notificación"}
        C3 -->|Email| C4["📧 Enviar correo<br/>electrónico"]
        C3 -->|SMS| C5["📱 Enviar mensaje<br/>de texto"]
        C4 --> C6["✅ Confirmar envío"]
        C5 --> C6
        C6 --> C7((Notificación<br/>enviada))
    end
    
    A4 -.Solicitud.-> B1
    B11 -.Datos.-> C1
    C6 -.Confirmación.-> A5
    
    style A1 fill:#2ecc71,stroke:#27ae60,stroke-width:3px,color:#fff
    style A2 fill:#3498db,stroke:#2980b9,stroke-width:2px,color:#fff
    style A3 fill:#3498db,stroke:#2980b9,stroke-width:2px,color:#fff
    style A4 fill:#3498db,stroke:#2980b9,stroke-width:2px,color:#fff
    style A5 fill:#e74c3c,stroke:#c0392b,stroke-width:2px,color:#fff
    style A6 fill:#e74c3c,stroke:#c0392b,stroke-width:3px,color:#fff
    
    style B1 fill:#2ecc71,stroke:#27ae60,stroke-width:3px,color:#fff
    style B2 fill:#f1c40f,stroke:#f39c12,stroke-width:2px,color:#000
    style B3 fill:#95a5a6,stroke:#7f8c8d,stroke-width:2px,color:#fff
    style B4 fill:#3498db,stroke:#2980b9,stroke-width:2px,color:#fff
    style B5 fill:#f39c12,stroke:#e67e22,stroke-width:2px,color:#fff
    style B6 fill:#3498db,stroke:#2980b9,stroke-width:2px,color:#fff
    style B7 fill:#3498db,stroke:#2980b9,stroke-width:2px,color:#fff
    style B8 fill:#95a5a6,stroke:#7f8c8d,stroke-width:2px,color:#fff
    style B9 fill:#f1c40f,stroke:#f39c12,stroke-width:2px,color:#000
    style B10 fill:#f39c12,stroke:#e67e22,stroke-width:2px,color:#fff
    style B11 fill:#e74c3c,stroke:#c0392b,stroke-width:2px,color:#fff
    style B12 fill:#e74c3c,stroke:#c0392b,stroke-width:3px,color:#fff
    
    style C1 fill:#2ecc71,stroke:#27ae60,stroke-width:3px,color:#fff
    style C2 fill:#f1c40f,stroke:#f39c12,stroke-width:2px,color:#000
    style C3 fill:#95a5a6,stroke:#7f8c8d,stroke-width:2px,color:#fff
    style C4 fill:#3498db,stroke:#2980b9,stroke-width:2px,color:#fff
    style C5 fill:#3498db,stroke:#2980b9,stroke-width:2px,color:#fff
    style C6 fill:#3498db,stroke:#2980b9,stroke-width:2px,color:#fff
    style C7 fill:#e74c3c,stroke:#c0392b,stroke-width:3px,color:#fff
```

---

## 📋 Descripción de Cada Carril

### 1️⃣ Paciente

**Rol**: Usuario que necesita atención médica

**Flujo**:
1. **Inicio**: El paciente identifica la necesidad de atención médica
2. **Ingresar a plataforma**: Accede al sistema de citas en línea
3. **Seleccionar especialidad**: Elige el tipo de atención necesaria (ej: Cardiología, Pediatría)
4. **Seleccionar médico**: Escoge un médico de la lista disponible
5. **Recibir confirmación**: Obtiene notificación de cita agendada
6. **Fin**: Proceso completado con cita confirmada

---

### 2️⃣ Sistema de Citas

**Rol**: Plataforma digital que gestiona agendamientos

**Flujo principal**:
1. **Recibir solicitud**: Captura la petición del paciente
2. **Consultar disponibilidad**: Verifica médicos disponibles en la especialidad
3. **Gateway de decisión - ¿Médico disponible?**:
   - **Sí**: Muestra fechas y horarios disponibles
   - **No**: Muestra mensaje de no disponibilidad y sugiere otros médicos
4. **Validar y reservar**: El paciente selecciona fecha/hora
5. **Gateway de decisión - ¿Datos válidos?**:
   - **Sí**: Registra la cita en la base de datos
   - **No**: Muestra error de validación y permite reintentar
6. **Enviar solicitud de notificación**: Activa el sistema de notificaciones
7. **Fin**: Cita registrada en el sistema

**Manejo de excepciones**:
- Si no hay médicos disponibles → Sugerir alternativas
- Si datos son inválidos → Permitir corrección

---

### 3️⃣ Sistema de Notificaciones

**Rol**: Servicio de comunicación con pacientes

**Flujo**:
1. **Recibir solicitud**: Obtiene datos de la cita confirmada
2. **Generar mensaje**: Crea texto de confirmación con detalles
3. **Gateway de decisión - Canal de notificación**:
   - **Email**: Envía correo electrónico
   - **SMS**: Envía mensaje de texto
4. **Confirmar envío**: Valida que la notificación fue entregada
5. **Fin**: Notificación enviada exitosamente

---

## 📊 Elementos BPMN Utilizados

| Elemento | Símbolo | Descripción | Cantidad |
|----------|---------|-------------|----------|
| Evento de inicio | ⭕ Verde | Inicio de cada proceso | 3 |
| Evento de fin | 🔴 Rojo | Finalización del proceso | 5 |
| Tarea | 📋 Azul | Actividad manual | 9 |
| Tarea del sistema | 📊 Amarillo | Actividad automatizada | 3 |
| Gateway exclusivo (XOR) | 💎 Gris | Decisión binaria | 3 |
| Evento de mensaje | 📧 Rojo | Comunicación entre procesos | 4 |
| Swimlanes | 🏊 | Separación de responsabilidades | 3 |

**Total de elementos**: 30 elementos BPMN

---

## 🎯 Puntos Críticos del Proceso

### ✅ Validaciones
1. **Disponibilidad de médico**: Verifica que hay cupos disponibles
2. **Validación de datos**: Asegura que información del paciente es correcta

### 🔄 Flujos Alternativos
1. **Médico no disponible**: Sugiere otros médicos en la misma especialidad
2. **Datos inválidos**: Permite corrección y reintento

### 📡 Integraciones
1. **Paciente → Sistema**: Solicitud de agendamiento
2. **Sistema → Notificaciones**: Envío de datos de confirmación
3. **Notificaciones → Paciente**: Confirmación final

---

## 📋 Leyenda de Colores

| Color | Elemento | Significado |
|-------|----------|-------------|
| 🟢 Verde | Evento de inicio | Comienza el proceso |
| 🔴 Rojo | Evento de fin / Mensajes | Termina o comunica |
| 🔵 Azul | Tareas manuales | Requiere acción humana |
| 🟡 Amarillo | Tareas automáticas | Sistema ejecuta |
| ⚪ Gris | Gateways | Decisiones |

---

## 🔍 Análisis del Proceso

### Actores involucrados:
- **Paciente**: Usuario final que agenda la cita
- **Sistema de citas**: Plataforma digital de agendamiento
- **Base de datos**: Almacena información de citas y médicos
- **Sistema de notificaciones**: Servicio de mensajería (email/SMS)

### Interacciones clave:
1. Paciente interactúa con interfaz de usuario
2. Sistema consulta base de datos de disponibilidad
3. Sistema registra cita en base de datos
4. Sistema activa servicio de notificaciones
5. Notificación llega al paciente

### Decisiones (Gateways):
1. **¿Médico disponible?** → Determina si se puede proceder o hay que sugerir alternativas
2. **¿Datos válidos?** → Verifica que la información es correcta antes de registrar
3. **Canal de notificación** → Determina si se envía por email o SMS

---

*Diagrama creado para el Taller 1 de Arquitectura Empresarial - Universidad de La Sabana*  
*Caso base: Clínica Salud Viva - Agendamiento de Citas Médicas*
