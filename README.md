# Documentación de mis APIs

## API para WordPress

### bootstrap.php
Permite cargar el entorno de WordPress desde cualquier script.

```php
<?php
require_once $_SERVER['DOCUMENT_ROOT'] . '/wp-load.php';
