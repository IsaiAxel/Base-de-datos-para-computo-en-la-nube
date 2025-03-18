## Modelo de datos en MongoDB

- Modelos 
   -Embebidos
   -Referenciados

- Modelos Embebidos

*Uno a Uno*
 json
db.departamentos.insertMany(
    [{
        _id:1,
        nombre:"Tecnologías de Información",
        responsable:{
            nombre:'Monico',
            apellidos:'Martinez Perez'
        },
        descripcion:'ejemplo de departamento'
    },
    {
        _id:2,
        nombre:"Contabilidad",
        responsable:{
            nombre:'Raul',
            apellidos:'Lopez Hernandez'
        },
        descripcion:'ejemplo de departamento'
    },

    ]
)


- Modelos Referenciados
*Uno a Uno*
 json
db.localidades.insertMany(
   [
    {
        _id:'BA',
        ciudad: 'Buenos Aires',
        pais: 'Argentina',
        poblacion: '16 millones',
        turismo: ["edificios", "tango", "gastronomia", "museos", "parques"],
        direccion: "Avenida Tortolos",
        cod_departamento:1
    },
    {
          _id:'SA',
        ciudad: 'Santiago',
        pais: 'Chile',
        poblacion: '20 millones',
        turismo: ["iglesias", "vino", "gastronomia", "museos"],
        direccion: "Calle soyla vaca del corral",
        cod_departamento:2
    }
   ]
)


db.departamentos.aggregate(
    [
        {
            $lookup:{
                from:"localidades",
                localField:"_id",
                foreignField:"cod_departamento",
                as :"localidades"
            }
        }
    ]
)

db.localidades.insertMany(
   [
    {
        _id:'1',
        nombre: '',
        
    },
    {
        _id:'',
        nombre: 'Santiago',
        precio: 'Chile',
        existencia: '20 millones',
        categoria: ""
    }
   ]
)