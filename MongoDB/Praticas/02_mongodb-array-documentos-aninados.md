# Busquedas en arrays y documentos anidados

## Buscar dentro de un documento anidado

1. Seleccionar las ciudades donde los alcades tengan mas de 70 años 


2. Realizar la consulta anterior pero utilizando una proyeccion 

db.ciudades.find({"alcalde.edad"})

3. Seleccionar la ciudad donde el alcalde tenga 76 años o 41
db["Ciudades"].find({$or:[{"alcalde.edad":76},{"alcalde.edad":41}]})


# Consultas con arrays

1. Crear collection cazas
2. Cargar los documentos de la coleccion cazas , de la data de cazas

## Ejemplos con consulta con arrays

1. Buscar los documentos que tengan usa como paises

db.cazas.find({paises:"usa"})

2. Buscar los documentos donde cualquier elemento del array dimensiones sea mayor a 5
db.cazas.find({dimensiones:{$gt:5}}).count()

3. Buscar lo s documentos donde las dimensiones del avion por ancho que es la posicion 1, sea superior  14

db.cazas.find({"dimensiones.1":{$gt:14}
},{_id:0, modelo:1 dimensiones:1})

### Arrays Operador $alcalde

1. Buscar 

db.cazas.find({paises:{$all:['egipto','israel']}})

2. Selccionar las cazas que sirven en inglaterra y españa

db.cazas.find({
    $and:[{paises:'inglaterra'},
    {paises:'españa'
    }]
})

### Arrays operador $elementMatch -> Permite hacer busquedas dentro de arrays, este busca la lista de condiciones que esta dentro del operador

1. Buscar que aviones tienen uso dentro de inglaterra

db.cazas.find({paises:{$elementMatch:{$eq:'inglaterra'}}})

2. Buscar los aviones donde las dimensiones sea mayor a 20 o mayor a 15

db.cazas.find({dimensiones:{$elemntMatch:{$lt:20, $gt:15}}})

### Buscar en arrays documentos anidados

1. Utilizar la coleccion ciudades
2. Buscar los consjeros de nombre Jeri Flowers de edad 76
db.ciudades.find({consejeros:{indentificador:1, nombre: "Jeri Flowers",edad:78}})
3. Buscar en consejeros la edad donde tengan una edad mayor a 70

db.ciudades.find({"consejeros.edad":{$gt:70}})

4. Buscar en consejeros en la posicion 2 que esten entre 70 y 80 años

db["Ciudades"].find({'consejeros.2.edad':{$gt:70,$lt:80}},{_id:0,"consejeros.nombre":1, "consejeros.edad":1})

5. Buscar los consejeros de la posicion 0 que sean mayores a 70 años 
 db["Ciudades"].find({"consejeros.0.edad":{$gt:70}},{_id:0,nombre:1,"alcalde.edad":1,"alcalde.nombre":1})

6. buscar consejeros mayores a 70

7.