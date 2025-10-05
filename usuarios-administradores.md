Identificar Usuarios Administradores en WordPress

En WordPress, a veces necesitamos conocer qué usuarios tienen rol de **Administrador**. Esto es útil, por ejemplo, para scripts externos o APIs que necesiten permisos especiales.

---

## 1️⃣ Obtener todos los administradores con PHP

```php
<?php
require_once $_SERVER['DOCUMENT_ROOT'] . '/wp-load.php';

// Obtener todos los usuarios con rol Administrator
$admins = get_users(array(
    'role' => 'Administrator'
));

foreach ($admins as $admin) {
    echo "ID: " . $admin->ID . " - Usuario: " . $admin->user_login . "<br>";
}
```

🔹 Explicación
get_users() → obtiene una lista de usuarios según criterios.

'role' => 'Administrator' → filtra solo los usuarios con rol de administrador.

$admin->ID → ID del usuario.

$admin->user_login → nombre de usuario.

2️⃣ Uso práctico
Conocer el ID del administrador te permite:

Ejecutar scripts externos con permisos de administrador (ej. eliminar usuarios).

Reasignar contenido de otros usuarios a un administrador.

Verificar permisos antes de ejecutar funciones sensibles.

3️⃣ Precauciones
No expongas scripts con permisos de administrador sin protección, ya que podrían ser usados malintencionadamente.

Siempre verifica que el usuario que estás usando tenga rol de administrador antes de ejecutar acciones como wp_delete_user() o cambios en la base.
