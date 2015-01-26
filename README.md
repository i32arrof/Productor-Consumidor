Prácticas de Sistemas Operativos
=================================

# PROBLEMA DEL PRODUCTOR CONSUMIDOR CON SEMAFOROS BINARIOS Y VARIABLES DE CONDICIÓN

Usando variables de condición junto con mutexs para evitar espera activa. Cuando el consumidor toma un producto notifica al productor que puede comenzar a trabajar nuevamente porque al menos hay un hueco donde poner una producción. En caso contrario si el buffer se vacía, el consumidor se pone a dormir y en el momento en que el productor agrega un producto crea una señal para despertarlo. Consulte la documentación de clases de teoría si lo considera oportuno.

# PROBLEMA FILOSOFOS COMENSALES

Cinco filósofos viven en una casa, donde hay una mesa preparada para ellos. Básicamente, la vida de cada filósofo consiste en pensar y comer, y después de años de haber estado pensando, todos los filósofos están de acuerdo en que la única comida que contribuye a su fuerza mental son los espaguetis.
Cinco filósofos viven en una casa, donde hay una mesa preparada para ellos. Básicamente, la vida de cada filósofo consiste en pensar y comer, y después de años de haber estado pensando, todos los filósofos están de acuerdo en que la única comida que contribuye a su fuerza mental son los espaguetis. Se presentan las siguientes suposiciones y/o restricciones:
• Debido a su falta de habilidad manual, cada filósofo necesita dos tenedores para comer los espaguetis, cogiendo solo un tenedor a la vez (en cualquier orden, izquierda-derecha o derecha-izquierda).
• La disposición para la comida es simple (ver figura): una mesa redonda en la que está colocado un gran cuenco para servir espaguetis, cinco platos, uno para cada filósofo, y cinco tenedores.
13
￼• Un filósofo que quiere comer utiliza,en caso de que estén libres, los dos tenedores situados a cada lado del plato, retira y come algunos espaguetis.
• Si cualquier filósofo toma un tenedor (solo un tenedor a la vez) y el otro está ocupado, se quedará esperando, con el tenedor en la mano, hasta que pueda tomar el otro tenedor, para luego empezar a comer.
• Si un filósofo piensa, no molesta a sus colegas. Cuando un filósofo ha terminado de comer suelta los tenedores y continua pensando.
• Si dos filósofos adyacentes intentan tomar el mismo tenedor a una vez, se produce una condición de carrera: ambos compiten por tomar el mismo tenedor, y uno de ellos se queda sin comer.
• Si todos los filósofos toman el tenedor que está a su derecha al mismo tiempo (o a su izquierda), entonces todos se quedarán esperando eternamente, porque alguien debe liberar el tenedor que les falta. Nadie lo hará porque todos se encuentran en la misma situación (esperando que alguno deje sus tenedores). Se produce un interbloqueo (deadlock o abrazo de la muerte). Entonces los filósofos se morirán de hambre.
El problema: diseñar un ritual (algoritmo) que permita a los filósofos comer. El algoritmo debe satisfacer la exclusión mutua (no puede haber dos filósofos que puedan utilizar el mismo tenedor a la vez) y evitar el interbloqueo e inanición (en este caso, el término inanición tiene un sentido literal, además de algorítmico). A partir del siguiente esquema de pseudocódigo y del que está disponible en Moodle, además de consultar la Web7 para informarse en profundidad del problema, implemente una solución en C utilizando semáforos que resuelva el problema de sincronización e inanición de la cena de los filósofos.

# PROBLEMA DE LECTORES Y ESCRITORES CON PRIORIDAD PARA LECTORES

Hay un objeto de datos (fichero de texto, base de datos, un bloque principal de memoria) que es utilizado por varios procesos o usuarios, unos que leen y otros que escriben. Solo puede utilizar el recurso un proceso y solo uno, es decir, o bien un proceso estará escribiendo o bien leyendo, pero nunca ocurrirá simultáneamente.
Se considera a cada usuario (lector y escritor) como un proceso distinto, y, por ejemplo, al fichero en cuestión como un recurso. Para que el problema esté bien resuelto se tiene que cumplir:
1) Cualquier número de lectores pueden leer del fichero simultáneamente.
2) Solo un escritor al tiempo puede escribir en el fichero.
3) Si un escritor está escribiendo en el fichero ningún lector puede leerlo.
Para distinguirlo del problema del productor-consumidor, supóngase que el área compartida es un catálogo de biblioteca. Los usuarios ordinarios de la biblioteca leen el catálogo para localizar un libro, pero no eliminan ese catálogo en su lectura. Uno o más bibliotecarios deben poder actualizar el catálogo. En la solución general, cada acceso al catálogo sería tratado como una sección crítica y los usuarios se verían forzados a leer el catálogo de uno en uno. Esto claramente impondría retardos intolerables. Al mismo tiempo, es importante impedir a los escritores (bibliotecarios) interferir entre sí y también es necesario impedir la lectura mientras la escritura está en curso para impedir que se acceda a información inconsistente.
Este problema se puede plantear dando prioridad a los lectores sobre escritores o viceversa. Resumidamente, cuando se da prioridad a los lectores, una vez que un lector haya empezado a leer, los demás no tienen que esperar a que éste termine ni tampoco esperar a que escriba un escritor que se ponga en espera de acceder a la sección crítica (esta solución podría dejar a los escritores en inanición, ya que estos deben esperar mientras haya al menos un lector en la sección crítica). Por el contrario, cuando se da prioridad a los escritores, si hay algún lector leyendo u otros lectores quieren hacer lo mismo, y hay un escritor esperando, se le da prioridad al escritor sobre los lectores en el acceso a la sección crítica. Es decir, los escritores deben comenzar a hacer su trabajo tan pronto como sea posible (esta solución puede dejar a los lectores en inanición). Si un escritor está esperando a escribir nadie más debe leer. Si necesita más información consulte la Web.
Una vez haya estudiado detenidamente el problema de los lectores-escritores implemente el problema mediante el uso de hilos dando prioridad a los lectores. Use como sección crítica la estructura de datos que considere oportuna. A continuación tiene un ejemplo en pseudocódigo. Consulte la información de las clases teóricas si lo considera oportuno.
