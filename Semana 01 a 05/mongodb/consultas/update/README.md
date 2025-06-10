#
# Actualizar documentos en MongoDB

MongoDB permite modificar documentos existentes en una colección usando los métodos `updateOne()`, `updateMany()` o `replaceOne()`. La actualización se realiza con operadores especiales que indican qué cambiar.

---

## Sintaxis básica

```js
db.collection.updateOne(
  { filtro },                  // Documento(s) que quieres actualizar
  { $set: { campo: valor } }   // Cambios que quieres aplicar
);
```

- `updateOne()` actualiza solo el primer documento que cumple el filtro.
- `updateMany()` actualiza todos los documentos que cumplen el filtro.
- `replaceOne()` reemplaza todo el documento por uno nuevo.

---

## Operadores comunes para actualizar

| Operador | Descripción                           | Ejemplo                          |
| -------- | ------------------------------------ | --------------------------------|
| `$set`   | Cambia el valor de un campo          | `{ $set: { precio: 20 } }`       |
| `$inc`   | Incrementa o decrementa un valor     | `{ $inc: { cantidad: 1 } }`      |
| `$unset` | Elimina un campo del documento       | `{ $unset: { campo: "" } }`      |

---

## Ejemplos

### Actualizar un solo documento

Actualizar el precio del libro "Rayuela":

```js
db.libros.updateOne(
  { titulo: "Rayuela" },
  { $set: { precio: 20 } }
);
```

### Actualizar varios documentos

Aumentar en 5 el precio de todos los libros del autor "Julio Cortázar":

```js
db.libros.updateMany(
  { "autor.nombre": "Julio", "autor.apellido": "Cortázar" },
  { $inc: { precio: 3 } }
);

```

### Reemplazar un documento completo

Reemplazar todo el documento de "Rayuela":

```js
db.libros.updateOne(
  { titulo: "El túnel" },
  { $set: { precio: 15.0 } }
);
```

---
