# Lab2 - Gestor de Opiniones

API REST en Node.js para gestionar opiniones tipo publicaciones y comentarios, con:

- Autenticación y perfil en PostgreSQL (tablas: `users`, `user_profiles`, `user_emails`, `user_password_resets`, `roles`, `user_roles`).
- Publicaciones y comentarios en MongoDB.
- Login por correo o username + contraseña.
- Verificación por correo, recuperación de contraseña con token y envío de emails.

## Stack

- Node.js + Express
- pnpm
- PostgreSQL (contenedor con `docker-compose.yml`)
- MongoDB (sin credenciales)
- Sequelize (Postgres) + Mongoose (Mongo)

## Preparación

1. Copia `.env.example` a `.env`.
2. Levanta PostgreSQL:

```bash
docker compose up -d
```

3. Asegúrate de tener MongoDB local activo en `mongodb://localhost:27017/opiniones_db`.
4. Instala dependencias:

```bash
pnpm install
```

5. Ejecuta la API:

```bash
pnpm dev
```

Base URL: `http://localhost:3000/api/v1`

## Funcionalidades implementadas

### 1) Auth y perfil (PostgreSQL)

- Registro de usuario
- Login por `emailOrUsername`
- Verificación de email
- Reenvío de verificación
- Forgot/reset password con token
- Obtener perfil autenticado
- Actualizar perfil (`name`, `surname`, `username`, `phone`, `profilePicture`)
- Cambiar contraseña exigiendo contraseña actual

No existe endpoint para eliminar perfiles.

### 2) Publicaciones (MongoDB)

- Crear publicación (requiere JWT)
- Listar publicaciones
- Obtener publicación por ID
- Editar solo tu publicación
- Eliminar solo tu publicación

Campos:

- `title`
- `category`
- `content`

### 3) Comentarios (MongoDB)

- Crear comentario en una publicación existente (requiere JWT)
- Listar comentarios por publicación
- Editar solo tu comentario
- Eliminar solo tu comentario

## Endpoints principales

### Auth

- `POST /auth/register`
- `POST /auth/login`
- `POST /auth/verify-email`
- `POST /auth/resend-verification`
- `POST /auth/forgot-password`
- `POST /auth/reset-password`
- `GET /auth/profile`
- `PUT /auth/profile`
- `PUT /auth/change-password`

### Posts

- `GET /posts`
- `GET /posts/:postId`
- `POST /posts`
- `PUT /posts/:postId`
- `DELETE /posts/:postId`

### Comments

- `GET /comments/post/:postId`
- `POST /comments`
- `PUT /comments/:commentId`
- `DELETE /comments/:commentId`

## Validaciones incluidas

- Reglas de longitud/formato en auth, perfil, publicaciones y comentarios.
- Validación de ObjectId para rutas de Mongo.
- Control de permisos: solo dueño puede editar/eliminar su publicación/comentario.
- Rate limiting en endpoints generales y de autenticación.

