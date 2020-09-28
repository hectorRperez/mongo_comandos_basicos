# Comandos basicos de MongoDB

## *Comando para iniciar el servidor de Mongo*

~~~
$ mongod
~~~

Este comando inicia nuestro servidor en local

## *Iniciar el shell de mongo para interacturar con nuestro servidor de mongo*

~~~
$ mongo
~~~

Nuestro servidor debe estar iniciado


___

## *Palabras claves para saber información*

$ db -> Devuelve que base de datos estamos utilizando

$ show dbs -> Nos muestra todas las bases de datos

$ help -> Nos muestra la ayuda

$ bd.help() -> Devuelve la ayuda de metodos en Mongo

___

## *Comando para crear una base de datos*

~~~
$ use *nombre de la base de datos*

$ use webstore
~~~

___

## *Eliminar la base de datos actual*

~~~
$ db.dropDatabase()
~~~

**Nota** Es importante saber que la base de datos que se va a eliminar es la que se esta utilizando al momento de ejecutar el comando

___

## *Mostrar las colecciones de una base de datos en Mongo*

~~~
$ show collections
~~~

___

## *Crear una colección*

~~~
$ db.createCollection(nombre_coleccion)

$ db.createCollection("user")
~~~

Puede ser que no tengamos ninguna collections creada, pero ingresando datos ya automaticamente creamos una collection

~~~
$ db.product.insert(
    {
        "nombre"        : "laptop",
        "precio"        : 40.2,
        "active"        : false,
        "create_at"     : new Date("12/12/1999"),
        "somedata"      : [1,"a",[]],
        "factucturer"   : {
            "name"     : "dell",
            "version"  : "xps",
            "location" : {
                "city"    : "usa",
                "address" : "asdsdsd",
            }
        }  
    }
)
~~~

___

## *Eliminar una collection*

~~~
$ db.nombre_collection.drop()

$ db.product.drop()
~~~

___


## *Ver todas los documentos de una collections*

~~~
$ db.product.find() 
~~~

Devuelve todos los documentos almacenados en una collections de forma desordenado

~~~
$ db.product.find().pretty() 
~~~

Devuelve todos los datos de forma ordenada

___

# OPERACIONES BASICAS 

## *Crear una base de datos*

~~~
$ use mystore
~~~

## *Crear una collection*

~~~
db.createCollection("product")
~~~

## *Insertar un documento en una collection*

~~~
db.product.insert({"name":"keyboard"})
~~~

## *Ver todos los documentos almacenados*

~~~
show.product.find().pretty()
~~~

## *Almacenar multiples datos*
___
~~~
db.product.insert([
    {
        "name"         : "mouse",
        "description"  : "razer mouse",
        "tags"         : ["computers", "gaming"],
        "quantity"     : 14,
        "create_at"    : new Date(),
    },
    {
        "name"         : "monitor",
        "description"  : "lg monitor",
        "tags"         : ["computers", "gaming"],
        "quantity"     : 3,
        "create_at"    : new Date()
    }
])
~~~

___
## *Buscar un documento por nombre especifico*

~~~
$ db.product.find({name:"mouse"})
~~~

___

## *Buscar un documento por nombre especifico pero solo se espera el primer resultado*

~~~
$ db.product.findOne({name:"mouse"})
~~~

___

## *Buscar un documento por nombre especifico pero que se omita los valores del propio documento*

~~~

$ db.product.findOne({"tags":"computers"},{"name":1,"description":1})

~~~

**Nota**
Al colocar {"name":1,"description":1} se le indica a Mongo que solo muestre esas propiedades

___

## *Buscar un documento por nombre especifico pero que los ordenes alfabeticamente*

~~~
db.product.find({"tags":"computers"}).sort({name:1})
~~~

**Nota**
Al colocar {name:1} se le indica a Mongo que devuelva en orden alfabetica con name


___

## *Buscar un documento por nombre especifico pero estableciendo un limite en la busqueda*


~~~
db.product.find().limit(2)
~~~

**Nota**
Se le indica a Mongo que devuelva solo 2 resultados

___

## *Contar cuantos datos tenemos*

~~~
db.product.count()
~~~

___

## *Utilizar funciones para manipular los documentos*

~~~
db.product.find().forEach(product => print("Product Name: " + product.name))
~~~

___
## *Actualizar documentos*

~~~
db.product.update({"name":"keyboard"},{"price":100})
~~~

**Nota**

La función *update* tiene dos objetos, el primero de busqueda y el segundo de remplazo. *Es importante saber* que el segundo remplazo remplaza el primer valor

___
## *Actualizar documentos utilizando el metodo $set. Se agrega una nueva propiedad*

~~~
db.product.update({"name":"lapto"}, {$set: {"calidad": "mala"}})
~~~

**Nota**
Se busca el documento con el valor de name "laptop" y se agrega el segundo objeto luego de la función $set

___
## *Actualizar documentos así no exista el documento*

~~~
db.product.update({"name":"desktop"}, {$set: {"description" :"Gaming Desktop"}}, {upsert:true})
~~~

**Nota**

Si no se consigué coincidencia igual se actualiza o se agrega el nuevo documento

___

## *Renombrar un valor de un documento*

~~~
db.product.update({"name":"laptop"}, {$rename: {"name":"nombre"}})
~~~

**Nota**

Se busca el documento con el primer valor, y luego se renombra el segundo parametro

___
## *Eliminar datos*

~~~
db.product.remove({"nombre":"keyboard"})
~~~

**Nota**

Eliminar los objeto que encuentre con los parametros que se estan pasando 


___
## *Eliminar todos los documentos de la collections*

~~~
db.product.remove({})
~~~

