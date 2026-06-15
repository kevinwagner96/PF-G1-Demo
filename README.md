# PF-G1 Demo

Orquestador Docker para levantar la demo completa de PF-G1 con un solo comando.

## Servicios

- Front: http://localhost:3000
- Back: http://127.0.0.1:3010
- Scheduler: http://127.0.0.1:3020
- PostgreSQL: interno en Docker como `db:5432`, base `pf_g1_django`

El compose construye las apps desde GitHub para que alcance con clonar este repo y ejecutar Docker Compose:

- Back: https://github.com/kevinwagner96/PF-G1-Back-Django.git#main
- Front: https://github.com/kevinwagner96/PF-G1-Front.git#main
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
| System Admin | sysadmin@hospital.com | sysadmin123 |
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
- Django Admin está en `http://127.0.0.1:3010/admin/` y se usa con el usuario `System Admin`.
- El Back aplica migraciones al iniciar.
- El Scheduler envia el resultado final al Back por callback interno de Docker Compose.
