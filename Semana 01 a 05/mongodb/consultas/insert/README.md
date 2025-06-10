# Insertar documentos en MongoDB

MongoDB permite insertar nuevos documentos en una colección usando el método `insertOne()`.

---

## Sintaxis básica

```js
db.collection.insertOne(documento);
```
Ejemplo:

```js   
    db.libros.insertOne({
    titulo: "El túnel",
    autor: {
        nombre: "Ernesto",
        apellido: "Sábato",
        nacionalidad: "Argentina"
    },
    precio: 14.5,
    cantidad_stock: 25
    });
```
Insertar varios documentos a la vez:

```js
    db.libros.insertMany([
    

])
```
Ejemplo:

```js
// Insertar varios libros
db.libros.insertMany([
  {
    titulo: "Ficciones",
    autor: {
      nombre: "Jorge Luis",
      apellido: "Borges",
      nacionalidad: "Argentina"
    },
    precio: 13.5,
    cantidad_stock: 18
  },
  {
    titulo: "Aura",
    autor: {
      nombre: "Carlos",
      apellido: "Fuentes",
      nacionalidad: "México"
    },
    precio: 12.0,
    cantidad_stock: 22
  }
]);
```