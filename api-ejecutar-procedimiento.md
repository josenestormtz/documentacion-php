## ⚙️ Ejecutar un procedimiento almacenado desde PHP

Este fragmento muestra cómo llamar a un **procedimiento almacenado (Stored Procedure)** en **MySQL** usando **MySQLi** en PHP, y devolver los resultados en formato **JSON**.

---

### 📜 Ejemplo de código

```php
<?php
// Conexión a la base de datos
$conn = new mysqli("localhost", "root", "", "mi_basedatos");
if ($conn->connect_error) {
    die(json_encode(['error' => 'Error de conexión: ' . $conn->connect_error]));
}

// Parámetro de entrada
$id = 1; // Ejemplo: ID recibido por JSON o GET

// Llamada al procedimiento
$sql = "CALL sp_get_usuario(?)";
$stmt = $conn->prepare($sql);
$stmt->bind_param("i", $id);
$stmt->execute();

// Obtener los resultados
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
