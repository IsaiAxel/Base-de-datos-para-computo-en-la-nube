## Practica 5 Agregaciones

- Para hacer esta práctica vamos a cargar unos datos ficticios de empresas.
- Tienes un fichero denominado “productos.json”
- Debes poner el resultado de las consultas en cada apartado

1. Cuenta los productos de tipo “medio”, usando un método básico

db.productos.countDocuments({ tipo: "medio" })

- Resultado : "25"

2. Indicar con un distinct, las empresas (fabricantes) que hay en la colección

db.productos.distinct("fabricante")


- Resultado

[
  'A.O. Smith',
  'Alere',
  'American Tire Distributors Holdings',
  'Anthem',
  'Archrock',
  'Ascena Retail Group',
  'AutoNation',
  'Best Buy',
  'CIT Group',
  'Cabot',
  'Comcast',
  'Comerica',
  'Core-Mark Holding',
  'DST Systems',
  'Darling Ingredients',
  'Delta Air Lines',
  'Delta Tucker Holdings',
  "Dick's Sporting Goods",
  'First Solar',
  'HCA Holdings',
  'Hanesbrands',
  'Hartford Financial Services Group',
  'Hawaiian Holdings',
  'HealthSouth',
  'Hyatt Hotels',
  'Kar Auction Services',
  'Kelly Services',
  'Kemper',
  'Kimberly-Clark',
  'Lennar',
  'Mercury General',
  'Mondelez International',
  'Motorola Solutions',
  'Nasdaq OMX Group',
  'National Oilwell Varco',
  'Nordstrom',
  'OneMain Holdings',
  'Oneok',
  'Orbital ATK',
  'Pep Boys-Mann',
  'Pool',
  'Precision Castparts',
  'Primoris Services',
  'Raymond James Financial',
  'Seaboard',
  'Securian Financial Group',
  'Simon Property Group',
  'State Farm Insurance Cos.',
  'State Street Corp.',
  'SunPower',
  'TEGNA',
  'Telephone & Data Systems',
  'Total System Services',
  'Tractor Supply',
  'TransDigm Group',
  'Trinity Industries',
  'TrueBlue',
  'Universal American',
  'Universal Health Services',
  'WGL Holdings',
  "Wendy's",
  'Werner Enterprises',
  'WestRock',
  'Williams-Sonoma'
]

3. Usando aggregate, visualizar los productos que tengan más de 80 unidades

db.productos.aggregate([
  { $match: { unidades: { $gt: 80 } } }
])

- Resultado
{
  _id: ObjectId('67d9c9b0007c4fb5a39cdaa8'),
  codigo: 0,
  nombre: 'Fantastic Wooden Fish',
  unidades: 95,
  precio: 291,
  fabricante: 'Kimberly-Clark',
  tipo: 'avanzado'
}
{
  _id: ObjectId('67d9c9b0007c4fb5a39cdaaa'),
  codigo: 2,
  nombre: 'Small Soft Fish',
  unidades: 96,
  precio: 189,
  fabricante: 'Primoris Services',
  tipo: 'medio'
}
{
  _id: ObjectId('67d9c9b0007c4fb5a39cdab4'),
  codigo: 12,
  nombre: 'Refined Concrete Salad',
  unidades: 90,
  precio: 129,
  fabricante: 'Universal Health Services',
  tipo: 'avanzado'
}
{
  _id: ObjectId('67d9c9b0007c4fb5a39cdac6'),
  codigo: 30,
  nombre: 'Small Rubber Pants',
  unidades: 89,
  precio: 16,
  fabricante: 'Hanesbrands',
  tipo: 'basico'
}
{
  _id: ObjectId('67d9c9b0007c4fb5a39cdac9'),
  codigo: 33,
  nombre: 'Generic Concrete Hat',
  unidades: 82,
  precio: 70,
  fabricante: 'American Tire Distributors Holdings',
  tipo: 'basico'
}
{
  _id: ObjectId('67d9c9b0007c4fb5a39cdadd'),
  codigo: 53,
  nombre: 'Licensed Plastic Hat',
  unidades: 96,
  precio: 38,
  fabricante: 'Best Buy',
  tipo: 'medio'
}
{
  _id: ObjectId('67d9c9b0007c4fb5a39cdade'),
  codigo: 54,
  nombre: 'Generic Metal Sausages',
  unidades: 84,
  precio: 77,
  fabricante: 'DST Systems',
  tipo: 'medio'
}
{
  _id: ObjectId('67d9c9b0007c4fb5a39cdae5'),
  codigo: 61,
  nombre: 'Sleek Rubber Keyboard',
  unidades: 82,
  precio: 33,
  fabricante: 'Alere',
  tipo: 'basico'
}
{
  _id: ObjectId('67d9c9b0007c4fb5a39cdaea'),
  codigo: 66,
  nombre: 'Incredible Concrete Fish',
  unidades: 96,
  precio: 336,
  fabricante: 'Darling Ingredients',
  tipo: 'medio'
}
4. Con $project visualizar solo el nombre, unidades y precio de los productos que tengan menos de 10 unidades

db.productos.aggregate([
  { $match: { unidades: { $lt: 10 } } },
  { $project: { nombre: 1, unidades: 1, precio: 1, _id: 0 } }
])

- Resultado 
{
  nombre: 'Ergonomic Metal Ball',
  unidades: 5,
  precio: 246
}
{
  nombre: 'Handmade Plastic Hat',
  unidades: 7,
  precio: 253
}
{
  nombre: 'Ergonomic Metal Table',
  unidades: 0,
  precio: 94
}
{
  nombre: 'Practical Frozen Chips',
  unidades: 0,
  precio: 305
}
{
  nombre: 'Fantastic Metal Pants',
  unidades: 5,
  precio: 129
}
{
  nombre: 'Intelligent Frozen Sausages',
  unidades: 3,
  precio: 111
}
{
  nombre: 'Rustic Plastic Mouse',
  unidades: 5,
  precio: 24
}

5. Con $project ponemos el fabricante pero le cambiamos el nombre por “empresa”. Usamos el mismo comando anterior

 db.productos.aggregate([
  { $match: { unidades: { $lt: 10 } } },
  { 
    $project: { 
      nombre: 1, 
      unidades: 1, 
      precio: 1, 
      empresa: "$fabricante",
      _id: 0 
    } 
  }
])

- Resultado 
{
  nombre: 'Ergonomic Metal Ball',
  unidades: 5,
  precio: 246,
  empresa: 'Seaboard'
}
{
  nombre: 'Handmade Plastic Hat',
  unidades: 7,
  precio: 253,
  empresa: "Dick's Sporting Goods"
}
{
  nombre: 'Ergonomic Metal Table',
  unidades: 0,
  precio: 94,
  empresa: 'Kelly Services'
}
{
  nombre: 'Practical Frozen Chips',
  unidades: 0,
  precio: 305,
  empresa: 'Delta Air Lines'
}
{
  nombre: 'Fantastic Metal Pants',
  unidades: 5,
  precio: 129,
  empresa: 'OneMain Holdings'
}
{
  nombre: 'Intelligent Frozen Sausages',
  unidades: 3,
  precio: 111,
  empresa: 'A.O. Smith'
}
{
  nombre: 'Rustic Plastic Mouse',
  unidades: 5,
  precio: 24,
  empresa: 'Orbital ATK'
}

6. Añadir a la consulta anterior un campo calculado que se llame total y que multiplique precio por unidades.

db.productos.aggregate([
  { $match: { unidades: { $lt: 10 } } },
  { 
    $project: { 
      nombre: 1, 
      unidades: 1, 
      precio: 1, 
      empresa: "$fabricante",
      total: { $multiply: ["$precio", "$unidades"] },
      _id: 0
    } 
  }
])

- Resultado
{
  nombre: 'Ergonomic Metal Ball',
  unidades: 5,
  precio: 246,
  empresa: 'Seaboard',
  total: 1230
}
{
  nombre: 'Handmade Plastic Hat',
  unidades: 7,
  precio: 253,
  empresa: "Dick's Sporting Goods",
  total: 1771
}
{
  nombre: 'Ergonomic Metal Table',
  unidades: 0,
  precio: 94,
  empresa: 'Kelly Services',
  total: 0
}
{
  nombre: 'Practical Frozen Chips',
  unidades: 0,
  precio: 305,
  empresa: 'Delta Air Lines',
  total: 0
}
{
  nombre: 'Fantastic Metal Pants',
  unidades: 5,
  precio: 129,
  empresa: 'OneMain Holdings',
  total: 645
}
{
  nombre: 'Intelligent Frozen Sausages',
  unidades: 3,
  precio: 111,
  empresa: 'A.O. Smith',
  total: 333
}
{
  nombre: 'Rustic Plastic Mouse',
  unidades: 5,
  precio: 24,
  empresa: 'Orbital ATK',
  total: 120
}
7. Hacer que el nombre salga en mayúsculas con el operador $toUpper

db.productos.aggregate([
  { $project: { nombreMayus: { $toUpper: "$nombre" }, _id: 0 } }
])

- Resultado 
{
  nombreMayus: 'FANTASTIC WOODEN FISH'
}
{
  nombreMayus: 'RUSTIC CONCRETE PANTS'
}
{
  nombreMayus: 'SMALL SOFT FISH'
}
{
  nombreMayus: 'PRACTICAL SOFT PANTS'
}
{
  nombreMayus: 'ERGONOMIC METAL BALL'
}
{
  nombreMayus: 'SMALL STEEL GLOVES'
}
{
  nombreMayus: 'HANDMADE STEEL CHAIR'
}
{
  nombreMayus: 'HANDCRAFTED SOFT GLOVES'
}
{
  nombreMayus: 'FANTASTIC CONCRETE SALAD'
}
{
  nombreMayus: 'HANDMADE PLASTIC HAT'
}
{
  nombreMayus: 'REFINED WOODEN TUNA'
}
{
  nombreMayus: 'REFINED CONCRETE SALAD'
}
{
  nombreMayus: 'SMALL CONCRETE FISH'
}
{
  nombreMayus: 'REFINED CONCRETE BIKE'
}
{
  nombreMayus: 'TASTY COTTON PANTS'
}
{
  nombreMayus: 'INCREDIBLE GRANITE GLOVES'
}
{
  nombreMayus: 'PRACTICAL METAL MOUSE'
}

8. Añadir un campo calculado que ponga el nombre del producto y el tipo concatenado con el operador $concat. Le llamamos al campo “completo”

db.productos.aggregate([
  {
    $project: {
      nombre: 1,
      tipo: 1,
      completo: { $concat: ["$nombre", " - ", "$tipo"] },
      _id: 0
    }
  }
])

- Resultado

{
  nombre: 'Fantastic Wooden Fish',
  tipo: 'avanzado',
  completo: 'Fantastic Wooden Fish - avanzado'
}
{
  nombre: 'Rustic Concrete Pants',
  tipo: 'medio',
  completo: 'Rustic Concrete Pants - medio'
}
{
  nombre: 'Small Soft Fish',
  tipo: 'medio',
  completo: 'Small Soft Fish - medio'
}
{
  nombre: 'Practical Soft Pants',
  tipo: 'avanzado',
  completo: 'Practical Soft Pants - avanzado'
}
{
  nombre: 'Ergonomic Metal Ball',
  tipo: 'medio',
  completo: 'Ergonomic Metal Ball - medio'
}
{
  nombre: 'Small Steel Gloves',
  tipo: 'avanzado',
  completo: 'Small Steel Gloves - avanzado'
}
{
  nombre: 'Ergonomic Wooden Shirt',
  tipo: 'avanzado',
  completo: 'Ergonomic Wooden Shirt - avanzado'
}
{
  nombre: 'Handmade Steel Chair',
  tipo: 'medio',
  completo: 'Handmade Steel Chair - medio'
}
{
  nombre: 'Handcrafted Soft Gloves',
  tipo: 'basico',
  completo: 'Handcrafted Soft Gloves - basico'
}
{
  nombre: 'Fantastic Concrete Salad',
  tipo: 'basico',
  completo: 'Fantastic Concrete Salad - basico'
}
{
  nombre: 'Handmade Plastic Hat',
  tipo: 'medio',
  completo: 'Handmade Plastic Hat - medio'
}
{
  nombre: 'Refined Wooden Tuna',
  tipo: 'avanzado',
  completo: 'Refined Wooden Tuna - avanzado'
}
{
  nombre: 'Refined Concrete Salad',
  tipo: 'avanzado',
  completo: 'Refined Concrete Salad - avanzado'
}
{
  nombre: 'Unbranded Soft Fish',
  tipo: 'basico',
  completo: 'Unbranded Soft Fish - basico'
}
{
  nombre: 'Small Concrete Fish',
  tipo: 'medio',
  completo: 'Small Concrete Fish - medio'
}
{
  nombre: 'Refined Concrete Bike',
  tipo: 'basico',
  completo: 'Refined Concrete Bike - basico'
}
{
  nombre: 'Tasty Cotton Pants',
  tipo: 'basico',
  completo: 'Tasty Cotton Pants - basico'
}
{
  nombre: 'Incredible Granite Gloves',
  tipo: 'avanzado',
  completo: 'Incredible Granite Gloves - avanzado'
}
{
  nombre: 'Practical Metal Mouse',
  tipo: 'basico',
  completo: 'Practical Metal Mouse - basico'
}
{
  nombre: 'Handcrafted Steel Chicken',
  tipo: 'medio',
  completo: 'Handcrafted Steel Chicken - medio'
}

9.  Ordena el resultado por el campo “total”

db.productos.aggregate([
  { 
    $project: { 
      nombre: 1, 
      tipo: 1, 
      total: { $multiply: ["$precio", "$unidades"] }, 
      completo: { $concat: ["$nombre", " - ", "$tipo"] } 
    }
  },
  { $sort: { total: -1 } }
])

- Resultado
{
  _id: ObjectId('67d9c9b0007c4fb5a39cdaea'),
  nombre: 'Incredible Concrete Fish',
  tipo: 'medio',
  total: 32256,
  completo: 'Incredible Concrete Fish - medio'
}
{
  _id: ObjectId('67d9c9b0007c4fb5a39cdaa8'),
  nombre: 'Fantastic Wooden Fish',
  tipo: 'avanzado',
  total: 27645,
  completo: 'Fantastic Wooden Fish - avanzado'
}
{
  _id: ObjectId('67d9c9b0007c4fb5a39cdacc'),
  nombre: 'Rustic Soft Table',
  tipo: 'medio',
  total: 24163,
  completo: 'Rustic Soft Table - medio'
}
{
  _id: ObjectId('67d9c9b0007c4fb5a39cdae1'),
  nombre: 'Practical Fresh Fish',
  tipo: 'avanzado',
  total: 22839,
  completo: 'Practical Fresh Fish - avanzado'
}
{
  _id: ObjectId('67d9c9b0007c4fb5a39cdab9'),
  nombre: 'Incredible Granite Gloves',
  tipo: 'avanzado',
  total: 20590,
  completo: 'Incredible Granite Gloves - avanzado'
}
{
  _id: ObjectId('67d9c9b0007c4fb5a39cdabf'),
  nombre: 'Handcrafted Metal Tuna',
  tipo: 'medio',
  total: 20160,
  completo: 'Handcrafted Metal Tuna - medio'
}
{
  _id: ObjectId('67d9c9b0007c4fb5a39cdaa9'),
  nombre: 'Rustic Concrete Pants',
  tipo: 'medio',
  total: 18414,
  completo: 'Rustic Concrete Pants - medio'
}
{
  _id: ObjectId('67d9c9b0007c4fb5a39cdaaa'),
  nombre: 'Small Soft Fish',
  tipo: 'medio',
  total: 18144,
  completo: 'Small Soft Fish - medio'
}
{
  _id: ObjectId('67d9c9b0007c4fb5a39cdad1'),
  nombre: 'Awesome Cotton Cheese',
  tipo: 'basico',
  total: 15512,
  completo: 'Awesome Cotton Cheese - basico'
}
{
  _id: ObjectId('67d9c9b0007c4fb5a39cdac1'),
  nombre: 'Licensed Fresh Chicken',
  tipo: 'basico',
  total: 15145,
  completo: 'Licensed Fresh Chicken - basico'
}
{
  _id: ObjectId('67d9c9b0007c4fb5a39cdaae'),
  nombre: 'Ergonomic Wooden Shirt',
  tipo: 'avanzado',
  total: 14994,
  completo: 'Ergonomic Wooden Shirt - avanzado'
}
{
  _id: ObjectId('67d9c9b0007c4fb5a39cdab1'),
  nombre: 'Fantastic Concrete Salad',
  tipo: 'basico',
  total: 12985,
  completo: 'Fantastic Concrete Salad - basico'
}
{
  _id: ObjectId('67d9c9b0007c4fb5a39cdacf'),
  nombre: 'Handmade Soft Chips',
  tipo: 'medio',
  total: 11648,
  completo: 'Handmade Soft Chips - medio'
}
{
  _id: ObjectId('67d9c9b0007c4fb5a39cdabe'),
  nombre: 'Unbranded Soft Table',
  tipo: 'avanzado',
  total: 11644,
  completo: 'Unbranded Soft Table - avanzado'
}
{
  _id: ObjectId('67d9c9b0007c4fb5a39cdab4'),
  nombre: 'Refined Concrete Salad',
  tipo: 'avanzado',
  total: 11610,
  completo: 'Refined Concrete Salad - avanzado'
}
{
  _id: ObjectId('67d9c9b0007c4fb5a39cdae8'),
  nombre: 'Awesome Cotton Mouse',
  tipo: 'basico',
  total: 11115,
  completo: 'Awesome Cotton Mouse - basico'
}

{
  _id: ObjectId('67d9c9b0007c4fb5a39cdae4'),
  nombre: 'Practical Frozen Salad',
  tipo: 'basico',
  total: 10750,
  completo: 'Practical Frozen Salad - basico'
}
{
  _id: ObjectId('67d9c9b0007c4fb5a39cdae4'),
  nombre: 'Practical Frozen Salad',
  tipo: 'basico',
  total: 10750,
  completo: 'Practical Frozen Salad - basico'
}
{
  _id: ObjectId('67d9c9b0007c4fb5a39cdab5'),
  nombre: 'Unbranded Soft Fish',
  tipo: 'basico',
  total: 9434,
  completo: 'Unbranded Soft Fish - basico'
}
{
  _id: ObjectId('67d9c9b0007c4fb5a39cdac2'),
  nombre: 'Intelligent Plastic Bike',
  tipo: 'medio',
  total: 9399,
  completo: 'Intelligent Plastic Bike - medio'
}

10.  Haciendo una nueva consulta, averiguar el numero de productos por tipo de producto

db.productos.aggregate([
  { $group: { _id: "$tipo", cantidad: { $sum: 1 } } }
])

- Resultado 

{
  _id: 'medio',
  cantidad: 25
}
{
  _id: 'basico',
  cantidad: 24
}
{
  _id: 'avanzado',
  cantidad: 18
}

11. Añadir el valor mayor y el menor

db.productos.aggregate([
  {
    $group: {
      _id: null,
      maxPrecio: { $max: "$precio" },
      minPrecio: { $min: "$precio" }
    }
  }
])

- Resultado 
{
  _id: null,
  maxPrecio: 337,
  minPrecio: 16
}

12. Añade el total de unidades por cada tipo

db.productos.aggregate([
  { $group: { _id: "$tipo", totalUnidades: { $sum: "$unidades" } } }
])

- Resultado
{
  _id: 'avanzado',
  totalUnidades: 773
}
{
  _id: 'medio',
  totalUnidades: 1224
}
{
  _id: 'basico',
  totalUnidades: 1067
}

13. Con el operador $set y el operador “$substr” visualiza todos los datos del producto "Small Metal Tuna" y los primeros 5 caracteres del nombre.

 db.productos.aggregate([
  { $match: { nombre: "Small Metal Tuna" } },
  {
    $set: {
      primeros5: { $substr: ["$nombre", 0, 5] }
    }
  }
])

- Resultado 

{
  _id: ObjectId('67d9c9b0007c4fb5a39cdadf'),
  codigo: 55,
  nombre: 'Small Metal Tuna',
  unidades: 46,
  precio: 43,
  fabricante: 'Raymond James Financial',
  tipo: 'medio',
  primeros5: 'Small'
}

14. Creamos una salida que tenga el nombre del articulo y el total (precio por unidades) y lo guardamos en una colección denominada productos2

db.productos.aggregate([
  {
    $project: {
      nombre: 1,
      total: { $multiply: ["$precio", "$unidades"] },
      _id: 0
    }
  },
  { $out: "productos2" }
])

- Resultado : null

15. Comprobamos que se ha creado

show collections

- Resultado cazas
Cazas
Ciudades
Ejemplo
Ejemplo2
libros
personas
productos
productos2

16. Hacemos un find para comprobar el resultado
db.productos2.find()

- Resultado 

{
  _id: ObjectId('67d9d8f6ea6debb4518bcdd7'),
  nombre: 'Fantastic Wooden Fish',
  total: 27645
}
{
  _id: ObjectId('67d9d8f6ea6debb4518bcdd8'),
  nombre: 'Rustic Concrete Pants',
  total: 18414
}
{
  _id: ObjectId('67d9d8f6ea6debb4518bcdd9'),
  nombre: 'Small Soft Fish',
  total: 18144
}
{
  _id: ObjectId('67d9d8f6ea6debb4518bcdda'),
  nombre: 'Practical Soft Pants',
  total: 2747
}
{
  _id: ObjectId('67d9d8f6ea6debb4518bcddb'),
  nombre: 'Ergonomic Metal Ball',
  total: 1230
}
{
  _id: ObjectId('67d9d8f6ea6debb4518bcddc'),
  nombre: 'Small Steel Gloves',
  total: 1665
}
{
  _id: ObjectId('67d9d8f6ea6debb4518bcddd'),
  nombre: 'Ergonomic Wooden Shirt',
  total: 14994
}
{
  _id: ObjectId('67d9d8f6ea6debb4518bcdde'),
  nombre: 'Handmade Steel Chair',
  total: 5392
}
{
  _id: ObjectId('67d9d8f6ea6debb4518bcddf'),
  nombre: 'Handcrafted Soft Gloves',
  total: 4512
}
{
  _id: ObjectId('67d9d8f6ea6debb4518bcde0'),
  nombre: 'Fantastic Concrete Salad',
  total: 12985
}
{
  _id: ObjectId('67d9d8f6ea6debb4518bcde1'),
  nombre: 'Handmade Plastic Hat',
  total: 1771
}
{
  _id: ObjectId('67d9d8f6ea6debb4518bcde2'),
  nombre: 'Refined Wooden Tuna',
  total: 8480
}
{
  _id: ObjectId('67d9d8f6ea6debb4518bcde3'),
  nombre: 'Refined Concrete Salad',
  total: 11610
}
{
  _id: ObjectId('67d9d8f6ea6debb4518bcde4'),
  nombre: 'Unbranded Soft Fish',
  total: 9434
}
{
  _id: ObjectId('67d9d8f6ea6debb4518bcde5'),
  nombre: 'Small Concrete Fish',
  total: 5040
}
{
  _id: ObjectId('67d9d8f6ea6debb4518bcde6'),
  nombre: 'Refined Concrete Bike',
  total: 2700
}
{
  _id: ObjectId('67d9d8f6ea6debb4518bcde7'),
  nombre: 'Tasty Cotton Pants',
  total: 3536
}
{
  _id: ObjectId('67d9d8f6ea6debb4518bcde8'),
  nombre: 'Incredible Granite Gloves',
  total: 20590
}
{
  _id: ObjectId('67d9d8f6ea6debb4518bcde9'),
  nombre: 'Practical Metal Mouse',
  total: 6650
}
{
  _id: ObjectId('67d9d8f6ea6debb4518bcdea'),
  nombre: 'Handcrafted Steel Chicken',
  total: 6215
}

17. Usando $cond y $project vamos a visualizar el nombre del producto, el precio y un campo llamado valoración que ponga “barato” si el precio es menor de 250 y caro si es mayor o igual

db.productos.aggregate([
  {
    $project: {
      nombre: 1,
      precio: 1,
      valoracion: {
        $cond: { if: { $lt: ["$precio", 250] }, then: "barato", else: "caro" }
      },
      _id: 0
    }
  }
])

- Resultado 
{
  nombre: 'Fantastic Wooden Fish',
  precio: 291,
  valoracion: 'caro'
}
{
  nombre: 'Rustic Concrete Pants',
  precio: 279,
  valoracion: 'caro'
}
{
  nombre: 'Small Soft Fish',
  precio: 189,
  valoracion: 'barato'
}
{
  nombre: 'Practical Soft Pants',
  precio: 67,
  valoracion: 'barato'
}
{
  nombre: 'Ergonomic Metal Ball',
  precio: 246,
  valoracion: 'barato'
}
{
  nombre: 'Small Steel Gloves',
  precio: 37,
  valoracion: 'barato'
}
{
  nombre: 'Ergonomic Wooden Shirt',
  precio: 238,
  valoracion: 'barato'
}
{
  nombre: 'Handmade Steel Chair',
  precio: 337,
  valoracion: 'caro'
}
{
  nombre: 'Handcrafted Soft Gloves',
  precio: 282,
  valoracion: 'caro'
}
{
  nombre: 'Fantastic Concrete Salad',
  precio: 265,
  valoracion: 'caro'
}
{
  nombre: 'Handmade Plastic Hat',
  precio: 253,
  valoracion: 'caro'
}
{
  nombre: 'Refined Wooden Tuna',
  precio: 212,
  valoracion: 'barato'
}
{
  nombre: 'Refined Concrete Salad',
  precio: 129,
  valoracion: 'barato'
}
{
  nombre: 'Unbranded Soft Fish',
  precio: 178,
  valoracion: 'barato'
}
{
  nombre: 'Small Concrete Fish',
  precio: 126,
  valoracion: 'barato'
}
{
  nombre: 'Refined Concrete Bike',
  precio: 180,
  valoracion: 'barato'
}
{
  nombre: 'Tasty Cotton Pants',
  precio: 52,
  valoracion: 'barato'
}
{
  nombre: 'Incredible Granite Gloves',
  precio: 290,
  valoracion: 'caro'
}
{
  nombre: 'Practical Metal Mouse',
  precio: 190,
  valoracion: 'barato'
}
{
  nombre: 'Handcrafted Steel Chicken',
  precio: 113,
  valoracion: 'barato'
}
