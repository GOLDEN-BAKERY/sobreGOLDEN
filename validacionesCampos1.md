# express-validator

**express-validator** es una biblioteca de middleware para Express que proporciona un marco de validación y saneamiento de datos del lado del servidor. Su función principal es validar los datos de entrada según las reglas que hayas definido, y opcionalmente limpiar los datos (saneamiento) para asegurarse de que están en el formato correcto antes de que los proceses en tu controlador.

### Aplicar las Validaciones en la Ruta POST:

1. Asegúrate de que tus validaciones de express-validator están en la ruta POST que se encarga de registrar los nuevos usuarios.

```javascript
const { check } = require('express-validator');

router.post('/crearCuenta', [
    check('correo', 'Ingrese un correo electrónico válido').isEmail(),
    check('nombre', 'El nombre es obligatorio').not().isEmpty(),
    check('telefono', 'El teléfono debe ser un número de 9 dígitos').matches(/^[0-9]{9}$/),
    // Otros checks si son necesarios
], controller.crear);

```



2. Manejar Resultados de Validación en el Controlador:

En tu controlador crear, asegúrate de que estás manejando correctamente los errores de validación.

```javascript

const { validationResult } = require('express-validator');

controller.crear = async (req, res) => {
    const errors = validationResult(req);
    if (!errors.isEmpty()) {
        return res.status(400).json({ errors: errors.array() });
    }

    // Lógica de registro de usuario
};

```