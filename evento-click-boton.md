# 🛠️ Mini Tutorial: Detectar evento click de un botón en JavaScript

Detectar cuando un usuario hace clic en un botón se logra fácilmente usando el evento `click`.

---

## 1️⃣ Usando `addEventListener` (recomendado)

```html
<button id="miBoton">Haz clic aquí</button>

<script>
const boton = document.getElementById('miBoton');

boton.addEventListener('click', () => {
  console.log('¡Botón clickeado!');
  alert('¡Has presionado el botón!');
});
</script>
```

### ✅ Explicación

1. `getElementById('miBoton')`: Obtiene la referencia al botón.
2. `addEventListener('click', ...)`: Escucha el evento clic.
3. La función dentro del listener se ejecuta cada vez que se hace clic en el botón.

---

💡 **Tip:** `addEventListener` es más flexible que `onclick` y permite asignar múltiples funciones al mismo botón sin reemplazarlas.
