## Arrays y Documentos anidados 

- Para hacer esta práctica vamos a cargar unos datos ficticios de empresas.
- Tienes un fichero denominado “personas.json”
- Debes poner el resultado de las consultas en cada apartado

1. Buscar las personas que vivan en Colombia

db.personas.find({ "direccion.pais": "Colombia" })

- Resultados 
{
  "nombre": "Anni Niño",
  "direccion": {
    "ciudad": "Buenaventura",
    "pais": "Colombia"
  },
  "colores": ["yellow", "salmon", "yellow"],
  "ingresos": 7387
}

2. Personas a las que le guste el color rosa

db.personas.find({
  colores: { $in: ["pink"] }
})

- Resultados 
{
  _id: ObjectId('67d9c8de007c4fb5a39cdaa1'),
  nombre: 'Lorena Saiz',
  direccion: {
    calle: '1611 Oscar Walk',
    ciudad: 'The Pas',
    pais: 'Canada'
  },
  colores: [
    'orchid',
    'teal',
    'pink'
  ],
  ingresos: 10407
}
{
  _id: ObjectId('67d9c8de007c4fb5a39cda94'),
  nombre: 'Laura Oquendo',
  direccion: {
    calle: '2800 Samir Trail',
    ciudad: 'Bijelo Polje',
    pais: 'Montenegro'
  },
  colores: [
    'pink',
    'blue',
    'teal'
  ],
  ingresos: 8707
}

3. Personas cuyo tercer color preferido sea el amarillo (yellow)

db.personas.find({ "colores.2": "yellow" })

- Resultados 

{
  _id: ObjectId('67d9c8de007c4fb5a39cda95'),
  nombre: 'Laura Salcedo',
  direccion: {
    calle: '11046 Cayla Centers',
    ciudad: 'Rosso',
    pais: 'Mauritania'
  },
  colores: [
    'indigo',
    'green',
    'yellow',
    'salmon'
  ],
  ingresos: 7435
}

{
  _id: ObjectId('67d9c8de007c4fb5a39cda9c'),
  nombre: 'Anni Niño',
  direccion: {
    calle: '207 Taylor Cliffs',
    ciudad: 'Buenaventura',
    pais: 'Colombia'
  },
  colores: [
    'yellow',
    'salmon',
    'yellow'
  ],
  ingresos: 7387
}
{
  _id: ObjectId('67d9c8de007c4fb5a39cda9d'),
  nombre: 'Andrea Paredes',
  direccion: {
    calle: '09438 Vandervort Drives',
    ciudad: 'San Antonio',
    pais: 'Puerto Rico'
  },
  colores: [
    'green',
    'indigo',
    'yellow',
    'salmon',
    'grey',
    'violet'
  ],
  ingresos: 6340
}


4. Personas cuyo tercer color preferido sea el amarillo (yellow) y que vivan en Mauritania (debe salir uno)

db.personas.aggregate([
  {
    $match: {
      "colores.2": "yellow",
      "direccion.pais": "Mauritania"
    }
  }
])

- Resultado

{
  _id: ObjectId('67d9c8de007c4fb5a39cda95'),
  nombre: 'Laura Salcedo',
  direccion: {
    calle: '11046 Cayla Centers',
    ciudad: 'Rosso',
    pais: 'Mauritania'
  },
  colores: [
    'indigo',
    'green',
    'yellow',
    'salmon'
  ],
  ingresos: 7435
}

5.  Usando el operador $all averiguar las personas que les gusta el plata (silver) y el salmon (salmon)

db.personas.find({
  colores: { $all: ["silver", "salmon"] }
})

- Resultados

{
  _id: ObjectId('67d9c8de007c4fb5a39cda99'),
  nombre: 'Ángel Anguiano',
  direccion: {
    calle: '20780 McLaughlin Union',
    ciudad: 'Paramaribo',
    pais: 'Suriname'
  },
  colores: [
    'plum',
    'silver',
    'olive',
    'salmon',
    'silver'
  ],
  ingresos: 5712
}

6. Con el operador $elemMatch, averigua las personas que les guste el rosa (Pink) o el rojo (red)

db.personas.find({
  colores: { $elemMatch: { $in: ["pink", "red"] } }
})

- Resultados

{
  _id: ObjectId('67d9c8de007c4fb5a39cda94'),
  nombre: 'Laura Oquendo',
  direccion: {
    calle: '2800 Samir Trail',
    ciudad: 'Bijelo Polje',
    pais: 'Montenegro'
  },
  colores: [
    'pink',
    'blue',
    'teal'
  ],
  ingresos: 8707
}
{
  _id: ObjectId('67d9c8de007c4fb5a39cda98'),
  nombre: 'Sergi Cordero',
  direccion: {
    calle: '0605 Delfina Lodge',
    ciudad: 'Obiozara',
    pais: 'Nigeria'
  },
  colores: [
    'indigo',
    'sky blue',
    'red'
  ],
  ingresos: 7134
}
{
  _id: ObjectId('67d9c8de007c4fb5a39cdaa1'),
  nombre: 'Lorena Saiz',
  direccion: {
    calle: '1611 Oscar Walk',
    ciudad: 'The Pas',
    pais: 'Canada'
  },
  colores: [
    'orchid',
    'teal',
    'pink'
  ],
  ingresos: 10407
}
{
  _id: ObjectId('67d9c8de007c4fb5a39cdaa2'),
  nombre: 'Manuel Campos',
  direccion: {
    calle: '291 Waelchi Crest',
    ciudad: 'Holetown',
    pais: 'Barbados'
  },
  colores: [
    'maroon',
    'red',
    'cyan',
    'blue',
    'white',
    'gold'
  ],
  ingresos: 11230
}
{
  _id: ObjectId('67d9c8de007c4fb5a39cdaa3'),
  nombre: 'Salvador Meraz',
  direccion: {
    calle: '9327 Satterfield Alley',
    ciudad: 'Tuntange',
    pais: 'Luxembourg'
  },
  colores: [
    'red',
    'yellow',
    'orange',
    'violet'
  ],
  ingresos: 4058
}
{
  _id: ObjectId('67d9c8de007c4fb5a39cdaa6'),
  nombre: 'Ángel Zaragoza',
  direccion: {
    calle: "2758 O'Connell Ridge",
    ciudad: 'Barclayville',
    pais: 'Liberia'
  },
  colores: [
    'orange',
    'maroon',
    'white',
    'tan',
    'red',
    'maroon'
  ],
  ingresos: 9869
}
