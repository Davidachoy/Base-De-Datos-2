David Achoy Yakimova
2020053336
Bases De Datos II GR 1
# Prueba Corta # 2

### Explique el concepto de shard, replica y partition
**Replica** Maneja las copias de pods que se necesiten en el momento o copias de las base de Datos

**shard** Utilizada en base de datos NoSql, suelen ser pequeñas particiones basadas en un criterio para acceder a datos mas facil. 

**partition** Utilizada en Base de datos SQL, son procesos en los que se dividen tablas en pequeñas partes, asi querrys que acceden a cierta informacion acceden de manera mas rapida.

### Explique la diferencia entre Strong Consistency Eventual Consistency
En una base de datos con **Eventual Consistency** hay tiempos en los que un grupo de Base de Datos no van a tener los mismo datos a la hora que se haga read, en cambio **Strong Consistency** siempre que se haga un read, todos los datos en todas las base de datos van a estar iguales.

### ¿En que consiste warm replicas y hot replicas?
**Sacado de apuntes**

**warm replicas** fuerzan consistencia fuerte

**hot replicas** utilizan consistencia eventual

**Busque mas informacion en internet acerca del tema**

Decia que **Hot Standby** era un metodo mas parecido a **stong consistency** en el que un sistema corre al mismo tiempo que otro sistema principal. Entonces en el momento que hubiera alguna falla o error, el sistema ocuparia el lugar del otro sistema, pero en este caso tendria la misma informacion. Esto seria por que al funcionar como Strong Consistency los datos son pasados en tiempo real.

**Warm standby** seria mas a **Consistecia eventual** en el que un sistema periodicamente extraye datos del sistema principal, entonces hay tiempos en el que los sistemas no tienen los mismos datos.

### ¿En que consiste consiste switch over y fail over?

**Fail over** En caso de que se caiga o haya un problema el sistema, el sistema automaticamente se levanta

**Switch Over** Avisa el error del sistema para que una persona encargada arregle el problema
