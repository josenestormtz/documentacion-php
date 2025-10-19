## ⚙️ Ejecutar un procedimiento almacenado con 3 parámetros desde PHP

Este ejemplo muestra cómo llamar a un **procedimiento almacenado** en **MySQL** que recibe **tres parámetros** usando **MySQLi** en PHP, y devolver el resultado como **JSON**.

---

### 📜 Ejemplo de código

```php
<?php
// Conexión a la base de datos
$conn = new mysqli("localhost", "root", "", "mi_basedatos");
if ($conn->connect_error) {
    die(json_encode(['error' => 'Error de conexión: ' . $conn->connect_error]));
}

// Parámetros de entrada
$nombre = "Néstor";
$correo = "nestor@example.com";
$activo = 1;

// Llamada al procedimiento
$sql = "CALL sp_registrar_usuario(?, ?, ?)";
$stmt = $conn->prepare($sql);

// 's' = string, 'i' = integer
$stmt->bind_param("ssi", $nombre, $correo, $activo);
$stmt->execute();

// Obtener resultados
$result = $stmt->get_result();
$datos = [];

while ($fila = $result->fetch_assoc()) {
    $datos[] = $fila;
}

// Devolver respuesta en JSON
echo json_encode([
    'estatus' => count($datos) > 0 ? 'ok' : 'sin_resultado',
    'resultado' => $datos
]);

$stmt->close();
$conn->close();
