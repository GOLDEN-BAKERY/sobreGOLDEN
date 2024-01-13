## Encriptación de Contraseña

La encriptación de la contraseña se realiza en el controlador `saveUsuario` antes de guardar un nuevo usuario en la base de datos.

### Proceso

1. **Extracción de la Contraseña:**
   La contraseña se extrae del cuerpo de la solicitud.

   ```javascript
   const { password } = req.body;


**Generación de Salt:**

Se genera un "salt" utilizando bcryptjs para agregar complejidad al proceso de hasheo.

```javascript
const salt = bcryptjs.genSaltSync();
```

**Hasheo de la Contraseña:**
La contraseña se hashea utilizando el "salt" generado en el paso anterior. Esto se hace de manera síncrona.

```javascript
body.password = bcryptjs.hashSync(password, salt);
```
***
### Seguridad

**La encriptación de la contraseña con bcryptjs mejora la seguridad al almacenar las contraseñas en la base de datos. En lugar de guardar la contraseña en texto plano, se guarda una versión hasheada que es muy difícil de revertir, protegiendo así la información sensible de los usuarios.**
***