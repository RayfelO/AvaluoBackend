# Despliegue local

## Requisitos

- [.NET 8 SDK](https://dotnet.microsoft.com/en-us/download/dotnet/8.0)
- [Docker Desktop](https://www.docker.com/products/docker-desktop/)
- Instancia de **SQL Server** (local, Express o remota)

## Pasos

### 1. Redis (Docker)

El proyecto incluye un `docker-compose.yml` con Redis. En la raiz del repositorio ejecuta:

```bash
docker-compose up -d
```

Esto levantara Redis en `localhost:6379`.

### 2. Base de datos

Asegurate de tener una base de datos SQL Server disponible. Puedes usar **SQL Server Express LocalDB** o una instancia Docker de SQL Server.

### 3. Configuracion de la aplicacion

Copia el archivo de configuracion de ejemplo:

```bash
cp AvaluoAPI/appsettings.example.json AvaluoAPI/appsettings.json
```

Edita `AvaluoAPI/appsettings.json` y completa los valores necesarios:

| Seccion | Descripcion |
|---------|-------------|
| `ConnectionStrings:DefaultConnection` | Cadena de conexion a SQL Server |
| `ConnectionStrings:Redis` | `localhost:6379` (si usaste el compose) |
| `Jwt:Key` | Clave secreta para firmar tokens (minimo 32 caracteres) |
| `Email:FromEmail` | Correo para envio de notificaciones |
| `Email:Password` | Contrasena del correo |
| `IronPdf:LicenseKey` | Licencia de IronPDF (si requieres generacion de PDFs) |

> **Importante**: Nunca commitees valores reales en `appsettings.json`. Usa `appsettings.Development.json` (ya ignorado por `.gitignore`) o variables de entorno.

### 4. Ejecutar

```bash
cd AvaluoAPI
dotnet run
```

La API estara disponible en:

- **API Base**: `https://localhost:8000`
- **Swagger UI**: `https://localhost:8000`

## Solucion de problemas

| Problema | Posible causa | Solucion |
|----------|---------------|----------|
| No se conecta a SQL Server | Cadena de conexion incorrecta | Verificar servidor, nombre de BD y autenticacion |
| Error de Redis | Servicio no levantado | Ejecutar `docker-compose up -d` |
| Swagger no carga | Puerto ocupado o sin HTTPS | Verificar que el puerto 8000 este libre |
| Error de licencia IronPDF | Falta licencia | Ingresar una licencia valida o deshabilitar funciones PDF |
