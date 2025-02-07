# Practica 1 : Base de datos  inserts

1. Conectarnos con mongosh a mongoDB
1. Crear una base de datos llamada curso
1. Comprobar que la base de datos no existe
1. Crear coleccion que se llame facturas y memorias

...json
sb.createCollection('Fcaturas')
show collection
...

5. insertar un documento con los siguietes datos

| Codigo   | Valor   |
|-------------|-------------|
| Cod_Factura | 10 |
| Ciente | Frutas Ramirez |
| Total | 223 |

| Codigo   | Valor   |
|-------------|-------------|
| Cod_Factura | 20 |
| Ciente | Frerreteria juan |
| Total | 140 |

...json
db.facturas.insertOne({cod_factura: 10,cliente: 'Frutas Ramirez',
total: 223 })

...

6. Crear una nueva coleccion pero usando directamente el insertOne.
insertar un documento en la coleccion productos con los siguientes datos:

| Codigo   | Valor   |
|-------------|-------------|
| Cod_Producto | 1 |
| Ciente | Tornillo x 1 |
| Total | 2 |

7. Crear un nuevo doc de producto que contenga un array que contenga los siguientes datos:

| Codigo   | Valor   |
|-------------|-------------|
| Cod_Producto | 2 |
| Nombre | Martillo |
| Precio | 20 |
| Unidades | 50 |
| Fabricantes | fab1,fab2,fab3,fab4 |

8. Borrar la coleccion Fcaturas y comprobar que se borro

...json
db.fcaturas.drop()
show collections
...

9. Insertar un documento en una coleccion denominada **Fabricantes**
para comprobar los subdocumentos y la clave id_personalizada

| Codigo   | Valor   |
|-------------|-------------|
| id | 1 |
| Nombre | fab1 |
| Localidad | ciudad:Buenos aires,pais:argentina,Calle:Calle pez 27,cod_postal:2900 |

10. Realizar una insercion de varios documentos en la coleccion productos 

| Codigo   | Valor   |
|-------------|-------------|
| Cod_Producto | 3 |
| Nombre | Alicates |
| Precio | 10 |
| Unidades | 25 |
| Fabricantes | fab1,fab2,fab5 |


| Codigo   | Valor   |
|-------------|-------------|
| Cod_Producto | 4 |
| Nombre | Arandela |
| Precio | 1 |
| Unidades | 500 |
| Fabricantes | fab2,fab3,fab4 |


