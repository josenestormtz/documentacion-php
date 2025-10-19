## ⚙️ Ejecutar un procedimiento almacenado con 3 parámetros desde PHP

Este ejemplo muestra cómo llamar a un **procedimiento almacenado** en **MySQL** que recibe **tres parámetros** usando **MySQLi** en PHP, y devolver el resultado como **JSON**.

---

### 📜 Ejemplo de código

```php
<?php
// 🔧 Variables de conexión
$servidor = "localhost";
$usuario = "root";
$contrasena = "";
$base_datos = "mi_basedatos";

// Conexión a la base de datos
$conn = new mysqli($servidor, $usuario, $contrasena, $base_datos);
if ($conn->connect_error) {
    die(json_encode(['error' => 'Error de conexión: ' . $conn->connect_error]));
}

// 📩 Parámetros de entrada
$nombre = "Néstor";
$correo = "nestor@example.com";
$activo = 1;

// ⚙️ Llamada al procedimiento almacenado
$sql = "CALL sp_registrar_usuario(?, ?, ?)";
$stmt = $conn->prepare($sql);

// 's' = string, 'i' = integer
$stmt->bind_param("ssi", $nombre, $correo, $activo);
$stmt->execute();

// 📦 Obtener resultados
$result = $stmt->get_result();
$datos = [];

while ($fila = $result->fetch_assoc()) {
    $datos[] = $fila;
}

// 📤 Devolver respuesta en formato JSON
echo json_encode([
    'estatus' => count($datos) > 0 ? 'ok' : 'sin_resultado',
    'resultado' => $datos
]);

$stmt->close();
$conn->close();
```

Si el procedimiento devuelve solo un registro con una columna (nombre), puedes utilizar el siguiente código:
```php
<?php
// 🔧 Variables de conexión
$servidor = "localhost";
$usuario = "root";
$contrasena = "";
$base_datos = "mi_basedatos";

// Conexión a la base de datos
$conn = new mysqli($servidor, $usuario, $contrasena, $base_datos);
if ($conn->connect_error) {
    die(json_encode(['error' => 'Error de conexión: ' . $conn->connect_error]));
}

// Parámetro de ejemplo
$id = 5;

// 🔹 Llamar al procedimiento
$sql = "CALL sp_obtener_usuario(?)";
$stmt = $conn->prepare($sql);
$stmt->bind_param("i", $id);
$stmt->execute();

// 🔹 Obtener el resultado (una sola fila)
$result = $stmt->get_result();
$fila = $result->fetch_assoc(); // ← aquí obtenemos directamente la fila

if ($fila) {
    // Si existe el registro, accedemos directamente al valor
    $nombre = $fila['nombre'];
    echo json_encode([
        'estatus' => 'ok',
        'nombre' => $nombre
    ]);
} else {
    echo json_encode([
        'estatus' => 'sin_resultado'
    ]);
}

$stmt->close();
$conn->close();
```
