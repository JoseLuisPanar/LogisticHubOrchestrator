# Arquitectura y convenciones de código

## Backend (.NET 10 / Clean Architecture)

### Capas y dependencias
```
Api            → controllers, middlewares, DI, configuración
Infrastructure → EF Core, repositorios, servicios externos, Identity
Application    → casos de uso, CQRS (commands/queries), DTOs, validadores
Domain         → entidades, value objects, reglas de negocio, sin dependencias externas
```
Regla de dependencia: `Api → Infrastructure → Application → Domain`. Domain no referencia ninguna otra capa. Application no referencia Infrastructure ni Api.

### Convenciones de nombres
- Proyectos: `LogisticsHubOrchestrator.Domain`, `LogisticsHubOrchestrator.Application`, `LogisticsHubOrchestrator.Infrastructure`, `LogisticsHubOrchestrator.Api`.
- Carpetas dentro de Application por feature (ej. `Shipments/Commands/CreateShipment`), no por tipo técnico.
- Entidades en singular (`Shipment`, no `Shipments`).
- Interfaces con prefijo `I` (`IShipmentRepository`).
- DTOs con sufijo `Dto` o `Response`/`Request` según uso.

### Persistencia
- EF Core 10 con migraciones versionadas en `Infrastructure/Persistence/Migrations`.
- No se generan migraciones directamente contra la base de datos de producción.
- Nombres de tablas en `snake_case` (convención habitual de PostgreSQL).

### Autenticación
- JWT emitido por ASP.NET Core Identity.
- Los claims y roles se definen en `Infrastructure/Identity`, nunca hardcodeados en controllers.

## Frontend (React 18 + Vite 8)
- Componentes funcionales con hooks, sin componentes de clase.
- Organización por features (`src/features/<nombre>`), no por tipo (`components/`, `hooks/` sueltos a nivel global).
- Llamadas a la API centralizadas en una capa `src/api/`, no fetch disperso en componentes.
- Tipado con TypeScript si el proyecto lo adopta (a confirmar).

## Versionado y dependencias
- Las versiones mayores del stack (.NET 10, React 18, Vite 8, PostgreSQL 17/18, EF Core 10) son fijas para este proyecto; cualquier upgrade mayor requiere decisión explícita del autor, no debe hacerse de forma automática.

## Commits
- Mensajes en formato Conventional Commits (`feat:`, `fix:`, `refactor:`, `docs:`, `chore:`, `test:`).
- Un commit por cambio lógico; evitar commits mezclando backend y frontend salvo que sea un mismo cambio funcional.
