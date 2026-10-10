# API Biblioteca - BiblioCampus

Servicio web REST en Node.js y Express para gestionar el catalogo, prestamos y devoluciones de libros de BiblioCampus.

## Requisitos

- Node.js 20 o superior
- npm

## Ejecucion local

```bash
npm install
npm start
```

La API queda disponible en:

```text
http://localhost:3000
```

Desde el emulador Android se consume con:

```text
http://10.0.2.2:3000
```

## Pruebas

```bash
npm test
```

Resultado esperado:

```text
tests 13
pass 13
fail 0
```

## URL publica

Pendiente de despliegue en Render.

## Formato de respuesta

Todas las respuestas usan una estructura JSON estandar:

```json
{
  "success": true,
  "message": "Mensaje de la operacion",
  "data": {},
  "errors": null,
  "timestamp": "2026-10-09T00:00:00.000Z"
}
```

## Endpoints

| Metodo | Ruta | Descripcion |
|---|---|---|
| GET | `/` | Verifica que la API esta activa. |
| GET | `/api/v1/libros` | Lista el catalogo completo. |
| GET | `/api/v1/libros?q=texto` | Busca libros por titulo o autor. |
| GET | `/api/v1/libros?categoria=Categoria` | Filtra libros por categoria. |
| GET | `/api/v1/libros/categorias` | Lista las categorias existentes. |
| GET | `/api/v1/libros/:id` | Consulta el detalle de un libro. |
| POST | `/api/v1/libros` | Registra un libro nuevo. |
| PUT | `/api/v1/libros/:id` | Actualiza los datos de un libro. |
| PATCH | `/api/v1/libros/:id/prestamo` | Registra el prestamo de un ejemplar. |
| PATCH | `/api/v1/libros/:id/devolucion` | Registra la devolucion de un ejemplar. |
| DELETE | `/api/v1/libros/:id` | Retira un libro del catalogo. |

## Codigos HTTP principales

| Codigo | Uso |
|---|---|
| 200 | Consulta o actualizacion correcta. |
| 201 | Libro creado correctamente. |
| 400 | Datos invalidos o identificador incorrecto. |
| 404 | Recurso no encontrado. |
| 409 | Conflicto con una regla de negocio. |
| 500 | Error interno del servidor. |

## Reglas de negocio implementadas

- Un libro nuevo inicia con todos sus ejemplares disponibles.
- No se puede prestar un libro con 0 ejemplares disponibles.
- No se puede devolver un ejemplar si todos estan disponibles.
- El ISBN no puede repetirse en el catalogo.
- Los campos obligatorios se validan antes de crear o actualizar.
- Al actualizar ejemplares se conservan los prestamos activos.
