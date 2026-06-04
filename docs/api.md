# Guia de la API

## Autenticacion

La API utiliza **JWT Bearer** para autenticacion. Las solicitudes protegidas deben incluir el header:

```http
Authorization: Bearer <token>
```

Ademas, se establece una cookie segura (`X-Permissions`) con los claims de permisos del usuario.

## Documentacion interactiva

Una vez levantado el proyecto, la documentacion interactiva de Swagger UI esta disponible en la raiz del servidor:

```
https://localhost:8000
```

## Endpoints principales

### Dashboard

| Metodo | Endpoint | Descripcion |
|--------|----------|-------------|
| GET | `/api/dashboard/studentOutcomes` | Resumen de Student Outcomes para el coordinador |
| GET | `/api/dashboard/evaluaciones` | Lista paginada de evaluaciones de la carrera |

### Usuarios

| Metodo | Endpoint | Descripcion |
|--------|----------|-------------|
| POST | `/api/usuarios/login` | Autenticacion y obtencion de token |
| GET | `/api/usuarios` | Listado de usuarios |

### Rúbricas y Competencias

| Metodo | Endpoint | Descripcion |
|--------|----------|-------------|
| GET | `/api/rubrica` | Listado de rúbricas |
| GET | `/api/competencias` | Listado de competencias |
| GET | `/api/pi` | Performance Indicators |

### Informes

| Metodo | Endpoint | Descripcion |
|--------|----------|-------------|
| GET | `/api/informes` | Listado de informes generados |
| POST | `/api/informes` | Generar nuevo informe (PDF) |

> Para el listado completo de endpoints, parametros y esquemas, consulta la interfaz de **Swagger UI** en ejecucion.

## Formato de respuestas

Las respuestas JSON utilizan **PascalCase** para las propiedades, manteniendo consistencia con las convenciones de C#.

```json
{
  "Id": 1,
  "Nombre": "Rubrica de Evaluacion",
  "Estado": "Activo"
}
```

## Codigos de estado comunes

| Codigo | Significado |
|--------|-------------|
| 200 | OK |
| 400 | Bad Request (validacion de DTO) |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |
| 500 | Internal Server Error |
