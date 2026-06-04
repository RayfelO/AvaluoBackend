# Arquitectura

## Vision general

El backend de Avaluo esta construido sobre una **arquitectura de capas** (Layered Architecture) con influencias de **Domain Driven Design (DDD)**. Este enfoque garantiza una clara separacion de responsabilidades, facilitando el mantenimiento, la escalabilidad y la comprension del sistema.

## Capas del sistema

### 1. Capa de Presentacion (Presentation Layer)
- **Responsabilidad**: Exponer la API REST a los clientes externos.
- **Componentes**: Controladores ASP.NET Core, ViewModels y filtros de validacion.
- **Regla clave**: No contiene logica de negocio ni acceso directo a datos.

### 2. Capa de Aplicacion (Application Layer)
- **Responsabilidad**: Coordinar operaciones entre las capas y orquestar casos de uso.
- **Componentes**: Servicios de aplicacion, DTOs, middlewares de excepcion y autenticacion.
- **Regla clave**: Conoce el dominio pero no depende de infrastructura concreta.

### 3. Capa de Dominio (Domain Layer)
- **Responsabilidad**: Implementar las reglas de negocio y modelar el core del sistema.
- **Componentes**: Entidades, value objects, abstracciones y servicios de dominio.
- **Regla clave**: Independiente de frameworks y tecnologias de persistencia.

### 4. Capa de Infraestructura (Infrastructure Layer)
- **Responsabilidad**: Proveer implementaciones tecnicas para persistencia, autenticacion e integraciones.
- **Componentes**: DbContext (EF Core + Dapper), repositorios, servicios de email, cache Redis, jobs Quartz y conectores externos (INTEC).
- **Regla clave**: Depende de abstracciones del dominio, no al reves.

## Principios de diseno

- **Separacion de responsabilidades**: Cada capa tiene un proposito unico.
- **Inversion de dependencias**: Las capas dependen de interfaces, no de implementaciones concretas.
- **Desacoplamiento**: Logica de negocio desvinculada de detalles tecnicos para facilitar pruebas y reutilizacion.

## Diagrama de referencia

![Layered Architecture](https://herbertograca.com/wp-content/uploads/2017/07/2010s-layered-architecture.png?w=1100)

> Fuente: [herbertograca.com](https://herbertograca.com/2017/08/03/layered-architecture/)
