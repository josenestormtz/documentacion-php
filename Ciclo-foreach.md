# 🛠️ Mini Tutorial: Ciclo forEach con Arrow Functions en JavaScript

`forEach` es una función que permite recorrer **arreglos** y ejecutar una función para cada elemento. Usar **arrow functions** hace el código más limpio y moderno.

---

## 1️⃣ Sintaxis básica con arrow function

```javascript
const frutas = ['Manzana', 'Plátano', 'Cereza'];

frutas.forEach(fruta => console.log(fruta));
```

**Salida:**

```
Manzana
Plátano
Cereza
```

---

## 2️⃣ Accediendo al índice

```javascript
const nombres = ['Ana', 'Luis', 'Carlos'];

nombres.forEach((nombre, indice) => {
  console.log(`${indice}: ${nombre}`);
});
```

**Salida:**

```
0: Ana
1: Luis
2: Carlos
```

---

## 3️⃣ Con un arreglo de objetos

```javascript
const usuarios = [
  { id: 1, nombre: 'Néstor' },
  { id: 2, nombre: 'María' },
  { id: 3, nombre: 'Pedro' }
];

usuarios.forEach(usuario => {
  console.log(`ID: ${usuario.id}, Nombre: ${usuario.nombre}`);
});
```

**Salida:**

```
ID: 1, Nombre: Néstor
ID: 2, Nombre: María
ID: 3, Nombre: Pedro
```

---

## 💡 Notas importantes

1. No se puede usar `break` o `continue` dentro de `forEach`.
2. Ideal para ejecutar acciones por cada elemento, pero no modificar directamente el arreglo.
3. Para modificar valores de un arreglo, considera usar `map()`.
