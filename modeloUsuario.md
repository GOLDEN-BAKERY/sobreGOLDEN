* Esquemas: Puedes definir esquemas para modelar tus datos. Los esquemas te permiten definir la estructura de los datos, los tipos de campos y pueden incluir validación de datos.

+ Modelos: Los esquemas se utilizan para crear modelos. Los modelos son constructores que creas a partir de esquemas de Mongoose y representan documentos que se pueden guardar y recuperar de la base de datos.

```javascript

const usuarioShema = Shema({

    nombre:{
        type: String,
        required: [true, 'El nombre es obligatorio']
    },
    correo:{
        type: String,
        required: [true ,'El correo es obligstorio'],
        unique : true

    },
    password:{
        type: String,
        required: [true, 'El password es obligstorio'],
    },
    img:{
        type: String
    },
    rol:{
        type: String,
        required: true,
        emun:['ADMIN_ROLE', 'USER_ROLE']
    },
    estado:{
        type: Boolean,
        default: true
    },
    google:{
        type: Boolean,
        default:false
    }
});

```
Los dos últimos campos, estado y google,  estan diseñados para manejar la lógica de estado del usuario y su método de autenticación. 
+ estado - Este campo se usa para representar si el usuario está activo o no. Al establecer default: true, estás diciendo que cuando se cree un nuevo usuario, por defecto, su estado será activo (true). Si en algún momento decides "borrar" un usuario, en lugar de eliminar el documento de la base de datos, simplemente cambiarías el valor de este campo a false (que erróneamente has escrito como fours, pero debería ser false).
+ google - te permite diferenciar entre los usuarios que se han registrado a través de tu método de autenticación estándar y aquellos que han utilizado Google, lo cual puede ser relevante para la lógica de inicio de sesión, permisos, o para funciones específicas de la aplicación que puedan variar según el método de registro del usuario.