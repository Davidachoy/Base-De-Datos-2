
# Apuntes semana 9 

---

Fecha: 22/09/22
Autor: David Achoy Yakimova

---
### Tips para la tarea 

Un deployment siempre garantiza que hayan pods. 

Los nombres que se utilizan en los helmcharts deberian ser basados en los recursos que se van a utilizar.

Algunos charts generan bugs donde en storage se guardan volumenes a la hora de desinstalarlos.

--- 

### Performance

**Atomicity** : Garantiza que un conjunto de sentencias son ejecutadas de forma atomica

**Consistency** : Garantiza que el cambio se haga sin importar la circunstancia para tener consistencia, PAra tener consistencia se necesita atomisidad. y en caso de errorres se hace un rollback y vuelve al estado anterior.

Aqui sale un termino que seria el **Lock** en el cual existe el read y write.

El lock de read es compatible con otro read, ya que se puede leer sin sufrir consistencia, pero no se puede hacer un Read y Write, ya que se pueden cambiar los datos en la lectura.

El lock de write no se le puede leer ni escribir, ya que no cumpliria con consistencia

**Rollback en cascada**: Devuelve todas las transacciones

**Isolation** : Implica que una transaccion corra sola.

**Durability** : Garantiza que una transaccion va a durar para siempre.

**Multiversioning**: Dos versiones de datos, la consistencia y la version calculada por la transaccion

**DeathLock**: Cuando dos entidades usan el mismo sistema compartido al mismo tiempo.

Existe dos tipos del phase lockin, es un algoritmo para los locks.
- Expanding: Pedir locks sin liberar
- Shrinking: Libera locks sin pedir mas

**Conservado**: Obtener todos los lock antes de que inicie la operacion (El rendimiento cae)

**Strict two phase**: Los locks de tipo escritura se liberan hasta que termine la transaccion. (Se evita el rollback de cascada)

**Strong strict two phase**: Se liberan los locks de escritura y lectura hasta que la transaccion termine (Atrasa todas las transaccion y tiempos de respuesta bajos)

**Two phase commit protocol**: 
- Commit Request: Todos tienen que tener exito o sino no funciona.
- Commit phase: En caso de failover hace rollback.


Commit request tiene dos logs redo y undo

**Redo**: Operaciones que se tienen que ejecutar para tener consistencia

**Undo**: Operacion para tener el rollback