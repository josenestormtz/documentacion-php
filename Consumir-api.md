# 🛠️ Mini Tutorial: Consumir una API con fetch en JavaScript

Una vez que la API permite CORS, podemos consumirla fácilmente desde el navegador usando JavaScript.

---

## 1️⃣ Usando `fetch` con `async/await` (recomendado)

```javascript
const url = 'https://dekandela.com.mx/api-estados.php';

async function obtenerDatos() {
  try {
    const response = await fetch(url);

    if (!response.ok) {
      throw new Error(`Error HTTP: ${response.status}`);
    }

    const data = await response.json(); // Convertimos la respuesta a JSON
    console.log('Datos recibidos:', data);
  } catch (error) {
    console.error('Hubo un problema con la petición:', error);
  }
}

obtenerDatos();
```

### ✅ Explicación paso a paso

1. **`fetch(url)`**: Realiza la petición GET a la API.
2. **`await response.json()`**: Convierte la respuesta a formato JSON.
3. **`if (!response.ok)`**: Verifica que la respuesta HTTP sea correcta (200-299).
4. **`try/catch`**: Captura errores de la petición o de la conversión a JSON.
5. **`obtenerDatos()`**: Llama a la función para ejecutar la petición.

---

### 💡 Tip adicional

Si tu API requiere **parámetros**, agrégalos directamente a la URL:

```javascript
const estado = 'CDMX';
const url = `https://dekandela.com.mx/api-estados.php?estado=${estado}`;
```
