# Apuntes semana 8 

---

Fecha: 13/09/22
Autor: David Achoy Yakimova

---

## Preguntas de la primera tarea

En Elasticsearch existen diferentes roles como :
- Master
- Data
- Ingest

**Nodeset** sirve para darle una configuracion de un conjunto de maquinas que funcionan en el cluster. Al cambiar el nodeset hay que levantar los recursos. 

El **Heap** sirve para configurar los recursos de la memoria. Siempre suelen tener el 50% de la memoria y el otro 50% se queda en el **Operating system**.

**Lucene**: Se encarga de realizar los indices.

Para configurar los recursos hay que hacerlo directamente en la configuracion del pod.

Resources:

&nbsp;&nbsp;&nbsp;&nbsp;Limit:

&nbsp;&nbsp;&nbsp;&nbsp;Request:

---

## Gatlings

**Gatlings** es una herramienta para hacer loadTesting. Para utilizar Gatlinks se puede utilizar **Flask**

El siguiente Link es el de la pagina oficial de Gatlings: [gatling.io](https://gatling.io/)

---

La facilidad de los JSON es que son autodescriptivos y que todos los programadores lo conocen.

**Protocol Buffer**: es un lenguaje Binario de google para el intercambio de datos

**Shard key**: son claves indexadas para partir las sharded collections 

Pagina oficial de [MongoDB](https://www.mongodb.com/)

### Como se compara SQL con NOSQL

- el SELECT desaparece de las base de datos NOSQL

- Una base de datos SQL asegura una transaccion de datos
- Con una base de datos NOSQL se renuncia a consistencia y aumenta el rendimiento.

### Caracteristicas de MONGODB

- Mongo tiene un set de indices limitados
- Mongo tiene Replicaset y esto funciona como un cluster donde van a existir muchos servidores de Mongo.
- Los shards de Mongo se dividen en Chunks y estos tienen limites de Shark keys
- Mongo crea un LoadBalancer, este hace que haya una distribucion equitativa de los chunks en los shards. Asegura que todos los shards respondan en paralelo.(Crea Overhead)
- Segun ciertas zonas geograficas exiten leyes sobre el manejo de datos privados de las personas. Mongo crea zonas geograficas y asigna servidores. A estos servidores se les asigan shards. Cada shard tiene su informacion por zona. Esto garantiza servers cerca de los clientes.
- Mongo Soporta hashed Sharding, Ranged Sharding y Zoned Sharding.

**hashed Sharding**: Se le aplica una formula y el #numero distribuye los datos.

**Ranged Sharding**: De X punto a Y punto se dividen los datos

**Zoned Sharding.**: se le distrubuyen a los usuarios que estan cerca y que cumpla con los requerimientos

el siguiente JSON sirve para conocer el nivel de consistencia que va a tener la base de datos
{W:value, J: value: W:Timeout:value}

**W** = (valor numerico) = Numero de servers a los que debe de llegar el update

**J** = (valor Booleano) = saber si utiliza el disco

**W:Timeout** = (valor numerico) = Cuanto tiempo tiene que pasar pasa saber si hay concistencia


