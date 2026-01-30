<!--
Posible prompt:
<prompt>
Tengo un cuestionario con preguntas sobre "Clases y Objetos". Debes tener en cuenta que los conocimientos previos que tengo (y por tanto tus respuestas deben ser adaptadas), son:
- C/C++ sin orientaciÃ³n a objetos.
- Temas de Java previos: ninguno.

Cada respuesta debe tener entre 2 - 4 pÃ¡rrafos de longitud (sin contar los trozos de cÃ³digo).

Por favor, escribe en impersonal las respuestas.

</prompt>
----
-->

# TEMA 1. Clases y objetos

## 1. Â¿CuÃ¡les son las cuatro caracterÃ­sticas bÃ¡sicas de la programaciÃ³n orientada a objetos? Describe brevemente cada una

### Respuesta
Las cuatro características básicas de la programación orientada a objetos son abstracción, encapsulación, herencia y polimorfismo. Todas ellas ayudan a organizar el código de forma más clara y modular que en la programación estructurada tradicional (como C).

La abstracción consiste en representar solo las características esenciales de un objeto, ignorando los detalles internos. La encapsulación agrupa datos y operaciones en una clase y controla el acceso a ellos, evitando modificaciones indebidas desde fuera.

La herencia permite crear nuevas clases a partir de otras, reutilizando y ampliando su comportamiento. El polimorfismo permite que una misma operación se comporte de forma distinta según el objeto que la ejecute, aumentando la flexibilidad del programa.

## 2. Cita cuatro lenguajes populares que permitan la programaciÃ³n orientada a objetos

### Respuesta
Algunos lenguajes de programación populares que permiten la programación orientada a objetos son Java, C++, Python y C#. Todos ellos soportan los conceptos básicos de la POO, como clases, objetos, herencia y polimorfismo.

## 3. Los paradigmas anteriores a la POO, Â¿QuÃ© es la **programaciÃ³n estructurada**? y, todavÃ­a mejor, Â¿QuÃ© es la **programaciÃ³n modular**?

### Respuesta
La programación estructurada es un paradigma que organiza el código usando estructuras de control claras como secuencia, selección (if) e iteración (for, while), evitando saltos incontrolados como goto. Su objetivo principal es hacer los programas más legibles y fáciles de mantener. Lenguajes como C usan este enfoque, donde el programa se compone de funciones que se ejecutan de forma ordenada.

La programación modular es una evolución de la estructurada que divide el programa en módulos independientes, cada uno con una responsabilidad concreta. En C, esto se refleja en el uso de archivos .c y .h, donde se separa la implementación de la interfaz. Cada módulo puede desarrollarse, probarse y mantenerse de forma aislada.

La principal diferencia es que la programación estructurada se centra en el control del flujo del programa, mientras que la modular se centra en la organización del código en partes reutilizables. Ambas buscan reducir la complejidad, pero ninguna integra datos y comportamiento de forma conjunta como lo hace la programación orientada a objetos.

## 4. Â¿QuÃ© tres elementos definen a un objeto en programaciÃ³n orientada a objetos?

### Respuesta
Un objeto en programación orientada a objetos se define por tres elementos fundamentales: identidad, estado y comportamiento. Estos conceptos permiten modelar entidades del mundo real dentro de un programa de forma clara y organizada.

La identidad es lo que diferencia a un objeto de otro, incluso aunque tengan los mismos datos. Por ejemplo, dos variables distintas que representen el mismo tipo de estructura en C siguen siendo entidades diferentes en memoria. En POO, cada objeto es único aunque tenga los mismos valores que otro.

El estado corresponde a los datos que almacena el objeto en un momento determinado, es decir, el valor de sus atributos. El comportamiento son las acciones que el objeto puede realizar, definidas mediante métodos, que operan sobre su propio estado, algo que en C suele hacerse pasando estructuras a funciones.

## 5. Â¿QuÃ© es una clase? Â¿Es lo mismo que un objeto? Â¿QuÃ© es una instancia? Â¿Todos los lenguajes orientados a objetos manejan el concepto de clase?

### Respuesta
Una clase es una plantilla o modelo que define cómo serán los objetos: qué datos tendrán (atributos) y qué operaciones podrán realizar (métodos). No es un objeto en sí, sino una descripción, parecida a un struct en C, pero acompañada de las funciones que trabajan sobre esos datos.

Un objeto es una entidad concreta creada a partir de una clase, y una instancia es precisamente ese proceso o resultado: un objeto que ocupa memoria y tiene valores propios. Dicho de forma simple, objeto e instancia suelen usarse como sinónimos, mientras que la clase es solo la definición.

No todos los lenguajes orientados a objetos manejan el concepto de clase de la misma forma. La mayoría, como Java o C++, sí usan clases, pero existen lenguajes orientados a objetos que se basan en prototipos en lugar de clases, como JavaScript, donde los objetos pueden crearse directamente sin una clase tradicional.

## 6. Â¿DÃ³nde se almacenan en memoria los objetos? Â¿Es igual en todos los lenguajes? Â¿QuÃ© es la **recolecciÃ³n de basura**? 

### Respuesta
En programación orientada a objetos, los objetos suelen almacenarse en memoria dinámica (heap). A diferencia de variables locales simples, los objetos tienen un tiempo de vida más largo y no dependen directamente del bloque de código donde se crean. Si vienes de C, puedes pensar en ellos como estructuras creadas con malloc, aunque el proceso esté automatizado.

No es igual en todos los lenguajes. En C++, los objetos pueden almacenarse tanto en la pila (stack) como en el heap, y el programador es responsable de liberar la memoria cuando se usa el heap. En Java, en cambio, los objetos siempre se crean en el heap, y el programador no libera la memoria manualmente.

La recolección de basura (garbage collection) es un mecanismo automático que se encarga de liberar la memoria ocupada por objetos que ya no se usan. El sistema detecta qué objetos no tienen referencias activas y recupera su memoria sin intervención del programador. Esto reduce errores comunes en C/C++, como fugas de memoria o accesos a memoria liberada, a costa de perder algo de control directo sobre la gestión de memoria.

## 7. Â¿QuÃ© es un mÃ©todo? Â¿QuÃ© es la **sobrecarga de mÃ©todos**? 

### Respuesta
Un método es una función asociada a una clase u objeto, que define una acción que ese objeto puede realizar. A diferencia de las funciones en C, un método opera directamente sobre los datos del propio objeto, sin necesidad de pasar explícitamente la estructura como parámetro, ya que forma parte de la clase.

La sobrecarga de métodos consiste en definir varios métodos con el mismo nombre dentro de una clase, pero con diferentes parámetros (número o tipo). El lenguaje decide automáticamente cuál ejecutar según los argumentos usados en la llamada, algo que en C suele resolverse usando nombres de funciones distintos.

Esto permite que una misma operación tenga comportamientos adaptados a distintos casos, mejorando la legibilidad del código. En Java, la sobrecarga se resuelve en tiempo de compilación y no depende del tipo de objeto, sino de la firma del método.

## 8. Ejemplo mÃ­nimo de clase en Java, que se llame Punto, con dos atributos, x e y, con un mÃ©todo que se llame `calculaDistanciaAOrigen`, que calcule la distancia a la posiciÃ³n 0,0. Por sencillez, los atributos deben tener visibilidad por defecto. Crea ademÃ¡s un ejemplo de uso con una instancia y uso del mÃ©todo

### Respuesta
A continuación tienes un ejemplo mínimo de una clase en Java llamada Punto, con dos atributos x e y y un método calculaDistanciaAOrigen. Los atributos tienen visibilidad por defecto (package-private), tal y como pides, y el método calcula la distancia al punto (0,0) usando la fórmula matemática habitual.
class Punto {
    double x;
    double y;

    double calculaDistanciaAOrigen() {
        return Math.sqrt(x * x + y * y);
    }
}
Esta clase define solo la estructura y el comportamiento del objeto, pero no crea ningún objeto todavía. Es equivalente a definir un struct y funciones asociadas en C, pero aquí todo queda agrupado en una única unidad. El método accede directamente a x e y, sin necesidad de pasarlos como parámetros.

A continuación se muestra un ejemplo de uso, donde se crea una instancia de Punto, se asignan valores a sus atributos y se llama al método:
public class Main {
    public static void main(String[] args) {
        Punto p = new Punto();
        p.x = 3;
        p.y = 4;

        double distancia = p.calculaDistanciaAOrigen();
        System.out.println(distancia);
    }
}
Aquí, p es una instancia de la clase Punto. El objeto se crea en memoria dinámica y el método se invoca usando el operador punto, lo que deja claro que la acción se realiza sobre ese objeto concreto. Este estilo evita pasar estructuras a funciones y es una de las bases de la programación orientada a objetos.

## 9. Â¿CuÃ¡l es el punto de entrada en un programa en Java? Â¿QuÃ© es `static` y para quÃ© vale? Â¿SÃ³lo se emplea para ese mÃ©todo `main`? Â¿Para quÃ© se combina con `final`?

### Respuesta
En Java, el punto de entrada de un programa es siempre el método main, que es donde empieza la ejecución. Su firma es public static void main(String[] args).

La palabra static indica que un método o atributo pertenece a la clase y no a un objeto, por lo que se puede usar sin crear instancias. No solo se usa en main; también sirve para constantes, contadores o métodos de utilidad.

Cuando se combina con final, como en static final, se crea una constante de clase, es decir, un valor fijo que no se puede cambiar y se puede acceder sin instanciar la clase.

## 10. Intenta ejecutar un poco de Java de forma bÃ¡sica, con los comandos `javac` y `java`. Â¿CÃ³mo podemos compilar el programa y ejecutarlo desde linea de comandos? Â¿Java es compilado? Â¿QuÃ© es la **mÃ¡quina virtual**? Â¿QuÃ© es el *byte-code* y los ficheros `.class`?

### Respuesta
Para ejecutar un programa en Java desde la línea de comandos, primero se compila el archivo .java con javac y luego se ejecuta con java. Por ejemplo, si tienes un archivo llamado Main.java:

javac Main.java   # Compila el archivo y genera Main.class
java Main         # Ejecuta el programa usando la máquina virtual de Java

Java es un lenguaje compilado e interpretado a la vez. El compilador javac traduce el código fuente .java a un byte-code intermedio que no depende del sistema operativo, y este byte-code se ejecuta mediante la máquina virtual de Java (JVM). Esto permite que un mismo programa funcione en diferentes sistemas sin recompilarlo.

El byte-code es un conjunto de instrucciones intermedias que la JVM puede interpretar. Cada archivo .class generado por javac contiene el byte-code de una clase. La JVM lee estos .class y los traduce a instrucciones que el sistema operativo puede ejecutar, gestionando también memoria y objetos automáticamente. Esto es lo que hace que Java sea portátil y seguro frente a errores de memoria típicos de C/C++.


## 11. En el cÃ³digo anterior de la clase `Punto` Â¿QuÃ© es `new`? Â¿QuÃ© es un **constructor**? Pon un ejemplo de constructor en una clase `Empleado` que tenga DNI, nombre y apellidos

### Respuesta
En Java, la palabra clave new se usa para crear una instancia (objeto) de una clase. Cuando escribes Punto p = new Punto();, estás reservando memoria para el objeto y llamando al constructor de la clase para inicializarlo. Es similar a usar malloc en C, pero con inicialización automática y seguridad de tipos.

Un constructor es un método especial de una clase que se ejecuta automáticamente al crear un objeto con new. Su función principal es inicializar los atributos del objeto. Se diferencia de otros métodos en que no tiene tipo de retorno y su nombre debe coincidir exactamente con el de la clase.

class Empleado {
    String dni;
    String nombre;
    String apellidos;

    // Constructor
    Empleado(String dni, String nombre, String apellidos) {
        this.dni = dni;
        this.nombre = nombre;
        this.apellidos = apellidos;
    }
}
// Ejemplo de uso:
public class Main {
    public static void main(String[] args) {
        Empleado e = new Empleado("12345678A", "Ana", "Pérez");
        System.out.println(e.nombre + " " + e.apellidos);
    }
}
En este ejemplo, al usar new Empleado(...) se crea un objeto Empleado y se inicializan sus atributos mediante el constructor. La palabra this se usa para diferenciar los atributos del objeto de los parámetros del constructor.

## 12. Â¿QuÃ© es la referencia `this`? Â¿Se llama igual en todos los lenguajes? Pon un ejemplo del uso de `this` en la clase `Punto`

### Respuesta
La referencia this es una variable implícita que existe dentro de los métodos de una clase y que apunta al objeto actual, es decir, a la instancia sobre la que se está ejecutando el método. Permite acceder de forma explícita a los atributos y métodos del propio objeto, algo útil cuando hay ambigüedad entre atributos y parámetros.
Ejemplo de uso de this en la clase Punto, donde se utiliza para diferenciar los atributos de la clase de los parámetros del constructor:
class Punto {
    double x;
    double y;

    Punto(double x, double y) {
        this.x = x;
        this.y = y;
    }

    double calculaDistanciaAOrigen() {
        return Math.sqrt(this.x * this.x + this.y * this.y);
    }
}


## 13. AÃ±ade ahora otro nuevo mÃ©todo que se llame `distanciaA`, que reciba un `Punto` como parÃ¡metro y calcule la distancia entre `this` y el punto proporcionado

### Respuesta


## 14. El paso del `Punto` como parÃ¡metro a un mÃ©todo, es **por copia** o **por referencia**, es decir, si se cambia el valor de algÃºn atributo del punto pasado como parÃ¡metro, dichos cambios afectan al objeto fuera del mÃ©todo? Â¿QuÃ© ocurre si en vez de un `Punto`, se recibiese un entero (`int`) y dicho entero se modificase dentro de la funciÃ³n? 

### Respuesta
Para añadir el método distanciaA, se aprovecha que cada objeto conoce sus propios atributos mediante this y que puede acceder a los atributos del otro objeto recibido como parámetro. El método calcula la distancia entre dos puntos aplicando la fórmula matemática habitual entre coordenadas en el plano.

El parámetro de tipo Punto representa otro objeto, distinto del actual. Usar this deja claro que una parte de la operación se realiza con el punto que llama al método, lo que ayuda a entender mejor el código y evita ambigüedades.
class Punto {
    double x;
    double y;

    Punto(double x, double y) {
        this.x = x;
        this.y = y;
    }

    double calculaDistanciaAOrigen() {
        return Math.sqrt(this.x * this.x + this.y * this.y);
    }

    double distanciaA(Punto otro) {
        double dx = this.x - otro.x;
        double dy = this.y - otro.y;
        return Math.sqrt(dx * dx + dy * dy);
    }
}


## 15. Â¿QuÃ© es el mÃ©todo `toString()` en Java? Â¿Existe en otros lenguajes? Pon un ejemplo de `toString()` en la clase `Punto` en Java

### Respuesta
El método toString() en Java es un método especial que sirve para obtener una representación en forma de texto de un objeto. Está definido en la clase base Object, de la que heredan todas las clases en Java, y se usa automáticamente en situaciones como imprimir un objeto con System.out.println. Si no se redefine, muestra una información poco útil basada en la dirección de memoria.
class Punto {
    double x;
    double y;

    Punto(double x, double y) {
        this.x = x;
        this.y = y;
    }

    @Override
    public String toString() {
        return "(" + x + ", " + y + ")";
    }
}


## 16. Reflexiona: Â¿una clase es como un `struct` en C? Â¿QuÃ© le falta al `struct` para ser como una clase y las variables de ese tipo ser instancias?


### Respuesta
Una clase se parece a un struct en C, en el sentido de que ambos permiten agrupar datos relacionados bajo un mismo tipo. Desde ese punto de vista, una clase puede verse como una evolución natural del struct, pensada para manejar programas más grandes y complejos de forma más organizada.

Sin embargo, al struct de C le faltan varios elementos clave para ser como una clase. En primer lugar, no puede incluir métodos que formen parte del tipo; las funciones que operan sobre un struct están separadas y deben recibirlo como parámetro. Tampoco existe el concepto de constructor, por lo que la inicialización debe hacerse manualmente.

Además, el struct no ofrece encapsulación ni control de acceso: todos sus campos son públicos y pueden modificarse libremente. En una clase, los datos y el comportamiento están unidos, los objetos son instancias creadas a partir de la clase, y el propio lenguaje refuerza estas reglas, lo que hace el código más seguro y mantenible.

## 17. Quitemos un poco de magia a todo esto: Â¿Como se podrÃ­a â€œemularâ€, con `struct` en C, la clase `Punto`, con su funciÃ³n para calcular la distancia al origen? Â¿QuÃ© ha pasado con `this`?

### Respuesta
En C se puede emular una clase usando un struct para representar los datos y una función que opere sobre ese struct. De este modo, el struct Punto contendría los atributos x e y, y una función recibiría un puntero a dicho struct para calcular la distancia al origen. Esto es una forma habitual de organizar código en C cuando se quiere imitar un estilo orientado a objetos.
#include <math.h>

typedef struct {
    double x;
    double y;
} Punto;

double calculaDistanciaAOrigen(Punto *p) {
    return sqrt(p->x * p->x + p->y * p->y);
}
En este caso, la función calculaDistanciaAOrigen recibe explícitamente un puntero al struct Punto. Ese puntero cumple el mismo papel que this en Java: indica sobre qué “objeto” se está trabajando. La diferencia es que en C el programador debe pasar ese puntero manualmente, mientras que en Java el lenguaje lo hace de forma implícita.