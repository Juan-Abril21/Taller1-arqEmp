# 📊 Modelo BPMN - Proceso de Compra de Mercancías

Este documento contiene los diagramas BPMN del proceso de compra de mercancías, modelados según el ejemplo de la Clínica Salud Viva y adaptado a un proceso de gestión de inventarios y compras.

---

## 🔄 Proceso completo: Gestión de Compra de Mercancías

El siguiente diagrama muestra el proceso completo dividido en tres carriles (swimlanes):
1. **Gestión de incidentes** - Manejo de pedidos de compra con validaciones de seguridad
2. **Proceso de compra de mercancías** - Flujo principal de compra con gestión de inventarios
3. **Gestión financiera** - Procesamiento de pagos y actualización de estados

---

## 📍 Diagrama 1: Gestión de Incidentes

Este proceso maneja la recepción y validación de pedidos de compra.

```mermaid
graph LR
    A((Inicio del evento)) --> B["⚠️ Capturar la<br/>demanda de<br/>pedidos de compra"]
    B --> C["📋 Registrar y<br/>verificar el<br/>pedido"]
    C --> D{"🔍 Juicio de seguridad"}
    D -->|Seguridad| E["📧 Mensaje de pedido<br/>de compra"]
    D -->|Inseguro| F["⚠️ Lanzar mensaje de<br/>excepción de pedido"]
    E --> G((Fin))
    F --> H((Terminar la licencia))
    
    style A fill:#2ecc71,stroke:#27ae60,stroke-width:3px
    style C fill:#3498db,stroke:#2980b9,stroke-width:2px
    style D fill:#95a5a6,stroke:#7f8c8d,stroke-width:2px
    style E fill:#e74c3c,stroke:#c0392b,stroke-width:2px
    style F fill:#f1c40f,stroke:#f39c12,stroke-width:2px
    style G fill:#e74c3c,stroke:#c0392b,stroke-width:3px
    style H fill:#e74c3c,stroke:#c0392b,stroke-width:3px
```

**Elementos del proceso:**
- **Evento de inicio**: Captura de la demanda de pedidos
- **Tarea manual**: Registro y verificación del pedido
- **Gateway exclusivo**: Validación de seguridad
- **Eventos de mensaje**: Comunicación de resultados
- **Eventos de fin**: Finalización del proceso

---

## 📦 Diagrama 2: Proceso de Compra de Mercancías

Este es el proceso central que gestiona el inventario y las órdenes de compra.

```mermaid
graph TB
    A((Recibir información<br/>de pedidos de<br/>compra)) --> B["📊 Actualización<br/>de la base<br/>de inventario"]
    B --> C["📧 Capturar mensajes<br/>de pedidos de la<br/>tienda"]
    B -.Información de<br/>inventarios incorrecta.-> D["⚠️ Error de<br/>manejo"]
    C --> E{"💎 Inventario de<br/>evaluación"}
    E -->|Satisface| F["📦 Paquete de<br/>mercancías"]
    F --> G["📤 Salida de<br/>mercancías"]
    G --> H["📧 Recibir aviso de<br/>cancelación del<br/>envío"]
    H --> I((Señal de salida de<br/>mercancías))
    E -->|No satisface| J["⚠️ Emitir señal de en<br/>stock insuficiente de<br/>productos"]
    J --> K{"➕ Puerta de enlace en<br/>paralelo"}
    K --> L["📦 Aprobar<br/>mercancías"]
    L --> M((Cancelar señal de<br/>envío))
    
    style A fill:#2ecc71,stroke:#27ae60,stroke-width:3px
    style B fill:#f1c40f,stroke:#f39c12,stroke-width:2px
    style D fill:#f1c40f,stroke:#f39c12,stroke-width:2px
    style E fill:#95a5a6,stroke:#7f8c8d,stroke-width:2px
    style F fill:#3498db,stroke:#2980b9,stroke-width:2px
    style G fill:#3498db,stroke:#2980b9,stroke-width:2px
    style J fill:#f39c12,stroke:#e67e22,stroke-width:2px
    style K fill:#95a5a6,stroke:#7f8c8d,stroke-width:2px
    style I fill:#e74c3c,stroke:#c0392b,stroke-width:3px
    style M fill:#e74c3c,stroke:#c0392b,stroke-width:3px
```

**Elementos clave:**
- **Actualización de inventario**: Tarea automatizada con validación de datos
- **Gateway de decisión**: Evaluación de disponibilidad de inventario
- **Tareas de envío**: Empaquetado y salida de mercancías
- **Gateway paralelo**: Manejo de procesos concurrentes
- **Eventos de error**: Gestión de excepciones

---

## 💰 Diagrama 3: Gestión Financiera

Proceso de finalización con manejo de pagos y actualización de estados.

```mermaid
graph LR
    A((Recibir señal de<br/>salida de mercancías)) --> B["📋 Tarea del<br/>sistema"]
    B --> C["💳 Desembolsar<br/>reembolsos"]
    C --> D["⏱️ Esperar 30 segundos"]
    D --> E["📊 Actualización<br/>del estado<br/>del pedido"]
    E --> F((Finalizar el evento))
    
    style A fill:#2ecc71,stroke:#27ae60,stroke-width:3px
    style B fill:#f1c40f,stroke:#f39c12,stroke-width:2px
    style C fill:#3498db,stroke:#2980b9,stroke-width:2px
    style D fill:#9b59b6,stroke:#8e44ad,stroke-width:2px
    style E fill:#f1c40f,stroke:#f39c12,stroke-width:2px
    style F fill:#e74c3c,stroke:#c0392b,stroke-width:3px
```

**Componentes:**
- **Evento de señal**: Recepción de confirmación de envío
- **Tareas de sistema**: Procesamiento automatizado
- **Evento de tiempo**: Espera de 30 segundos para sincronización
- **Actualización de estado**: Registro del pedido completado

---

## 🗺️ Diagrama Integrado: Todos los Procesos en Swimlanes

El siguiente diagrama muestra cómo los tres procesos se integran en un flujo completo:

```mermaid
graph TB
    subgraph "Gestión de incidentes"
        A1((Inicio)) --> A2["⚠️ Capturar demanda"]
        A2 --> A3["📋 Registrar pedido"]
        A3 --> A4{"🔍 Juicio seguridad"}
        A4 -->|Seguridad| A5["📧 Mensaje pedido"]
        A4 -->|Inseguro| A6["⚠️ Excepción"]
        A5 --> A7((Fin))
        A6 --> A8((Terminar))
    end
    
    subgraph "Gestión de almacenes"
        B1((Info pedidos)) --> B2["📊 Actualizar inventario"]
        B2 --> B3["📧 Capturar mensajes"]
        B2 -.Error.-> B4["⚠️ Error manejo"]
        B3 --> B5{"💎 Evaluar inventario"}
        B5 -->|OK| B6["📦 Empaquetar"]
        B6 --> B7["📤 Salida mercancías"]
        B7 --> B8["📧 Aviso cancelación"]
        B8 --> B9((Señal salida))
        B5 -->|Stock bajo| B10["⚠️ Stock insuficiente"]
        B10 --> B11{"➕ Paralelo"}
        B11 --> B12["📦 Aprobar"]
        B12 --> B13((Cancelar))
    end
    
    subgraph "Gestión financiera"
        C1((Señal entrada)) --> C2["📋 Tarea sistema"]
        C2 --> C3["💳 Desembolsar"]
        C3 --> C4["⏱️ Esperar 30s"]
        C4 --> C5["📊 Actualizar estado"]
        C5 --> C6((Fin))
    end
    
    A5 -.Mensaje.-> B1
    B9 -.Señal.-> C1
    
    style A1 fill:#2ecc71,stroke:#27ae60,stroke-width:3px
    style A3 fill:#3498db,stroke:#2980b9,stroke-width:2px
    style A4 fill:#95a5a6,stroke:#7f8c8d,stroke-width:2px
    style A7 fill:#e74c3c,stroke:#c0392b,stroke-width:3px
    
    style B2 fill:#f1c40f,stroke:#f39c12,stroke-width:2px
    style B5 fill:#95a5a6,stroke:#7f8c8d,stroke-width:2px
    style B6 fill:#3498db,stroke:#2980b9,stroke-width:2px
    style B7 fill:#3498db,stroke:#2980b9,stroke-width:2px
    
    style C2 fill:#f1c40f,stroke:#f39c12,stroke-width:2px
    style C3 fill:#3498db,stroke:#2980b9,stroke-width:2px
    style C4 fill:#9b59b6,stroke:#8e44ad,stroke-width:2px
    style C6 fill:#e74c3c,stroke:#c0392b,stroke-width:3px
```

---

## 📋 Leyenda de Elementos BPMN

| Símbolo | Tipo | Significado | Color |
|---------|------|-------------|-------|
| ⭕ Círculo verde | Evento de inicio | Inicia el proceso | Verde |
| 🔴 Círculo rojo | Evento de fin | Termina el proceso | Rojo |
| 📋 Rectángulo azul | Tarea | Actividad a realizar | Azul |
| 📋 Rectángulo amarillo | Tarea del sistema | Actividad automatizada | Amarillo |
| 💎 Rombo | Gateway exclusivo | Decisión (XOR) | Gris |
| ➕ Rombo con + | Gateway paralelo | Procesos concurrentes | Gris |
| 📧 Sobre | Evento de mensaje | Recepción/envío de mensaje | Rojo |
| ⚠️ Triángulo | Evento de error | Manejo de excepciones | Amarillo |
| ⏱️ Reloj | Evento de tiempo | Temporizador | Morado |

---

## 🎯 Análisis del Proceso

### Actores involucrados:
1. **Sistema de gestión de incidentes**: Valida y registra pedidos
2. **Gestión de almacenes**: Controla inventario y despacho
3. **Sistema financiero**: Procesa pagos y actualizaciones

### Puntos críticos identificados:
- ✅ Validación de seguridad en pedidos
- ✅ Verificación de inventario disponible
- ⚠️ Manejo de errores en actualización de inventario
- ⚠️ Gestión de stock insuficiente

### Decisiones principales:
1. **Juicio de seguridad**: Determina si el pedido es válido
2. **Evaluación de inventario**: Verifica disponibilidad de productos
3. **Gateway paralelo**: Permite procesos concurrentes para eficiencia

---

*Diagrama creado para el Taller 1 de Arquitectura Empresarial - Universidad de La Sabana*
