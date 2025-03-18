# Consultas

1. Cargar el articulo empleados.json

En local:
Comando:

mongoimport --db curso --collection empleados --file empleados
json

Docker:
mongoimport --db curso --collection empleados --file empleados json --port 27018

2. Utilizar la base de datos curso
...json 
use curso
...

3. Buscar todos los empleados que trabajan en google

db.empleados.find({ empresa: "Google" })

4. Empleados que vivan en peru

b.empleados.find({ pais: "Peru" })

5. Empleados que ganen mas de 8000 dolares

db.empleados.find({ salario: { $gt: 8000 } })

6. Empleados con ventasa inferiores de 1000

db.empleados.find({ ventas: { $lt: 1000 } })

7. Realizar la consulta anterior pero devolviendo una sola fila

db.empleados.findOne({ ventas: { $lt: 1000 } })

8. Empleados que trabajan en google o yahoo con el operador $in

db.empleados.find({ empresa: { $in: ["Google", "Yahoo"] } })

9. Empleados de amazon que ganen mas de 9000 dolares

db.empleados.find({ 
  empresa: "Amazon", 
  salario: { $gt: 9000 } 
})

10. Empleados que trabajen en yahoo que gane mas de 6000 o empleados que trabajen en google que tengan ventas inferiores a 2000

db.empleados.find({
  $or: [
    { empresa: "Yahoo", salario: { $gt: 6000 } },
    { empresa: "Google", ventas: { $lt: 20000 } }
  ]
})

11. Visualizar el nombre, apellidos y el pais de cada empleado 

db.empleados.find(
  {}, 
  { nombre: 1, apellidos: 1, pais: 1 }
)

