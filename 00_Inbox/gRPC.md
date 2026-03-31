---
status: final
tags:
  - backend
  - grpc
  - microservicios
  - protocolos
  - dotnet
  - java
created: 2026-03-31
---
# 📡 [[gRPC]] (Google Remote Procedure Call)

**[[gRPC]]** (Google Remote Procedure Call) es un framework de comunicación de código abierto y alto rendimiento, desarrollado inicialmente por Google. Su objetivo es facilitar la interconexión de servicios (**[[Microservicios]]**) de una manera tan sencilla como si estuvieras llamando a una función local, pero entre máquinas diferentes.

---
## 🏛️ Los Pilares de [[gRPC]]

**[[gRPC]]** se apoya principalmente en dos tecnologías clave que lo diferencian de los servicios web tradicionales:

### 1. Protocol Buffers ([[Protobuf]])
A diferencia de **[[REST]]**, que suele usar **[[JSON]]** o **[[XML]]** (texto plano), **[[gRPC]]** utiliza **[[Protobuf|Protocol Buffers]]** como su lenguaje de definición de interfaz (IDL) y formato de intercambio de mensajes.
* **Binario:** Los datos se serializan en formato binario, lo que los hace mucho más pequeños y rápidos de procesar que el **[[JSON]]**.
* **Tipado fuerte:** Defines tus servicios y mensajes en un archivo `.proto`. A partir de ahí, se genera código automáticamente en el lenguaje que necesites (**[[C#]]**, **[[Java]]**, etc.).

### 2. Basado en [[HTTP-2]]
**[[gRPC]]** utiliza **[[HTTP-2]]** como transporte, lo que le otorga ventajas técnicas inmediatas:
* **Multiplexación:** Permite enviar múltiples peticiones y respuestas simultáneamente a través de una sola conexión **[[TCP]]**.
* **Streaming bidireccional:** Tanto el cliente como el servidor pueden enviar flujos de datos al mismo tiempo.
* **Compresión de cabeceras:** Reduce aún más el tamaño de los paquetes.
---
## ⚖️ [[gRPC]] vs. [[REST]]

| Característica         | [[gRPC]]                                     | [[REST]]                           |
| :--------------------- | :------------------------------------------- | :--------------------------------- |
| **Protocolo de Datos** | **[[Protobuf\|Protocol Buffers]]** (Binario) | **[[JSON]]** / **[[XML]]** (Texto) |
| **Contrato**           | Estricto (archivo `.proto`)                  | Opcional (OpenAPI/Swagger)         |
| **Transporte**         | **[[HTTP-2]]**                               | HTTP 1.1 / **[[HTTP-2]]**          |
| **Rendimiento**        | Muy alto (baja latencia)                     | Medio                              |
| **Navegador**          | Soporte limitado (requiere proxy)            | Soporte nativo total               |
