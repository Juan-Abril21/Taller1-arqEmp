# 🗒️ Registro de Trabajo en Clase - Taller 1

## 📆 Fecha de la sesión
_Febrero 2026_

## 👥 Integrantes presentes
- [Completar con los nombres del equipo]

## 🧠 Actividades realizadas en clase

Durante la sesión de clase se trabajó en el modelado del proceso de agendamiento de citas médicas para la Clínica Salud Viva, que sirvió como caso base de referencia.

### ¿Qué se discutió con el equipo?
- Análisis del flujo del proceso de agendamiento de citas
- Identificación de actores principales: Paciente, Sistema de citas, Base de datos
- Discusión sobre los eventos de inicio y fin del proceso
- Identificación de decisiones críticas en el flujo (disponibilidad de médico, validación de datos)

### ¿Qué decisiones de modelado se tomaron?
- Usar swimlanes (carriles) para diferenciar responsabilidades entre actores
- Incluir eventos de mensaje para notificaciones (correo/SMS)
- Modelar gateways exclusivos para decisiones binarias
- Representar tareas del sistema y tareas manuales de manera diferenciada

### ¿Qué herramientas se usaron?
- Inicialmente: pizarra y papel para bocetos
- Digitalización: Mermaid (diagramas en markdown)
- Documentación: Markdown

### ¿Qué parte del trabajo se alcanzó a desarrollar?
- ✅ Identificación completa del flujo del proceso
- ✅ Boceto inicial del diagrama BPMN
- ✅ Definición de actores y responsabilidades
- ✅ Identificación de puntos críticos del proceso

## 🧩 Boceto inicial del modelo

El proceso de agendamiento se dividió en tres carriles principales:
1. **Paciente**: Inicia la solicitud y recibe confirmación
2. **Sistema de citas**: Valida disponibilidad y procesa la solicitud
3. **Sistema de notificaciones**: Envía confirmaciones

**Flujo principal identificado:**
```
Inicio → Seleccionar especialidad → Seleccionar médico → 
Verificar disponibilidad → Seleccionar fecha/hora → 
Confirmar datos → Registrar cita → Enviar notificación → Fin
```

**Puntos de decisión:**
- ¿Médico disponible? (Sí/No)
- ¿Datos válidos? (Sí/No)
- ¿Confirmación exitosa? (Sí/No)

## 🔁 Tareas definidas para complementar el taller

| Tarea asignada | Responsable | Fecha estimada |
|----------------|-------------|----------------|
| Digitalizar modelo BPMN del caso base | [Nombre] | [Fecha] |
| Adaptar modelo al cliente real | [Nombre] | [Fecha] |
| Redacción del informe técnico | [Nombre] | [Fecha] |
| Investigación sobre buenas prácticas BPMN | [Nombre] | [Fecha] |
| Compilación de referencias bibliográficas | [Nombre] | [Fecha] |
| Revisión final y entrega | Equipo completo | [Fecha] |

## 📝 Observaciones y retroalimentación del docente

_Espacio para anotar comentarios y sugerencias recibidas durante la clase:_

- Asegurarse de usar la notación BPMN correcta para cada elemento
- Mantener el diagrama limpio y legible
- Documentar supuestos tomados durante el modelado
- Incluir manejo de excepciones en el flujo

---

_Este documento resume el trabajo colaborativo realizado durante la sesión del Taller 1 en el curso AREM - Universidad de La Sabana._
