# 🧩 Crear una API sencilla en PHP ("Hola Mundo")

Este tutorial muestra cómo crear una API básica en **PHP** que devuelva un mensaje en formato **JSON**.

---

## 📁 1. Crear el archivo

En la carpeta donde alojas tu proyecto o tu servidor web (por ejemplo, `/api/`), crea un archivo llamado prueba.php.


---

## 🧠 2. Escribir el código

Copia y pega el siguiente código dentro del archivo:

```php
<?php

// === PRODUCCIÓN: NO IMPRIMIR ERRORES EN PANTALLA ===
ini_set('display_errors', 0);
ini_set('display_startup_errors', 0);
error_reporting(E_ALL);

// Limpia buffers previos y empieza uno nuevo
if (function_exists('ob_get_level')) {
  while (ob_get_level() > 0) { @ob_end_clean(); }
}

// === ENCABEZADOS DE RESPUESTA ===
header('Content-Type: application/json; charset=utf-8');
header('Access-Control-Allow-Origin: *'); // Permite acceso desde cualquier origen (útil para pruebas)

// === RESPUESTA DE LA API ===
$respuesta = [
    'mensaje' => 'Hola Mundo 🌎',
    'fecha' => date('Y-m-d H:i:s')
];

// === DEVOLVER COMO JSON ===
echo json_encode($respuesta);
```

## 🚀 3. Probar la API

Abre tu navegador o Postman y accede a la ruta:

```url
http://localhost/api/hola.php
```

Deberías ver una respuesta como esta:

```php
{
  "mensaje": "Hola Mundo 🌎",
  "fecha": "2025-10-18 09:45:00"
}
```

## 💡 Consejo adicional

Si planeas crear más endpoints (por ejemplo /api/usuarios.php o /api/productos.php), es recomendable:

Mantener todos tus archivos dentro de una carpeta /api/.

Reutilizar configuraciones comunes (por ejemplo, manejo de errores o conexión a base de datos).

Probar tus endpoints con herramientas como Postman, Insomnia, o desde la terminal con curl.

✅ Resultado

Con este simple script ya tienes una API básica en PHP que responde con datos en formato JSON.
Es el punto de partida ideal para crear endpoints más complejos, conectar con bases de datos o integrarlo con WordPress.
