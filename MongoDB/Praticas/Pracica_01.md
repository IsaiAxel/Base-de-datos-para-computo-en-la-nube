# Prcatica 1
## Operadores logicos
### Operador ANd
#### Ejercicios

### Operador OR

1. Mostrar los libros de la editorial biblio con precio mayor a 40 o libros

db.libros.find(
    {
        $or:[
            { editorial:'Biblio'.precio:{$gt:40}},
            { editorial:{$eq:'Palneta'},Precio:{$gt:30}}
        ]
    }
)

db.coleccion.find(filtro, columnas)

db.libros.find({},{titulo:1})

seleccionar los documentos , mostrando el titulo y la editorial 

...json
db.libros.find({},{titulo:1, editorial:1})
db.libros.find({},{titulo:1, editorial:1, _id:0})
...

2. seleccionar todos los documentos de la editorial planeta mostrando solamente el titulo y la editorial
...json
db.libros.find({editorial:'Planeta'},{_id:0, titulo:1, editorial:1})

3. 
db..libros.InsertOne(
    {
        _id:10,
        titulo: 'Mongo en entornos graficos',
        editorial: 'Terra',
        precio: 125
    }
)

db.libros.find(
    {
        cantidad:{ $exists: false }
    }
)

1. Mostrar todos los documentos que no contengan el campo cantidad 
json 
db.libros.find({ cantidad :{ $exists: false}})

## Operador Type (Permite preguntar si un detereminado campo corresponde con un tipo )

[Operador Type](https://www.mongodb.com/docs/manual/reference/operator/query/type/#mongodb-query-op.-type)

1. Mostrar todos los documentos donde el precio sea dobles

db.libros.find({precio:{$type:1}})

db.libros.find({precio:{$type:16}})

db.libros.InsertOne({
        _id:11,
        titulo: 'IA',
        editorial: 'Terra',
        precio: 125.4
        cantidad: 20
})

## Primero es el filtro y el segundo la proyectcion 
db.libros.find({precio:{$type:1}},{_id:0})

db.libros.insertMany([
 {
    _id: 12,
    titulo: 'IA',
    editorial: 'Terra',
    precio: 125,
  cantidad: 20
  },
  {
    _id: 13,
    titulo: 'Python para todos',
    editorial: 2001,
    precio: 200,
  cantidad: 30
  }]
  )

  1. seleccionar los documentos donde la editorial sea de tipo entero

  db.libros.find({editorial:{$type:16}})

  1. seleccionar los documentos donde la editorial sea de tipo string

  db.libros.find({editorial:{$type:string}})

  # Practica de consultas

  1. Instalar las tools de mongodb
  [DatabaseTools](https://www.mongodb.com/try/download/database-tools)

  2. Cargar el json empleados(Debemos estar ubicados en la carpeta donde se muestren el JSON  empleados)

  -El local :
  comando:
  mongoimport --db curso --collection empleados --file empleados.json

  mongoimport --db curso --collection empleados --file empleados.json --port 27018

  2. db.libros.updateMany(
    {},
    {$inc:(precio:5)}
  )

-Actualizar con un incremento de cinco a todos los documentos

-Actualizar con multiplicacion de 2 a todos los documentos que la cantidad sean mayores a 20

db.libros.updateMany({cantidad:{$gt:20},{$mul:{cantidad:2}}})



-Actualizar todos los documentos donde el precio sea mayor a 20 y se multiplique x2 la cantidad y el precio 

db.libros.updateMany(
  { precio: { $gt: 20 } }, 
  { $mul: { cantidad: 2, precio: 2 } }
)

3. remplazar documentos completos 

replaceOne