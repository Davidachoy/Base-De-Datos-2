David Achoy Yakimova

2020053336

Bases De Datos II GR 1

### Prueba Corta # 9

## Suponiendo que un sistema de bases de datos relacional que presenta un read-heavy workload y los queries son muy diferentes, explique detalladamente ¿porque el uso de caches puede afectar el rendimiento del sistema de forma negativa? (30 pts)

El cache es una muy buena herramienta para las Bases de datos ya que permite obtener la informacion solicitada de manera casi que inmediata, pero si el sistema realiza muchos querrys esta se puede llenar y al llenarse ocurre lo que se llama un cache miss o que el sistema en vez de agarrar los datos de la cache, va y los busca al disco duro haciendo los querrys mas lentos. Tambien podria afectar la consistencia de dichos querrys.

## El particionamiento de tablas en bases de datos relacionales es un concepto muy parecido al de shards en bases de datos NoSQL, explique detalladamente ¿Cómo afecta el particionamiento y el sharding en el rendimiento de bases de datos SQL y NoSQL? (30 pts)

En este caso genera querrys mas rapidos ya que la informacion se divide en partes y se distribuye en diferentes workers nodes y alfinal se unen en el nodo escogido como coordinador. Al no hacerse, pueden quedar nodos sin usar.

## En un sistema de bases de datos con Strong Consistency cuyo workload es de read-heavy y write-heavy, ¿Cómo afectan los exclusive locks el rendimiento de las bases de datos NoSQL? (20 pts)

En este caso los exclusive locks bajarian el rendimiendo de la base de datos por que al ser muchas lecturas y escrituras, el sistema se bloquea para asegurar que las trasnsacciones se cumplan. 

## Explique detalladamente, ¿Cómo afecta la selección de discos físicos el rendimiento de una base de datos SQL y NoSQL? (20 pts)

Los discos fisicos en comparacion a los de red son mas rapidos, ya que los de red estan limitados por las tarjetas de red y el internet. Pero al usar discos fisicos estos tiene limitantes como el espacio y la disponibilidad en diferentes partes el mundo. Discos en red como en AWS permite tener Bases de datos en diferentes regiones.