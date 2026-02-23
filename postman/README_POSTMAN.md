# Guía de uso - Colección Postman

## 📥 Importación

1. Abre Postman
2. Click en **Import** (esquina superior izquierda)
3. Arrastra los 2 archivos JSON:
   - `Gestor_Opiniones.postman_collection.json`
   - `Lab2_Environment.postman_environment.json`
4. Selecciona el environment **Lab2 - Desarrollo** en el dropdown (esquina superior derecha)

## 🚀 Flujo de prueba completo

### 1. Verificar servidor activo
- Ejecuta `Health Check` para confirmar que la API responde

### 2. Registro y autenticación
1. **Auth > 1. Register User**: Crea un nuevo usuario
   - Guarda automáticamente el `userId`
2. **IMPORTANTE**: Ve a la consola del servidor y copia el token de verificación del log (o revisa el email si configuraste SMTP)
3. **Auth > 2. Verify Email**: Pega el token copiado y verifica el email
4. **Auth > 3. Login**: Inicia sesión
   - Guarda automáticamente el `authToken` para requests autenticados

### 3. Perfil
1. **Profile > 1. Get My Profile**: Obtiene tu perfil completo
2. **Profile > 3. Update Profile**: Actualiza tus datos (nombre, username, teléfono)
3. **Profile > 4. Change Password**: Cambia tu contraseña (requiere contraseña actual)

### 4. Publicaciones
1. **Posts > 1. Create Post**: Crea una publicación
   - Guarda automáticamente el `postId`
2. **Posts > 2. Get All Posts**: Lista todas las publicaciones
3. **Posts > 3. Get Post By ID**: Obtiene tu publicación específica
4. **Posts > 4. Update Post**: Edita tu publicación (solo tú puedes hacerlo)
5. **Posts > 5. Delete Post**: Elimina tu publicación (⚠️ esto borrará también sus comentarios)

### 5. Comentarios
1. **Comments > 1. Create Comment**: Comenta en tu publicación
   - Guarda automáticamente el `commentId`
2. **Comments > 2. Get Comments By Post**: Lista comentarios de la publicación
3. **Comments > 3. Update Comment**: Edita tu comentario (solo tú puedes hacerlo)
4. **Comments > 4. Delete Comment**: Elimina tu comentario

### 6. Recuperación de contraseña
1. **Auth > 5. Forgot Password**: Solicita reset de contraseña
2. Copia el token del log/email
3. **Auth > 6. Reset Password**: Pega el token y define nueva contraseña

## 🔑 Variables de entorno

La colección usa estas variables (se actualizan automáticamente):

- `baseUrl`: URL base de la API
- `authToken`: Token JWT para autenticación (se guarda en login)
- `userId`: ID del usuario registrado
- `postId`: ID de la última publicación creada
- `commentId`: ID del último comentario creado

## ⚠️ Notas importantes

1. **Orden de ejecución**: Sigue el flujo numerado para evitar errores de dependencias
2. **Email verification**: Si no tienes SMTP configurado, copia el token del log del servidor
3. **Tokens de recuperación**: Los tokens de reset también aparecen en el log si no hay SMTP
4. **Permisos**: Solo puedes editar/eliminar tus propias publicaciones y comentarios
5. **Rate limiting**: Si haces muchas requests seguidas, espera 1 minuto

## 🧪 Pruebas de permisos

Para probar que solo el dueño puede editar/eliminar:

1. Crea un segundo usuario (cambia el email/username en Register)
2. Loguea con el segundo usuario (se actualizará el token)
3. Intenta editar/eliminar la publicación del primer usuario
4. Deberías recibir error 403 (Forbidden)

## 📝 Ejemplos de datos

La colección viene con datos de ejemplo listos para usar. Puedes modificarlos antes de enviar cada request.

**Usuario de prueba:**
- Email: `juan.perez@example.com`
- Username: `juanperez`
- Password: `Password123`
- Phone: `12345678`

**Publicación de ejemplo:**
- Title: "Mi primera publicación"
- Category: "General"
- Content: Texto de ejemplo

**Comentario de ejemplo:**
- Content: "Excelente publicación..."
