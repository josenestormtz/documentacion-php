# 🛠️ Mini Tutorial: Cargar un <select> dinámicamente con JavaScript

Puedes llenar un <select> en HTML usando **arreglos locales** o **datos obtenidos desde una API**.

---

## 1️⃣ Usando un arreglo local

```html
<select id="miSelect"></select>

<script>
const select = document.getElementById('miSelect');
const opciones = ['CDMX', 'Jalisco', 'Nuevo León', 'Yucatán'];

opciones.forEach(opcion => {
  const elemento = document.createElement('option');
  elemento.value = opcion;        // Valor que se enviará al backend
  elemento.textContent = opcion;  // Texto que verá el usuario
  select.appendChild(elemento);
});
</script>
```

---

## 2️⃣ Usando datos desde una API

Supongamos que tu API devuelve un arreglo de objetos como:

```json
[
  { "id": 1, "estado": "CDMX" },
  { "id": 2, "estado": "Jalisco" },
  { "id": 3, "estado": "Nuevo León" }
]
```

```html
<select id="miSelect"></select>

<script>
const select = document.getElementById('miSelect');
const url = 'https://dekandela.com.mx/api-estados.php';

fetch(url)
  .then(res => res.json())
  .then(data => {
    data.forEach(item => {
      const opcion = document.createElement('option');
      opcion.value = item.id;         // id de cada estado
      opcion.textContent = item.estado; // nombre que verá el usuario
      select.appendChild(opcion);
    });
  })
  .catch(err => console.error('Error al cargar estados:', err));
</script>
```

---

## 3️⃣ Añadir un placeholder

Si quieres que la primera opción sea un mensaje como “Selecciona un estado”:

```javascript
const placeholder = document.createElement('option');
placeholder.textContent = 'Selecciona un estado';
placeholder.disabled = true;
placeholder.selected = true;
select.appendChild(placeholder);
```

---

💡 **Notas importantes:**

1. Siempre obtén la referencia del `<select>` con `getElementById` o `querySelector`.
2. `appendChild` agrega cada opción al final del `<select>`.
3. Con `fetch` puedes cargar datos de manera dinámica y mantener tu select actualizado automáticamente.
