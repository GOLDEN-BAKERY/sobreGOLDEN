### Documentación del Proceso de Autenticación:

1. **Recepción de Credenciales:**

    El servidor recibe una solicitud POST en la ruta /iniciar con las credenciales del usuario (email y contraseña) a través del cuerpo de la solicitud (request body).

2. **Controlador de Inicio de Sesión (existe)**:

    Se define un controlador de inicio de sesión en el servidor que maneja la solicitud POST.
    Este controlador extrae las credenciales (email y contraseña) del cuerpo de la solicitud utilizando la desestructuración de objetos de JavaScript.

3. **Búsqueda de Usuario en MongoDB**:

    Se realiza una búsqueda en la base de datos MongoDB utilizando Mongoose.
    Se usa el modelo Usuario para invocar el método findOne, pasando el email como criterio de búsqueda para encontrar un documento de usuario correspondiente.

4. **Verificación de Credenciales**:

    Se compara la contraseña proporcionada en la solicitud con la almacenada en el documento del usuario encontrado.
    Actualmente, esta comparación se realiza directamente ya que las contraseñas están almacenadas en texto plano.

5. **Respuestas del Servidor**:

    *Éxito:* Si se encuentra un documento de usuario y las contraseñas coinciden, se envía una respuesta con el estado HTTP 200 y el mensaje 'éxito'.
    *Usuario No Existe o Error de Login:* Si no se encuentra un documento de usuario con el email proporcionado, o si las contraseñas no coinciden, se envía una respuesta con el estado HTTP 401 y el mensaje 'usuario no existe o error de login'.
    *Error en el Servidor:* Si ocurre un error durante el proceso de búsqueda o comparación, se captura en un bloque catch y se envía una respuesta con el estado HTTP 500 y un mensaje de error genérico.

***
### Consideraciones de Seguridad:
Se destaca que el almacenamiento de contraseñas en texto plano es una práctica insegura.
Se recomienda la implementación futura de hasheo de contraseñas con una biblioteca como bcrypt para proteger la información de los usuarios.
***

