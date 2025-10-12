# 🛠️ Mini Tutorial: Habilitar CORS en PHP

Cuando intentas consumir una API desde un dominio diferente (cross-origin), el navegador puede bloquear la petición por **CORS**. Para solucionarlo, debes configurar tu API para permitir el acceso desde otros orígenes.

---

## 1️⃣ Qué es CORS

**CORS (Cross-Origin Resource Sharing)** es un mecanismo de seguridad que evita que una página web haga peticiones a otro dominio sin permiso.
Si la API no devuelve el encabezado `Access-Control-Allow-Origin`, el navegador bloqueará la petición.

---

## 2️⃣ Cómo habilitar CORS en PHP

Abre tu archivo PHP (ejemplo: `api-estados.php`) y agrega **al inicio del archivo**, antes de cualquier salida (`echo`, `print`, HTML, etc.):

```php
<?php
// Permitir cualquier dominio
header("Access-Control-Allow-Origin: *");

// Permitir métodos específicos (GET, POST, OPTIONS)
header("Access-Control-Allow-Methods: GET, POST, OPTIONS");

// Permitir encabezados específicos
header("Access-Control-Allow-Headers: Content-Type");
```

> ✅ Esto permitirá que cualquier página web haga peticiones a tu API.
> Si quieres restringirlo a tu dominio específico:

```php
header("Access-Control-Allow-Origin: https://dk.dekandela.com.mx");
```

---

## 3️⃣ Verificación

1. Guarda los cambios en tu servidor.
2. Desde tu frontend, realiza la petición `fetch` normalmente:

```javascript
fetch('https://dekandela.com.mx/api-estados.php')
  .then(res => res.json())
  .then(data => console.log(data))
  .catch(err => console.error(err));
```

3. Si todo está correcto, el navegador **ya no bloqueará** la petición y podrás recibir los datos.

---

## 4️⃣ Notas importantes

* Las cabeceras deben enviarse **antes de cualquier salida** en PHP.
* Si usas **autenticación o cookies**, es posible que necesites agregar:

```php
header("Access-Control-Allow-Credentials: true");
```

* Evita usar `*` en producción si quieres **controlar qué dominios pueden acceder**.
