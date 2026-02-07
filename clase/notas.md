# 🗒️ Registro de Trabajo en Clase - Taller 1

## 📆 Fecha de la sesión
_[Completar con la fecha de la clase]_

## 👥 Integrantes presentes
- [Nombre 1]
- [Nombre 2]
- [Nombre 3]

---

## 🧠 Actividades realizadas en clase

Durante la sesión de clase se trabajó en el modelado del **proceso de agendamiento de citas médicas** para la **Clínica Salud Viva**, caso base de referencia del taller.

### ¿Qué se discutió con el equipo?

- **Análisis del contexto**: La Clínica Salud Viva es una institución médica de tamaño medio que ofrece atención presencial y virtual
- **Identificación del proceso**: Agendamiento de citas médicas a través de plataforma digital
- **Actores identificados**:
  - Paciente (usuario final)
  - Sistema de citas (plataforma digital)
  - Sistema de notificaciones (email/SMS)
- **Flujo principal discutido**: Selección de especialidad → Médico → Fecha → Confirmación

### ¿Qué decisiones de modelado se tomaron?

1. **Uso de swimlanes**: Se decidió dividir el proceso en 3 carriles para separar responsabilidades:
   - **Paciente**: Acciones del usuario
   - **Sistema de Citas**: Lógica de agendamiento y validación
   - **Sistema de Notificaciones**: Envío de confirmaciones

2. **Gateways identificados**:
   - ¿Médico disponible? (Exclusivo - XOR)
   - ¿Datos válidos? (Exclusivo - XOR)
   - Canal de notificación: Email o SMS (Exclusivo - XOR)

3. **Manejo de excepciones**:
   - Flujo alternativo cuando médico no está disponible
   - Validación de datos antes de registrar la cita
   - Sugerencias de médicos alternativos

4. **Eventos de mensaje**: Para representar la comunicación entre:
   - Paciente → Sistema de citas
   - Sistema de citas → Sistema de notificaciones
   - Sistema de notificaciones → Paciente

### ¿Qué herramientas se usaron?

- **Boceto inicial**: Pizarra y papel para discutir el flujo
- **Digitalización**: Mermaid (diagramas como código en formato markdown)
- **Documentación**: Markdown para registro de notas
- **Código de colores**: Aplicado para diferenciar tipos de elementos BPMN

### ¿Qué parte del trabajo se alcanzó a desarrollar?

- ✅ Identificación completa del flujo del proceso
- ✅ Definición de los 3 carriles (swimlanes)
- ✅ Identificación de eventos de inicio y fin
- ✅ Mapeo de actividades principales (12 tareas)
- ✅ Definición de decisiones (3 gateways)
- ✅ Identificación de flujos alternativos
- ✅ Digitalización del diagrama BPMN en Mermaid

---

## 🧩 Boceto inicial del modelo

### Flujo principal identificado:

**Carril 1: Paciente**
```
Inicio → Ingresar a plataforma → Seleccionar especialidad → 
Seleccionar médico → Recibir confirmación → Fin
```

**Carril 2: Sistema de Citas**
```
Recibir solicitud → Consultar disponibilidad → 
¿Médico disponible? [Sí/No] →
  [Sí] → Mostrar fechas → Validar datos → ¿Datos válidos? [Sí/No] →
    [Sí] → Registrar cita → Enviar notificación → Fin
    [No] → Mostrar error → Reintentar
  [No] → Sugerir otros médicos → Retornar
```

**Carril 3: Sistema de Notificaciones**
```
Recibir solicitud → Generar mensaje → 
Canal [Email/SMS] →
  [Email] → Enviar correo electrónico → Confirmar envío → Fin
  [SMS] → Enviar mensaje de texto → Confirmar envío → Fin
```

### Puntos críticos identificados:

1. **Validación de disponibilidad**: El sistema debe verificar en tiempo real que el médico tenga cupos
2. **Validación de datos**: Antes de registrar, se verifica que la información del paciente sea correcta
3. **Notificación dual**: El sistema puede enviar confirmación por email o SMS según preferencia

---

## 📋 Elementos BPMN identificados en el proceso

| Elemento | Tipo | Cantidad | Ubicación |
|----------|------|----------|-----------|
| Eventos de inicio | ⭕ | 3 | Inicio de cada carril |
| Eventos de fin | 🔴 | 5 | Finales múltiples |
| Tareas manuales | 📋 | 9 | Acciones del paciente y sistema |
| Tareas del sistema | 📊 | 3 | Procesos automatizados |
| Gateways exclusivos | 💎 | 3 | Decisiones binarias |
| Eventos de mensaje | 📧 | 4 | Comunicación entre carriles |

---

## 🔁 Tareas definidas para complementar el taller

| Tarea asignada | Responsable | Fecha estimada |
|----------------|-------------|----------------|
| Revisar y validar el diagrama BPMN del caso base | [Nombre] | [Fecha] |
| Identificar cliente real para aplicación del modelo | [Nombre] | [Fecha] |
| Adaptar modelo BPMN al cliente real | [Nombre] | [Fecha] |
| Redacción del informe técnico | [Nombre] | [Fecha] |
| Investigación sobre buenas prácticas BPMN | [Nombre] | [Fecha] |
| Compilación de referencias bibliográficas | [Nombre] | [Fecha] |
| Revisión final del trabajo de clase | Equipo completo | [Fecha] |

---

## 📝 Observaciones y retroalimentación del docente

_Espacio para anotar comentarios recibidos durante la clase:_

- 
- 
- 

---

## 🎯 Aprendizajes de la sesión

- Comprensión de la notación BPMN 2.0 y sus elementos básicos
- Uso de swimlanes para separar responsabilidades entre actores
- Identificación de gateways para representar decisiones
- Uso de eventos de mensaje para comunicación entre procesos
- Importancia de definir flujos alternativos y manejo de excepciones
- Aplicación práctica de BPMN a un caso real de salud

---

_Este documento resume el trabajo colaborativo realizado durante la sesión del Taller 1 en el curso AREM - Universidad de La Sabana._
