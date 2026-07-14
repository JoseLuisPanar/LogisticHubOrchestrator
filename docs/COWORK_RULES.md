# Reglas de trabajo para Cowork en LogisticsHubOrchestrator

Este documento define qué puede y qué no puede hacer Cowork al trabajar en este repositorio de forma autónoma.

## Cowork puede, sin pedir aprobación
- Leer, buscar y explicar código de cualquier capa del repositorio.
- Crear o editar archivos dentro de `src/backend` y `src/frontend` siguiendo las convenciones de [ARCHITECTURE.md](ARCHITECTURE.md).
- Escribir o actualizar tests unitarios y de integración.
- Actualizar documentación (`docs/`, `README.md`) para reflejar cambios ya realizados.
- Ejecutar build, linters y tests en local o en el sandbox.
- Generar migraciones de EF Core en local (no aplicarlas contra bases de datos remotas).

## Cowork necesita aprobación humana explícita antes de
- Aplicar migraciones de base de datos contra cualquier entorno que no sea local/desarrollo.
- Modificar o rotar secretos, cadenas de conexión, claves JWT o configuración de Identity.
- Cambiar dependencias mayores del stack fijado (.NET 10, React 18, Vite 8, PostgreSQL 17/18, EF Core 10) o actualizar de versión mayor cualquier paquete crítico (auth, ORM, framework).
- Modificar pipelines de CI/CD, workflows de despliegue o configuración de infraestructura.
- Hacer push o merge directo sobre ramas protegidas (`main`/`develop`).
- Eliminar archivos o migraciones existentes.

## Cowork nunca debe
- Commitear archivos `.env`, credenciales, certificados o cualquier secreto.
- Ejecutar acciones contra bases de datos de producción.
- Saltarse la capa de validación de Application para acceder directo a Infrastructure desde Api.
- Introducir dependencias del Domain hacia Infrastructure o Api (rompe Clean Architecture).

## Alcance de cambios automáticos
- Los cambios deben limitarse al feature o bug solicitado; evitar refactors amplios no solicitados.
- Si un cambio requiere tocar más de una capa (Domain + Application + Infrastructure + Api), explicitar el motivo antes de aplicarlo.
- Ante ambigüedad sobre una regla de negocio o de arquitectura no cubierta aquí, preguntar antes de asumir.
