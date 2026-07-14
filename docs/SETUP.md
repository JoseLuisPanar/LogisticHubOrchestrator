# Arranque rápido en local

## Requisitos previos
- .NET 10 SDK
- Node.js (compatible con Vite 8) + npm/pnpm
- PostgreSQL 17 o 18 en local o vía Docker

## Base de datos
```bash
# Ejemplo con Docker
docker run --name logistichub-db -e POSTGRES_PASSWORD=postgres -p 5432:5432 -d postgres:17
```
Configurar la cadena de conexión en `src/backend/Api/appsettings.Development.json` (no commitear credenciales reales).

## Backend
```bash
cd src/backend
dotnet restore
dotnet ef database update --project Infrastructure --startup-project Api
dotnet run --project Api
```

## Frontend
```bash
cd src/frontend
npm install
npm run dev
```

## Variables de entorno
Definir en `.env` (no versionado) al menos:
- Cadena de conexión a PostgreSQL
- Clave/secret para firma de JWT
- URL base de la API para el frontend
