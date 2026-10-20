# API de anime

API REST con Express y PostgreSQL. Incluye catálogo de ejemplo y operaciones para listar, consultar, crear, modificar y eliminar animes.

## Ejecutar con Docker

Desde esta carpeta:

```powershell
docker compose up --build -d
```

API: <http://localhost:3001/api/animes>

Ejemplos:

- `GET /api/animes`
- `GET /api/animes/1`
- `POST /api/animes` con `{ "titulo": "Frieren", "genero": "Fantasía", "anio": 2023, "descripcion": "Una aventura después del final." }`
- `PATCH /api/animes/1` para actualizar campos
- `DELETE /api/animes/1`
- `GET /health`

PostgreSQL escucha localmente en el puerto `5433` y conserva sus datos en el volumen Docker existente `Animes_alan`. Créalo primero en Docker Desktop. Como es un volumen externo, `docker compose down -v` no lo elimina; puedes conservarlo desde Docker Desktop para mantener los datos.

## Desplegar en Render

Sube el repositorio a GitHub y crea un Blueprint en Render indicando el archivo `anime-api/render.yaml`. El Blueprint define la API Docker y una base Render Postgres, conectadas con `DATABASE_URL`. El disco/volumen Docker local solo conserva los datos de tu equipo; Render Postgres conserva los datos desplegados. Consulta [Render Blueprints](https://render.com/docs/blueprint-spec).

La primera inicialización crea la tabla `animes` y carga tres ejemplos solo si aún está vacía.
