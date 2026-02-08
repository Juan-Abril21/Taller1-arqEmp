# 🗒️ Registro de Trabajo en Clase - Taller 1

## 📆 Fecha de la sesión
7 de febrero de 2026

## 👥 Integrantes presentes
- [Jose  Guzman]
- [Juan Abril]
- [Bryam Diaz]

---

## 🧠 Actividades realizadas en clase

Durante la sesión de clase se trabajó en el modelado del **proceso de agendamiento de citas médicas** para la **Clínica Salud Viva**, caso base de referencia del taller.

### ¿Qué se discutió con el equipo?

- **Análisis del contexto**: La Clínica Salud Viva es una institución médica de tamaño medio que ofrece atención presencial y virtual
- **Identificación del proceso**: Agendamiento de citas médicas a través de plataforma digital
- **Actores identificados**:
  - **Paciente**: Usuario final que solicita la cita médica
  - **APP Web**: Sistema digital de agendamiento y validación de citas
  - **Sistema de Notificaciones**: Módulo encargado de enviar confirmaciones vía email/SMS
- **Flujo principal discutido**: Selección de especialidad → Consulta de disponibilidad → Validación → Confirmación

### ¿Qué decisiones de modelado se tomaron?

1. **Uso de swimlanes (carriles)**: Se decidió dividir el proceso en 3 carriles para separar responsabilidades:
   - **Paciente**: Acciones del usuario (llenar datos, escoger especialidad, recibir notificación)
   - **APP Web**: Lógica de agendamiento, validación de disponibilidad y registro en base de datos
   - **Sistema de Notificaciones**: Generación y envío de confirmaciones

2. **Gateways (compuertas de decisión) identificados**:
   - **¿Especialista disponible?** (Gateway Exclusivo - XOR): Valida si hay médicos con cupos disponibles
   - **¿Información del registro válida?** (Gateway Exclusivo - XOR): Verifica que los datos del paciente sean correctos antes de registrar
   - **Canal de notificación** (Gateway Exclusivo - XOR): Determina si se envía por Email o SMS

3. **Manejo de excepciones**:
   - Flujo alternativo cuando especialista no está disponible: "Mostrar mensaje error médico no disponible"
   - Validación de datos antes de registrar: "Mostrar mensaje error de validación"
   - Retorno al inicio para que el paciente intente nuevamente

4. **Comunicación entre carriles**: 
   - El flujo muestra claramente las interacciones entre los 3 actores
   - Las flechas representan el paso de información entre sistemas
   - Se mantiene la secuencia lógica del proceso

### ¿Qué herramientas se usaron?

- **Herramienta de modelado BPMN**: Para crear el diagrama profesional `BPMN.jpg`
- **Notación estándar BPMN 2.0**: Uso de eventos, actividades, gateways y swimlanes
- **Documentación**: Markdown para registro de notas y análisis

### ¿Qué parte del trabajo se alcanzó a desarrollar?

- ✅ Identificación completa del flujo del proceso de agendamiento
- ✅ Definición de los 3 carriles (swimlanes): Paciente, APP Web, Sistema de Notificaciones
- ✅ Identificación de eventos de inicio y fin en cada carril
- ✅ Mapeo de 10 actividades principales del proceso
- ✅ Definición de 3 gateways de decisión (compuertas exclusivas XOR)
- ✅ Identificación y documentación de flujos alternativos (manejo de errores)
- ✅ Creación del diagrama BPMN completo y digitalizado

---

## 🧩 Diagrama BPMN del Proceso

El diagrama completo se encuentra en el archivo `BPMN.jpg` de esta carpeta.

### Descripción detallada del flujo:

**Carril 1: Paciente**
```
[Inicio] → Llena los datos personales y escoge especialidad → 
Escoge especialista → [espera validación del sistema] → 
Recibir notificación → [Fin]
```

**Carril 2: APP Web**
```
[Recibir solicitud] → Consultar disponibilidad de especialistas → 

  Gateway XOR: ¿Especialista disponible?
    ↓ [No] → Mostrar mensaje error médico no disponible → [retorno al inicio]
    ↓ [Sí] → Continuar
  
  Mostrar fechas y horarios disponibles → 
  Validar información del registro →
  
  Gateway XOR: ¿Información del registro válida?
    ↓ [No] → Mostrar mensaje error de validación → [retorno a validar]
    ↓ [Sí] → Continuar
  
  Registrar cita en base de datos → 
  Enviar notificación al Sistema de Notificaciones
```

**Carril 3: Sistema de Notificaciones**
```
[Recibir solicitud de notificación] → 
Generar mensaje de confirmación →

  Gateway XOR: Canal de notificación
    ↓ Email → Enviar notificación por Email
    ↓ SMS → Enviar notificación por SMS
  
  → Enviar notificación al usuario → [Fin]
```


### Puntos críticos identificados:

1. **Validación de disponibilidad en tiempo real**: El sistema debe consultar la base de datos para verificar que el especialista tenga cupos disponibles
2. **Validación de datos del registro**: Antes de confirmar la cita, se verifica que la información del paciente sea correcta y completa
3. **Manejo de errores con retroalimentación**: Cuando hay un error (médico no disponible o datos inválidos), el sistema muestra mensajes claros y permite reintentar
4. **Notificación multicanal**: El sistema puede enviar confirmación por email o SMS según la preferencia del usuario

---

## 📋 Elementos BPMN identificados en el diagrama

| Elemento BPMN | Cantidad | Ubicación en el diagrama |
|---------------|----------|--------------------------|
| **Eventos de inicio** ⭕ | 3 | Uno al inicio de cada carril (Paciente, APP Web, Sistema de Notificaciones) |
| **Eventos de fin** 🔴 | 3 | Uno al final de cada carril |
| **Actividades/Tareas** 📋 | 10 | Distribuidas en los 3 carriles |
| **Gateways Exclusivos (XOR)** 💎 | 3 | - ¿Especialista disponible?<br>- ¿Información del registro válida?<br>- Canal de notificación (Email/SMS) |
| **Flujos de secuencia** → | 18+ | Conectando todas las actividades |
| **Swimlanes (Carriles)** 🏊 | 3 | Paciente, APP Web, Sistema de Notificaciones |

### Detalles de las actividades por carril:

**Paciente (2 actividades):**
- Llena los datos personales y escoge especialidad
- Recibir notificación

**APP Web (6 actividades):**
- Consultar disponibilidad de especialistas
- Mostrar mensaje error médico no disponible *(flujo alternativo)*
- Mostrar fechas y horarios disponibles
- Validar información del registro
- Mostrar mensaje error de validación *(flujo alternativo)*
- Registrar cita en base de datos

**Sistema de Notificaciones (2 actividades principales):**
- Generar mensaje de confirmación
- Enviar notificación usuario (por Email o SMS)

---

## 🎯 Aprendizajes de la sesión

- Comprensión de la notación BPMN 2.0 y sus elementos básicos
- Uso de **swimlanes** para separar responsabilidades entre actores del proceso
- Identificación y uso correcto de **gateways exclusivos (XOR)** para representar decisiones binarias
- Diseño de **flujos alternativos** para manejo de excepciones y errores
- Importancia de la validación en múltiples etapas del proceso
- Aplicación práctica de BPMN a un caso real del sector salud
- Modelado de procesos digitales que integran múltiples sistemas

---

_Este documento resume el trabajo colaborativo realizado durante la sesión del Taller 1 en el curso de Arquitectura Empresarial - Universidad de La Sabana._
