# PF-G1 Demo

Orquestador Docker para levantar la demo completa de PF-G1 con un solo comando.

## Servicios

- Front: http://localhost:3000
- Back: http://127.0.0.1:3010
- Scheduler: http://127.0.0.1:3020
- PostgreSQL: interno en Docker como `db:5432`, base `pf_g1_django`

Durante la migración Django, el compose construye Back y Front desde carpetas locales:

- Back: ../PF-G1-Back-Django
- Front: ../PF-G1-Front
- Scheduler: https://github.com/LucasCttr/pf-or-scheduler.git#scheduler-api

## Ejecutar

```bash
docker compose up --build
```

Luego abrir:

```text
http://localhost:3000
```

Usuarios de prueba:

| Rol | Email | Password |
| --- | --- | --- |
| Administrador | admin@hospital.com | admin123 |
| Cirujano | cirujano@hospital.com | cirujano123 |
| Jefe Quirofano | jefe@hospital.com | jefe123 |
| Recepcionista | recepcion@hospital.com | recepcion123 |

## Reset de datos

Desde el MVP, usar el boton `Restablecer demo` del sidebar.

Para borrar el volumen de PostgreSQL y arrancar desde cero:

```bash
docker compose down -v
```

## Notas

- PostgreSQL no se publica en `localhost:5432` para evitar conflictos con una DB local ya levantada.
- El Back se conecta a la DB por la red interna de Docker usando `db:5432`.
- El Front nunca llama directo al Scheduler.
- El Back aplica migraciones al iniciar.
- El Scheduler envia el resultado final al Back por callback interno de Docker Compose.
