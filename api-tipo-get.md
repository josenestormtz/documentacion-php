# 🧩 Leer parámetros en una API tipo GET (PHP)

Este ejemplo muestra cómo crear una pequeña **API en PHP** que recibe parámetros desde la URL (método **GET**) y devuelve una respuesta en **JSON**.

---

## 🧠 1️⃣ Crear el archivo

Crea un archivo llamado `api-ejemplo.php` con el siguiente contenido:

```php
<?php
// api-ejemplo.php

// Encabezados para respuesta JSON
header("Content-Type: application/json; charset=UTF-8");
header("Access-Control-Allow-Origin: *");

// === 1️⃣ Leer parámetros desde la URL ===
// Ejemplo de URL:
// https://tusitio.com/api-ejemplo.php?nombre=Nestor&edad=35

$nombre = $_GET['nombre'] ?? '';
$edad = $_GET['edad'] ?? '';

// === 2️⃣ Validar los parámetros ===
if (empty($nombre) || empty($edad)) {
    echo json_encode([
        "status" => "error",
        "message" => "Faltan parámetros. Usa ?nombre=TuNombre&edad=TuEdad"
    ]);
    exit;
}

// === 3️⃣ Procesar la información (ejemplo) ===
$mensaje = "Hola $nombre, tienes $edad años.";

// === 4️⃣ Responder en formato JSON ===
$response = [
    "status" => "success",
    "message" => $mensaje,
    "data" => [
        "nombre" => $nombre,
        "edad" => $edad
    ]
];

echo json_encode($response, JSON_UNESCAPED_UNICODE | JSON_PRETTY_PRINT);
?>
```

🧭 2️⃣ Cómo probarlo

Abre tu navegador o usa Postman / curl con la siguiente URL:

```php
https://tusitio.com/api-ejemplo.php?nombre=Nestor&edad=35
```

🧾 3️⃣ Resultado esperado
```php
{
  "status": "success",
  "message": "Hola Nestor, tienes 35 años.",
  "data": {
    "nombre": "Nestor",
    "edad": "35"
  }
}
```

🧩 4️⃣ Tip adicional

Puedes manejar valores numéricos o parámetros opcionales así:

```php
$id = isset($_GET['id']) ? (int)$_GET['id'] : 0;
$filtro = $_GET['filtro'] ?? '';
```
