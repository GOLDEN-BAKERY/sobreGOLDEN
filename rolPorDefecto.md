# Resumen de Configuración de Roles de Usuario

## Modelo de Rol
- Se confirmó que la colección `rols` en la base de datos contiene los roles:
  - `ADMIN_ROLE`
  - `USER_ROLE`
  - `VENTAS_ROLE`

## Modelo de Usuario
- Se ajustó el `UsuarioSchema` para incluir el campo `rol` con las propiedades:
  - `type: String`: Define que el valor del rol es una cadena de texto.
  - `required: true`: Hace el campo obligatorio.
  - `enum: ['ADMIN_ROLE', 'USER_ROLE', 'VENTAS_ROLE']`: Restringe los valores del rol a los definidos.
  - `default: 'USER_ROLE'`: Establece 'USER_ROLE' como el valor predeterminado si no se especifica un rol al crear un nuevo usuario.

## Middleware de Validación
- Se modificó la validación del rol con `express-validator` para hacerla opcional y permitir que la solicitud continúe si no se proporciona un rol:
  ```javascript
  check('rol').optional().custom(async (rol) => {
      const existeRol = await Role.findOne({ rol });
      if (!existeRol) {
          throw new Error(`El rol ${rol} no está registrado en la Base de Datos`);
      }
  }),


### Controlador de Usuario

Se incluyó un bloque condicional en el controlador saveUsuario para asignar 'USER_ROLE' si el rol no se proporciona en la solicitud:

    ```javascript

if (!body.rol) {
    body.rol = 'USER_ROLE';
}
```
Sin embargo, se determinó que este paso podría ser redundante, ya que Mongoose ya maneja el valor predeterminado.

***
### Pruebas y Confirmación

***Se realizaron pruebas para confirmar que la creación de usuarios funciona correctamente tanto con el bloque condicional en el controlador como sin él, demostrando que Mongoose asigna el valor predeterminado 'USER_ROLE' adecuadamente.**

**Con estos ajustes, se garantiza que cada nuevo usuario se cree con un rol, ya sea proporcionado explícitamente en la solicitud o asignado automáticamente a 'USER_ROLE', manteniendo así la integridad del sistema de roles y simplificando el proceso de registro de usuarios.**
***
