## Documentación: Creación de Usuario y Guardado en Base de Datos

### Objetivo
Detallar el proceso establecido para aceptar datos de registro de usuarios a través de una petición POST y almacenarlos en una base de datos MongoDB utilizando Mongoose.

### Procedimiento

1. **Modelo de Usuario con Mongoose**: 
   Se define un esquema `UsuarioSchema` con los campos correspondientes a los datos del formulario de registro.

2. **Middleware de Análisis de Cuerpo**: 
   Se configura `express.json()` en el servidor Express para parsear el cuerpo de las solicitudes entrantes en formato JSON.

3. **Controlador de Guardado de Usuario**: 
   Implementación de un controlador `saveUsuario` que:
   - Recibe el cuerpo completo de la solicitud (`req.body`).
   - Crea una instancia del modelo `Usuario` con los datos recibidos.
   - Guarda la nueva instancia en la base de datos utilizando `usuario.save()`.

4. **Manejo de Errores**: 
   Utilización de un bloque `try-catch` para manejar errores de validación o de guardado, enviando una respuesta con estado HTTP 500 y un mensaje descriptivo en caso de fallo.

5. **Configuración de Ruta**: 
   Establecimiento de la ruta `/crearCuenta` en las rutas de Express, vinculada al controlador `saveUsuario`.

### Resultado

La configuración permite el registro de usuarios nuevos de manera efectiva, con los datos enviados desde el formulario almacenándose correctamente en la base de datos. Los campos no obligatorios o faltantes se manejan sin interrumpir el proceso de guardado.

### Recomendaciones

Antes del lanzamiento, asegurar que todos los campos necesarios sean marcados como requeridos y que la seguridad en el manejo de contraseñas sea reforzada mediante técnicas como el hashing.
