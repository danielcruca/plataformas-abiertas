
# 📘 Consultas en MongoDB - Parte 2


# 🔧 ¿Cómo funciona?
Un pipeline de agregación es como una línea de producción en la que vas procesando los datos paso por paso.

Cada paso se llama una etapa (stage), y podés  combinarlas. Las más comunes son:

| Etapa      | ¿Qué hace?                                               | Ejemplo simple                                 |
|------------|----------------------------------------------------------|------------------------------------------------|
| `$match`   | Filtra documentos (como un WHERE)                        | Solo ventas del 2025                           |
| `$group`   | Agrupa documentos y calcula valores (como un GROUP BY)   | Total vendido por producto                     |
| `$sort`    | Ordena los resultados                                    | De mayor a menor cantidad vendida              |
| `$project` | Escoge y transforma los campos que querés mostrar        | Mostrar solo nombre y total                    |
| `$limit`   | Muestra solo cierta cantidad                             | Los 5 productos más vendidos                   |
| `$lookup`  | Une datos de otra colección (como un JOIN en SQL)        | Buscar el stock del producto en otra tabla     |


## 1. Agregaciones con `$aggregate`

Las agregaciones permiten procesar datos y devolver resultados resumidos. Se usan etapas como `$match`, `$group`, `$sort`, `$project`, entre otras.

---

### a. 📅 Cantidad vendida de prendas por fecha específica

**Conceptos:**
- Filtrado con `$match`
- Agrupación con `$group`
- Ordenamiento con `$sort`

```js
db.ventas.aggregate([
  {
    $match: {
      fecha_venta: new Date("2025-05-31") //  Fecha específica
    }
  },
  {
    $group: {
      _id: "$libro.titulo", // Agrupar por título del libro
      cantidad_vendida: { $sum: "$cantidad" } // Sumar cantidad vendida
    }
  },
  {
    $sort: { cantidad_vendida: -1 } // Ordenar de mayor a menor
  }
]);
```


---

### b. 📚 Libros con al menos una venta

**Opciones:**
- `$group` para agrupar por libro
- `$match` para filtrar resultados después
- `$lookup` (opcional) para combinar con otra colección

```js
db.ventas.aggregate([
  {
    $group: {
      _id: "$libro.titulo",         // Agrupar por título
      total_ventas: { $sum: 1 }     // Contar ventas
    }
  },
  {
    $sort: { total_ventas: -1 }     // Ordenar por más vendidos
  }
]);
```

---

### c. 📦 Libros vendidas y su stock restante

**Conceptos:**
- `$lookup` para combinar con libros
- `$project` para mostrar campos personalizados

```js
db.ventas.aggregate([
  {
    $group: {
      _id: "$libro.titulo",                   // Agrupar por título
      cantidadVendida: { $sum: "$cantidad" }  // Sumar cantidad vendida
    }
  },
  {
    $lookup: {
      from: "libros",                         // Buscar en colección 'libros'
      localField: "_id",                      // Título agrupado
      foreignField: "titulo",                 // Título en libros
      as: "info_libro"
    }
  },
  {
    $unwind: "$info_libro"                    // Descomponer el array
  },
  {
    $project: {
      _id: 0,
      titulo: "$_id",
      cantidadVendida: 1,
      stockTotal: "$info_libro.cantidad_stock"
    }
  },
  {
    $sort: { cantidadVendida: -1 }            // Ordenar por más vendidos
  }
]);
```

---

### d. 🏆 Top 5 libros más vendidos

**Pasos:**
1. Agrupar por título
2. Sumar cantidades
3. Ordenar
4. Limitar

```js
db.ventas.aggregate([
  {
    $group: {
      _id: "$libro.titulo",                  // Agrupar por título
      cantidadVendida: { $sum: "$cantidad" }
    }
  },
  {
    $sort: { cantidadVendida: -1 }           // Ordenar descendente
  },
  {
    $limit: 5                                // Limitar a top 5
  }
]);
```

---

### Ejemplo sencillo

Obtener todos los libros por autor.

```js
db.libros.aggregate([
  {
    $group: {
      _id: "$autor",            // Agrupa por nombre del autor
      totalLibros: { $sum: 1 }  // Cuenta cuántos libros tiene cada autor
    }
  },
  {
    $sort: { totalLibros: -1 }  // Ordena de mayor a menor cantidad
  }
]);

```
