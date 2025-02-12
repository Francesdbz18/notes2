```
db.products.insertMany([
  {
    "codigo": "B67890",
    "denominacion": "Auriculares Inalámbricos",
    "pvp": 49.99,
    "categoria": "Accesorios",
    "uv": 5,
    "stock": 100
  },
  {
    "codigo": "C23456",
    "denominacion": "Smartphone Modelo X",
    "pvp": 299.99,
    "categoria": "Electrónica",
    "uv": 15,
    "stock": 30
  }
]);

[{
  $project: {
    artículo: { $toUpper: "$denominación" }, 
    importe: { $multiply: ["$pvp", "$uv"] },
		stockactual: { $subtract: ["$stock", "$uv"] },
    areponer: {
			$cond: [{$lte: [{ $subtract: ["$stock", "$uv"] }, 0]}, true, false] }
  }
}
]
[{
 $group: {
   _id: "$categoria",
   contador: {$sum: 1},
   sumaunidades: { $sum: "$uv"},
   totalimporte: {$sum: {$multiply: ["$pvp", "$uv"]}}
 } 
}]
```
