# 🧩 Leer parámetros JSON en una API PHP

Cuando una API recibe una solicitud `POST` con datos en formato JSON, los valores no aparecen en `$_POST`.  
En su lugar, se leen desde el **flujo de entrada (input stream)** y se decodifican.

---

## 📁 1. Ejemplo de API: `api_json.php`

```php
<?php
header('Content-Type: application/json; charset=utf-8');

// Leer el cuerpo de la solicitud (raw input)
$json = file_get_contents('php://input');

// Convertir el JSON a un arreglo asociativo
$datos = json_decode($json, true);

// Validar que se haya recibido correctamente
if (!$datos) {
    echo json_encode(['error' => 'JSON inválido o vacío']);
    exit;
}

// Acceder a valores específicos
$nombre = $datos['nombre'] ?? 'Invitado';
$edad   = $datos['edad'] ?? null;

// Preparar respuesta
$respuesta = [
    'mensaje' => "Hola, $nombre 👋",
    'edad' => $edad,
    'recibido' => $datos
];

// Devolver la respuesta como JSON
echo json_encode($respuesta);
