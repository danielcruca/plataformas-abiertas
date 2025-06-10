# Eliminar documentos en MongoDB

MongoDB permite borrar documentos de una colección usando los métodos `deleteOne()` y `deleteMany()`.

---

## Sintaxis básica

```js
db.collection.deleteOne({ filtro });   // Borra un solo documento que cumple el filtro
db.collection.deleteMany({ filtro });  // Borra todos los documentos que cumplen el filtro
```

Ejemplo:
```js
    db.libros.deleteMany({ "autor.nombre": "Julio", "autor.apellido": "Cortázar" });
    // o
    db.libros.deleteOne({ _id: ObjectId("64b9f8e5a1c2b3d456789012") });

```