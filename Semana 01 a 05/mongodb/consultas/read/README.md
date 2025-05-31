
# 📚 Consultas en MongoDB vs SQL

Aquí una guía práctica de consultas comunes en **MongoDB** junto a su equivalente en **SQL** tradicional.

---

## 🔹 1. Obtener todos los libros

### 📦 MongoDB
```javascript
db.libros.find()
```

### 🧮 SQL
```sql
SELECT * FROM libros;
```

---

## 🔹 2. Filtrar por ID de libro

### 📦 MongoDB
```javascript
db.libros.find({
  _id: ObjectId("6823e02cea9cb5e5156c4bd4")
})
```

### 🧮 SQL
```sql
SELECT * FROM libros 
WHERE id = '6823e02cea9cb5e5156c4bd4';
```

---

## 🔹 3. Filtrar por nombre y apellido del autor

### 📦 MongoDB
```javascript
db.libros.find({
  "autor.nombre": "Isabel",
  "autor.apellido": "Allende"
})
```

### 🧮 SQL
```sql
SELECT * FROM libros 
WHERE autor_nombre = 'Isabel' 
  AND autor_apellido = 'Allende';
```

---

## 🔹 4. Buscar libros con más de 5 unidades en stock

> `$gt` → **mayor que**

### 📦 MongoDB
```javascript
db.libros.find({
  "cantidad_stock": { $gt: 5 }
})
```

### 🧮 SQL
```sql
SELECT * FROM libros 
WHERE cantidad_stock > 5;
```

---

## 🔹 5. Otros operadores de comparación

### 🔸 `$lt` → menor que
```javascript
db.libros.find({
  "cantidad_stock": { $lt: 10 }
})
```

### 🔸 `$lte` → menor o igual que
```javascript
db.libros.find({
  "cantidad_stock": { $lte: 5 }
})
```

### 🔸 `$gte` → mayor o igual que
```javascript
db.libros.find({
  "cantidad_stock": { $gte: 20 }
})
```

---

## 🔹 6. Contar cantidad de libros

### 📦 MongoDB
```javascript
db.libros.countDocuments()
```

### 🧮 SQL
```sql
SELECT COUNT(*) FROM libros;
```

