te dejo por aquí los pantallazos y los códigos correspondientes a los apartados del ejercicio de las películas que nos mandaste en clase :

Consultas / Buscar documentos

Realizar las siguientes consultas en la colección movies:
 1. Obtener todos los documentos

Código :   db.movies.find()
![Alt text](1.1.png)


2. Obtener documentos con writer igual a "Quentin Tarantino"

Código : db.movies.find({writer:"Quentin Tarantino"})
![Alt text](1.2.png)



3. Obtener documentos con actors que incluyan a "Brad Pitt"

Código : db.movies.find({ actors: { $in: ['Brad Pitt'] } })
![Alt text](1.3.png)



4. Obtener documentos con franchise igual a "The Hobbit"

Código  : db.movies.find({franchise:"The Hobbit"})
![Alt text](1.4.png)



5. Obtener todas las películas de los 90s

Código : db.movies.find({ year: { $gte: 1990, $lte: 1999 } })
![Alt text](1.5.png)




6. Obtener las películas estrenadas entre el año 2000 y 2010.

Código : db.movies.find({ year: { $gte: 2000, $lte: 2010 } })
![Alt text](1.6.png)





Actualizar Documentos
1. Agregar sinopsis a "The Hobbit: An Unexpected Journey" : "A reluctant hobbit, Bilbo Baggins, sets out to the Lonely Mountain with a spirited group of dwarves to reclaim their mountain home - and the gold within it - from the dragon Smaug."

Código : db.movies.updateOne({title:'The Hobbit: An Unexpected Journey'},{$set: {synopsis: "A reluctant hobbit, Bilbo Baggins, sets out to the Lonely Mountain with a spirited group of dwarves to reclaim their mountain home - and the gold within it - from the dragon Smaug." } })

![Alt text](2.1.png)




2. Agregar sinopsis a "The Hobbit: The Desolation of Smaug" : "The dwarves, along with Bilbo Baggins and Gandalf the Grey, continue their quest to reclaim Erebor, their homeland, from Smaug. Bilbo Baggins is in possession of a mysterious and magical ring."

Código : db.movies.updateOne({title:'The Hobbit: The Desolation of Smaug'},{$set: {synopsis: 'The dwarves, along with Bilbo Baggins and Gandalf the Grey, continue their quest to reclaim Erebor, their homeland, from Smaug. Bilbo Baggins is in possession of a mysterious and magical ring.'} })

![Alt text](2.2.png)



3. Agregar una actor llamado "Samuel L. Jackson" a la película "Pulp Fiction"

Código :  mongo_movies> db.movies.updateOne({title:'Pulp Fiction'},{$push: {actors: 'Samuel L. Jackson'}})

![Alt text](2.3.png)



Búsqueda por Texto / Text Search
1. Encontrar las películas que en el título contengan la palabra "Hobbit"

Código :  db.movies.createIndex({ title: 'text'}) - db.movies.find({ $text: { $search: 'Hobbit' } })

![Alt text](3.1.png)








2. Encontrar las películas que en la sinopsis contengan la palabra "Gandalf"

Me da error todo el rato con el indice de texto que he creado , he intentado renombrarlo y no me deja crear otro , así que he tenido que borrar el que había creado para el title y volver a crear otro .

Código : db.movies.dropIndex("title_text") - db.movies.createIndex({ synopsis : 'text' }) -db.movies.find({ $text: { $search: "Gandalf" } })

![Alt text](3.2.png)


3. Encontrar las películas que en la sinopsis contengan la palabra "Bilbo" y no la palabra "Gandalf"

Código :  db.movies.find({ $text: { $search: "Bilbo -Gandalf" } })

![Alt text](3.3.png)






4. Encontrar las películas que en la sinopsis contengan la palabra "dwarves" ó "hobbit"

Código : db.movies.find({$or:[{synopsis:{$regex:"dwarves"}},{synopsis:{$regex:"hobbit"}}]})

![Alt text](3.4.png)


5. Encontrar las películas que en la sinopsis contengan la palabra "gold" y "dragon"

Código :db.movies.find({$and:[{synopsis:{$regex:"gold"}},{synopsis:{$regex:"dragon"}}]})

![Alt text](3.5.png)







Eliminar Documentos
1. Eliminar la película "Pee Wee Herman's Big Adventure"

Código :  db.movies.deleteOne({ title: "Pee Wee Herman's Big Adventure" })

![Alt text](4.1.png)



2. Eliminar la película "Avatar"

Código : db.movies.deleteOne({ title: 'avatar' })

![Alt text](4.2.png)




Aquí es como ha quedado con las modificaciones y las películas borradas .

![Alt text](findFINAL.png)

![Alt text](findFINAL2.png)