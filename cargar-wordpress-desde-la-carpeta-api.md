# Mini Tutorial: Cargar WordPress desde la carpeta `/api/`

Este tutorial explica cómo cargar el entorno de WordPress desde scripts o APIs ubicadas fuera del núcleo de WordPress (por ejemplo, en `/api/`), usando un archivo `bootstrap.php`.

---

## 1️⃣ Estructura de carpetas recomendada

```text
/public_html/
  ├── wp-admin/
  ├── wp-content/
  ├── wp-includes/
  ├── wp-load.php
  ├── index.php
  └── api/
       ├── bootstrap.php
       └── mi_api.php
```

php
Copiar código

> Mantener los scripts separados ayuda a organizar tu proyecto y facilita el mantenimiento.

---

## 2️⃣ Crear el archivo `bootstrap.php`

Ubicado en `/api/bootstrap.php`:

```php
<?php
/**
 * bootstrap.php
 * 
 * Permite cargar WordPress desde cualquier script externo.
 */

// Cargar WordPress desde la raíz del sitio
require_once $_SERVER['DOCUMENT_ROOT'] . '/wp-load.php';
Se utiliza $_SERVER['DOCUMENT_ROOT'] para apuntar automáticamente a la raíz del sitio, evitando rutas relativas como ../wp-load.php.

3️⃣ Usar bootstrap.php en tus scripts
Ejemplo de /api/mi_api.php:

php
Copiar código
<?php
require_once __DIR__ . '/bootstrap.php';

// Obtener usuario por login
$user = get_user_by('login', 'nestor');

if ($user) {
    $respuesta = [
        'estatus' => 'ok',
        'mensaje' => "El usuario {$user->user_login} está registrado."
    ];
} else {
    $respuesta = [
        'estatus' => 'error',
        'mensaje' => 'Usuario no encontrado.'
    ];
}

// Devolver respuesta en formato JSON
header('Content-Type: application/json');
echo json_encode($respuesta);
4️⃣ Beneficios de este enfoque
✅ Centraliza la carga de WordPress en un solo archivo (bootstrap.php)

✅ Facilita el mantenimiento de tus scripts y APIs

✅ Evita problemas con rutas relativas

✅ Permite reutilizar la configuración en todos los scripts de /api/

5️⃣ Resultado esperado
Al acceder a tu API, por ejemplo:

arduino
Copiar código
https://tusitio.com/api/mi_api.php
Obtendrás una respuesta JSON como:

json
Copiar código
{
  "estatus": "ok",
  "mensaje": "El usuario nestor está registrado."
}
Ahora puedes crear más scripts en /api/ que utilicen cualquier función de WordPress sin duplicar código.
