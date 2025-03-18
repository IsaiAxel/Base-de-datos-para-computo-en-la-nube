## Agregaciones

## Metodos para realizar agregaciones simples 

- distinct(): Devuelve valores no duplicados 
- countDocuments(): Cuenta los documentos en una coleccion
-estimatedDocumentCount(): Cuenta de manera aproximada durante un periodo de tiempo.

## Una aggregation pipeline consta de una o mas etapas (stage) que procesa documentos 

1. Cada etapa realiza una operacion en los documentos de entrada.Por ejemplo, una frase puede filtrar documentos,agrupar documentos y calcular valores.

2. Los documentos que se generan en una fase pasan a la siguiente fase 

3. Puede devolver resultados para grupos de documentos como totales.

### Se utiliza la clausula "aggregate"

- Existen una serie de operadores que se pueden utilizar para realizar operaciones. Se tienen distintos tipos:
etapa, de comparacion, boleanos, aritmeticos, de cadenam etc.

## Metodos Simples: countDocuments() y distinct()

-- contar los documentos de la coleccion libros libros
db.libros.count

3. Mostrar todos loa libros mostrando solamente laeditorial 

4. Mostrar todas las distintas editoriales 



## $match. Una pipeline basica
## tienen funciones de etapa

db.libros.aggregate([
    $match:{editorial:"Terra"}
])

## $project. Incluir y renombrar campos

db.libros.aggregate([{
    $match:{editoria:'Terra'}
},
{
    $project:(
        id:0,
        titulo:1,
        precio:1,
        NombreEditorial:"$editorial",
        editorial:1
    )
}])

- Generado por mongo compas

## $group .Agrupaciones

--Cuantos documentos hay por cada una de las editoriales
[{
    $group:{
        _id: "$editorial",
        "Numero Documentos":{
            $count:{}
        }
    }
}]

--Cuantos documentos hay por cada una de las editoriales por numero de documentos de manera descendentes

{
    _id: "$propiety"
}

- Operador set


- Creando nuevas colecciones utilizando $out


- Ejemplos con modelos de comparacion y logicos 
[
  {
    $project:
      /**
       * specifications: The fields to
       *   include or exclude.
       */
      {
        _id: 0,
        price: 1,
        name: 1,
        caro: {
          $gt: ["$price", 300]
        },
        medio: {
          $and: [
            {
              $gte: ["$price", 100]
            },
            {
              $lte: ["$price", 300]
            }
          ]
        },
        barato: {
          $lt: ["precio", 100]
        }
      }
  }
]
- $cont - Devuelve valorwws segun una condicion (es parecido a un operador ternario de un lenguaje de programacion)

{
  _id: 0,
  price: 1,
  name: 1,
  room_type:1,
  caro: {
    $cond:[
      {
    $gt: ["$price", 300]
      }, 'Si','No'
 ] },
  medio: {
    $cond: [
      {
        "$and": [
          {
            "$gte": ["$price", 100]
          },
          {
            "$lte": ["$price", 300]
          }
        ]
      },
      "Si",
      "No"
    ]
  },
  barato: {
    $cond: [
      {
        "$lt": ["$price", 100]
      },
      "Si",
      "No"
    ]
  }
}

- Views
db.createView("ganancias_libros","libros"
    [
        {
            $match:{
                editorial:"Biblio"
            }

        }
    ]
)