# 📄 Informe Técnico del Taller

## 🔖 Nombre del Taller
_Taller 1 - Modelado de Proceso del Cliente con BPMN_

## 👥 Integrantes del equipo
- [Nombre 1] (correo@unisabana.edu.co)
- [Nombre 2] (correo@unisabana.edu.co)
- [Nombre 3] (correo@unisabana.edu.co)

## 🧠 Descripción general del trabajo

El objetivo de este taller fue modelar un proceso de negocio real utilizando la notación BPMN (Business Process Model and Notation). El trabajo se desarrolló en dos fases:

1. **Fase en clase**: Modelado del proceso de agendamiento de citas médicas de la Clínica Salud Viva (caso base)
2. **Fase de aplicación**: Adaptación del modelo a un proceso real de gestión de compra de mercancías

Durante el desarrollo se identificaron eventos de inicio y fin, actividades principales, decisiones (gateways), actores involucrados y puntos críticos del flujo. El trabajo colaborativo permitió comprender la importancia de la notación estándar BPMN para documentar procesos empresariales de manera clara y reproducible.

## 🔧 Proceso de desarrollo

### Decisiones tomadas:
1. **Estructura del modelo**: Se optó por utilizar tres swimlanes (carriles) para diferenciar claramente las responsabilidades:
   - Gestión de incidentes
   - Gestión de almacenes/inventarios
   - Gestión financiera

2. **Herramientas utilizadas**: 
   - Diagramas en formato Mermaid para facilitar el versionamiento y colaboración
   - Markdown para documentación técnica
   - Git para control de versiones

3. **Aspectos modelados primero**:
   - Identificación de actores y roles
   - Definición del flujo principal (happy path)
   - Incorporación de excepciones y manejo de errores
   - Integración entre los diferentes carriles

4. **Ajustes realizados**:
   - Inclusión de eventos de tiempo (espera de 30 segundos)
   - Adición de eventos de error para manejo de excepciones
   - Refinamiento de mensajes entre procesos
   - Diferenciación visual mediante colores para facilitar la comprensión

## 🧩 Análisis del modelo propuesto

### Estructura del modelo:
El modelo se estructura en tres procesos interrelacionados que se ejecutan de manera secuencial y, en algunos casos, paralela:

1. **Gestión de incidentes**: 
   - Captura y valida la demanda de pedidos
   - Incluye un gateway de decisión para validación de seguridad
   - Genera eventos de mensaje o excepciones según el resultado

2. **Gestión de almacenes**:
   - Actualiza el inventario y captura mensajes de pedidos
   - Evalúa la disponibilidad de productos
   - Maneja dos caminos: empaquetado/envío o gestión de stock insuficiente
   - Incluye gateway paralelo para procesos concurrentes

3. **Gestión financiera**:
   - Recibe señal de salida de mercancías
   - Procesa desembolsos y reembolsos
   - Actualiza el estado del pedido
   - Incluye evento de tiempo para sincronización

### Cómo representa las necesidades del cliente:
- **Trazabilidad**: El proceso permite seguir el estado de un pedido desde su inicio hasta su finalización
- **Validación de seguridad**: Asegura que solo pedidos válidos sean procesados
- **Gestión de inventario**: Controla disponibilidad y previene ventas de productos fuera de stock
- **Manejo de excepciones**: Contempla escenarios de error y los gestiona adecuadamente
- **Integración**: Los tres procesos están conectados mediante eventos de mensaje y señales

### Supuestos tomados:
1. Existe un sistema de gestión de inventarios que se actualiza en tiempo real
2. Las validaciones de seguridad se realizan de manera automatizada
3. El tiempo de espera de 30 segundos en gestión financiera es para sincronización con sistemas bancarios
4. Los mensajes entre procesos se transmiten de manera confiable
5. El gateway paralelo permite que ciertas tareas se ejecuten simultáneamente sin bloqueo

## 📈 Diagrama final entregado

Ver archivo: [modelo-bpmn.md](./modelo-bpmn.md)

El diagrama incluye:
- ✅ Eventos de inicio y fin claramente marcados
- ✅ Tareas diferenciadas por tipo (manual, automatizada, del sistema)
- ✅ Gateways exclusivos y paralelos
- ✅ Eventos de mensaje, error y tiempo
- ✅ Código de colores para mejor visualización
- ✅ Leyenda explicativa de elementos BPMN

## 📋 Tabla de actores, entidades o componentes

| Nombre del elemento | Tipo | Descripción | Responsable |
|---------------------|------|-------------|-------------|
| Sistema de gestión de incidentes | Sistema | Valida y registra pedidos de compra | Sistema automático |
| Validador de seguridad | Componente | Evalúa la seguridad de los pedidos | Sistema de seguridad |
| Sistema de inventarios | Sistema | Mantiene registro actualizado de productos | Gestión de almacenes |
| Gestor de mensajes | Componente | Captura y distribuye mensajes entre procesos | Middleware |
| Evaluador de inventario | Componente | Verifica disponibilidad de productos | Sistema de inventarios |
| Sistema de empaquetado | Proceso | Prepara mercancías para envío | Almacén |
| Sistema de envío | Proceso | Gestiona la salida de mercancías | Logística |
| Sistema financiero | Sistema | Procesa pagos y actualizaciones de estado | Contabilidad |
| Procesador de reembolsos | Componente | Gestiona desembolsos y reembolsos | Sistema bancario |
| Actualizador de estados | Componente | Registra cambios de estado de pedidos | Base de datos |

## 🔍 Investigación complementaria

### Tema investigado:
**Buenas prácticas en modelado BPMN y patrones comunes en procesos de compra**

### Resumen:

El modelado BPMN (Business Process Model and Notation) es un estándar ISO para documentar procesos de negocio de manera visual y comprensible. Según la especificación oficial de OMG (Object Management Group), BPMN 2.0 define un conjunto de elementos gráficos que permiten representar procesos complejos de manera clara y precisa.

Las buenas prácticas en BPMN incluyen:
1. **Simplicidad**: Mantener los diagramas lo más simples posible, evitando complejidad innecesaria
2. **Consistencia**: Usar la misma notación para elementos similares en todo el diagrama
3. **Granularidad apropiada**: Definir el nivel de detalle adecuado según la audiencia
4. **Uso correcto de gateways**: Diferenciar entre exclusivos (XOR), inclusivos (OR) y paralelos (AND)
5. **Swimlanes**: Usar carriles para separar responsabilidades entre actores o departamentos

En procesos de compra específicamente, se identifican patrones comunes como:
- **Validación de pedidos**: Verificación de datos y condiciones antes de procesar
- **Verificación de inventario**: Comprobación de disponibilidad antes de comprometer recursos
- **Manejo de excepciones**: Gestión de escenarios de error (stock insuficiente, datos inválidos)
- **Notificaciones**: Comunicación entre sistemas mediante eventos de mensaje
- **Concurrencia**: Uso de gateways paralelos para optimizar tiempos de procesamiento

La investigación también reveló que los procesos de compra bien modelados deben incluir:
- Puntos de sincronización entre diferentes departamentos
- Manejo explícito de errores y excepciones
- Eventos de compensación para deshacer transacciones si es necesario
- Eventos de tiempo para gestionar plazos y timeouts

Estos principios se aplicaron en el modelo propuesto para asegurar que el proceso sea robusto, escalable y fácil de entender para todos los stakeholders.

## 📚 Referencias

1. Object Management Group (OMG). *Business Process Model and Notation (BPMN) Version 2.0*. 2011. [https://www.omg.org/spec/BPMN/2.0/](https://www.omg.org/spec/BPMN/2.0/)

2. Freund, J., & Rücker, B. *Real-Life BPMN: Using BPMN 2.0 to Analyze, Improve, and Automate Processes in Your Company*. Camunda Services GmbH, 2019.

3. Silver, B. *BPMN Method and Style: A Levels-Based Methodology for BPM Process Modeling and Improvement Using BPMN 2.0*. Cody-Cassidy Press, 2011.

4. Chinosi, M., & Trombetta, A. "BPMN: An introduction to the standard". *Computer Standards & Interfaces*, 34(1), 124-134, 2012. DOI: 10.1016/j.csi.2011.06.002

5. Dumas, M., La Rosa, M., Mendling, J., & Reijers, H. *Fundamentals of Business Process Management*. Springer, 2018.

6. Camunda. "BPMN 2.0 Tutorial". [https://camunda.com/bpmn/](https://camunda.com/bpmn/). Consultado: Febrero 2026.

7. BPMNQuickGuide. "BPMN Quick Guide". [http://www.bpmnquickguide.com/](http://www.bpmnquickguide.com/). Consultado: Febrero 2026.

---

_Este documento hace parte de la entrega del Taller 1 del curso AREM (Arquitectura Empresarial) - Universidad de La Sabana._
