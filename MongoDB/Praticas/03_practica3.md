## Pracica 3.U Updates y Deletes

1. Cambiar el salario del empleado Imogene Nolan. Se le asigna 8mil

db.empleados.updateOne(
   { nombre: "Imogene" , apellidos:"Nolan" },
   { $set: { salario: 8000 } }
)


2. Cambiar "Belgium" por "Bélgica" en los empleados (debe haber dos)

db.empleados.updateMany(
   { pais: "Belgium" },
   { $set: { pais: "Bélgica" } }
)

3. Incrementar el salario de todos los empleados de Google en 1000

db.empleados.updateMany(
   { empresa: "Google" },
   { $inc: { salario: 1000 } }
)


4. Reemplazar el empleado "Omar Gentry" por el siguiente documento

db.empleados.replaceOne(
   { nombre: "Omar Gentry" },
   {
       nombre: "Omar",
       apellidos: "Gentry",
       correo: "sin correo",
       direccion: "Sin calle",
       region: "Sin region",
       pais: "Sin pais",
       empresa: "Sin empresa",
       ventas: 0,
       salario: 0,
       departamentos: "Este empleado ha sido anulado"
   }
)

   {
"nombre": "Omar",
"apellidos": "Gentry",
"correo": "sin correo",
"direccion": "Sin calle",
"region": "Sin region",
"pais": "Sin pais",
"empresa": "Sin empresa",
"ventas": 0,
"salario": 0,
"departamentos": "Este empleado ha sido anulado"
}
5. comprobar que el empleado asido modificado 

db.empleados.find({ nombre: "Omar" }).pretty()

6. Borrar todos los empleados que ganen mas de 8500.
Nota:deben ser borrados 3 documentos

db.empleados.deleteMany(
   { salario: { $gt: 8500 } }
)

7. Visualizar con una expresion regular todos los empleados con apellidos que comiencen con R 

db.empleados.find(
   { apellidos: { $regex: /^R/, $options: "i" } }
).pretty()

8. Buscar todas las funciones regiones que contengan un "V".
Hacerlo con el operador $regex y que no distinga mayuscula y minuscula . Deben salir 2
db.empleados.find(
   { region: { $regex: "v", $options: "i" } }
).pretty()

9. Visualizar los apellidps de los empleados ordenados por el propio apellido

db.empleados.find(
   {},
   { apellidos: 1, _id: 0 }
).sort({ apellidos: 1 }).pretty()

10. indicar el numero de empleados que trabajan en google

db.empleados.countDocuments(
   { empresa: "Google" }
)

11. Borrar la coleccion empleados y la base de datos

db.empleados.drop()
