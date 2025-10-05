# Manejo de errores con try-catch en PHP

En PHP, el bloque `try-catch` se utiliza para **capturar excepciones** y manejar errores de forma controlada, evitando que el script se detenga abruptamente.

---

## 1️⃣ Sintaxis básica

```php
try {
    // Código que puede generar un error
} catch (Exception $e) {
    // Código para manejar la excepción
    echo $e->getMessage();
}
```

2️⃣ Ejemplo práctico
```php
<?php
try {
    $numero = 10;
    $divisor = 0;

    if ($divisor === 0) {
        // Lanzar una excepción manualmente
        throw new Exception("No se puede dividir entre cero.");
    }

    $resultado = $numero / $divisor;
    echo "El resultado es: $resultado";

} catch (Exception $e) {
    // Capturar y mostrar la excepción
    echo "¡Ocurrió un error! " . $e->getMessage();
}
```

🔹 Explicación
try: contiene el código que puede generar un error.

throw new Exception(): lanza una excepción si ocurre un problema.

catch (Exception $e): captura la excepción y permite manejarla.

$e->getMessage(): obtiene el mensaje de error de la excepción.

3️⃣ Beneficios
Previene que el script se detenga por errores inesperados.

Permite mostrar mensajes de error claros al usuario.

Facilita el debugging y manejo de errores en aplicaciones más grandes, como APIs o integraciones con WordPress.
