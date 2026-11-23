# Práctica 8 — Microservicios

El monolito de la práctica 7 queda partido en tres servicios y un gateway.

| Servicio | Puerto host | Base |
| --- | --- | --- |
| gateway (nginx) | 80 | — |
| servicio_auth | 8001 | postgres_auth :5433 |
| servicio_usuarios | 8002 | postgres_usuarios :5434 |
| servicio_productos | 8003 | postgres_productos :5435 |

`servicio_auth` firma JWT con RS256. Los otros dos solo tienen la llave pública.

## Arranque

```bash
cp servicio_auth/.env.example servicio_auth/.env
cp servicio_usuarios/.env.example servicio_usuarios/.env
cp servicio_productos/.env.example servicio_productos/.env
docker compose up --build
```

Token: `POST http://localhost/api/auth/token/`

La llave `servicio_auth/keys/private.pem` es de laboratorio. No la uses fuera de esta práctica.

## Tests

Sin Docker, cada servicio usa SQLite si no hay `DATABASE_ENGINE`.

```bash
cd servicio_auth && python manage.py test
cd servicio_usuarios && python manage.py test
cd servicio_productos && python manage.py test
```
