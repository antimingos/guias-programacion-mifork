<!--
Posible prompt:
<prompt>
Tengo un cuestionario con preguntas sobre "ComposiciÃ³n". Debes tener en cuenta que los conocimientos previos que tengo (y por tanto tus respuestas deben ser adaptadas), son:
- C/C++ sin orientaciÃ³n a objetos.
- Temas de Java previos: Clases y Objetos, EncapsulaciÃ³n y Excepciones.

Cada respuesta debe tener entre 2 - 4 pÃ¡rrafos de longitud (sin contar los trozos de cÃ³digo).

Por favor, escribe en impersonal las respuestas.

</prompt>
----
-->
# Tema 4.1. ComposiciÃ³n


## 1. En C, podemos crear estructuras mayores **componiendo** unas con otras, que suelen describirse como "A tiene-un/tiene-varios B". Pon un ejemplo, empleando `struct`, de una lÃ­nea de puntos, donde puntos tienen dos coordenadas (`x` e `y`), y la lÃ­nea esta hecha de dos puntos. Incluye una funciÃ³n para calcular la distancia entre puntos y otra para hallar la longitud de una lÃ­nea.

### Respuesta
En C se pueden crear estructuras más complejas componiendo otras más simples. Esto se conoce como una relación “tiene-un”, donde una estructura contiene otras dentro de ella. Por ejemplo, un punto puede representarse con dos coordenadas (x e y), y una línea puede definirse como dos puntos: el punto inicial y el punto final.

Primero se define la estructura Punto. Después se define la estructura Linea, que contiene dos variables de tipo Punto. De esta forma se expresa que una línea tiene dos puntos. Esta técnica permite organizar mejor los datos y reutilizar estructuras ya definidas.

Para trabajar con estas estructuras se pueden crear funciones. Una función calcula la distancia entre dos puntos usando la fórmula de distancia euclidiana. Otra función calcula la longitud de una línea, simplemente aplicando la función de distancia a los dos puntos que forman la línea.

#include <stdio.h>
#include <math.h>

struct Punto {
    double x;
    double y;
};

struct Linea {
    struct Punto p1;
    struct Punto p2;
};

double distancia(struct Punto a, struct Punto b) {
    double dx = a.x - b.x;
    double dy = a.y - b.y;
    return sqrt(dx*dx + dy*dy);
}

double longitudLinea(struct Linea l) {
    return distancia(l.p1, l.p2);
}


## 2. Ahora transforma ese ejemplo a orientaciÃ³n a objetos con Java, para tener un primer ejemplo de **composiciÃ³n** en orientaciÃ³n a objetos. Crea una clase `Punto`, y una clase `Linea`. La clase `Punto` debe tener un mÃ©todo para calcular distancia a otro `Punto` y `Linea` debe tener un mÃ©todo para calcular su longitud. Gracias a la ocultaciÃ³n de informaciÃ³n, supera a C, garantizando que los puntos sean inmutables, al igual que la lÃ­nea, que una vez creada, no queremos que se modifique de quÃ© a quÃ© puntos va dicha lÃ­nea.  

### Respuesta
En Java se puede aplicar composición creando clases que contienen objetos de otras clases. En este caso, una Linea tiene dos objetos Punto: el punto inicial y el punto final. Esto refleja la misma idea que en C, pero usando clases y objetos propios de la orientación a objetos.

La clase Punto contiene las coordenadas x e y y un método distancia para calcular la distancia a otro punto. Para garantizar la inmutabilidad, los atributos se declaran private y final, y no se proporcionan métodos setter. De esta forma, una vez creado un punto, sus coordenadas no pueden modificarse.

La clase Linea contiene dos objetos Punto y un método longitud que calcula la distancia entre ellos usando el método de Punto. Sus atributos también son private y final, por lo que la línea tampoco puede cambiar después de crearse.

public class Punto {
    private final double x;
    private final double y;

    public Punto(double x, double y) {
        this.x = x;
        this.y = y;
    }

    public double distancia(Punto otro) {
        double dx = this.x - otro.x;
        double dy = this.y - otro.y;
        return Math.sqrt(dx*dx + dy*dy);
    }
}

public class Linea {
    private final Punto p1;
    private final Punto p2;

    public Linea(Punto p1, Punto p2) {
        this.p1 = p1;
        this.p2 = p2;
    }

    public double longitud() {
        return p1.distancia(p2);
    }
}


## 3. Â¿QuÃ© significa la **multiplicidad** en la composiciÃ³n? En el ejemplo anterior, Â¿cuÃ¡l es la multiplicidad entre `Linea` y `Punto`? IndÃ­calo expresando la multiplicidad en ambas direcciones, de `Linea` a `Punto` y de `Punto` a `Linea`.

### Respuesta
La multiplicidad en la composición indica cuántos objetos de una clase pueden estar relacionados con objetos de otra clase. Se usa para describir la cantidad mínima y máxima de elementos que participan en la relación. Es un concepto común en el diseño de clases y en diagramas UML para entender cómo se conectan los objetos.

En el ejemplo anterior, una Linea está formada por exactamente dos Punto: el punto inicial y el punto final. Por tanto, la multiplicidad de Linea a Punto es 2, ya que cada línea siempre contiene dos puntos.

En sentido contrario, un Punto puede pertenecer a cero, una o varias líneas, porque el mismo punto podría usarse como extremo de muchas líneas distintas. Por ello, la multiplicidad de Punto a Linea es 0..* (de cero a muchos). Esto significa que un punto no tiene por qué estar en ninguna línea, pero también puede formar parte de muchas.


## 4. Â¿QuÃ© significa composiciÃ³n **fuerte** y composiciÃ³n **dÃ©bil**? Â¿QuÃ© consecuencia implica en relaciÃ³n al ciclo de vida de los objetos? Indica a cuÃ¡l solemos referirnos como **"asociaciÃ³n o agregaciÃ³n"** y a cuÃ¡l como **"composiciÃ³n"** propiamente.

### Respuesta
La composición fuerte y la composición débil se diferencian en el grado de dependencia entre los objetos. En ambos casos existe una relación “tiene-un”, pero cambia cómo se relacionan sus ciclos de vida.

En la composición fuerte, el objeto contenido depende completamente del objeto que lo contiene. Esto significa que se crea y se destruye junto con él, y normalmente no se comparte con otros objetos. Si el objeto principal desaparece, las partes que lo componen también dejan de existir. A esta relación se le suele llamar composición propiamente.

En la composición débil, el objeto contenido puede existir independientemente del objeto que lo utiliza. Puede ser compartido por varios objetos y seguir existiendo aunque uno de ellos desaparezca. A esta relación se le suele llamar asociación o agregación.


## 5. Cuando una clase usa a otra al recibirla o devolverla como parÃ¡metro en algÃºn mÃ©todo, al hacer `new` dentro de un mÃ©todo, o al usarlas como variables locales, Â¿hablamos de composiciÃ³n o de **"dependencia"**?

### Respuesta
Cuando una clase utiliza otra solo dentro de un método, por ejemplo como parámetro, valor de retorno, variable local o creando un objeto con new dentro del método, se habla de dependencia. En este caso la clase no guarda el objeto como parte de su estado, sino que simplemente lo usa temporalmente para realizar alguna operación.

La composición ocurre cuando un objeto contiene a otro como atributo (campo) de la clase. Esto significa que el objeto forma parte de la estructura interna de la clase y existe mientras exista el objeto que lo contiene. Por tanto, la relación es más fuerte y permanente.

En cambio, en una dependencia la relación es más débil y momentánea. La clase solo necesita a la otra para ejecutar cierta funcionalidad, pero no la mantiene como parte de sí misma. Por eso se dice que una clase depende de otra cuando solo la utiliza dentro de sus métodos.


## 6. En el ejemplo anterior de lÃ­nea y punto, programa la relaciÃ³n entre `Linea` y `Punto` de dos formas. Una **como composiciÃ³n fuerte**, donde el ciclo de vida de los puntos estÃ¡ ligado al de Linea y otra **como composiciÃ³n dÃ©bil**, donde no.

### Respuesta
En el ejemplo de Linea y Punto, la relación puede implementarse de dos formas según el ciclo de vida de los objetos. Si los puntos se crean dentro de Linea y solo existen como parte de ella, se trata de composición fuerte. Si los puntos se crean fuera y se pasan a la línea, entonces pueden existir independientemente y se considera composición débil (agregación).

En la composición fuerte, la clase Linea crea los objetos Punto dentro de su constructor. Así, los puntos dependen completamente de la línea y no existen fuera de ella. Si la línea desaparece, también lo hacen sus puntos.

class Linea {
    private final Punto p1;
    private final Punto p2;

    public Linea(double x1, double y1, double x2, double y2) {
        this.p1 = new Punto(x1, y1);
        this.p2 = new Punto(x2, y2);
    }

    public double longitud() {
        return p1.distancia(p2);
    }
}


En la composición débil (agregación), los puntos se crean fuera de la línea y se pasan como parámetros al constructor. Esto permite que los mismos puntos puedan ser usados por varias líneas o existir sin estar ligados a una en concreto.

class Linea {
    private final Punto p1;
    private final Punto p2;

    public Linea(Punto p1, Punto p2) {
        this.p1 = p1;
        this.p2 = p2;
    }

    public double longitud() {
        return p1.distancia(p2);
    }
}


## 7. En Java, en la composiciÃ³n fuerte, Â¿cuando el contenedor destruye los objetos? No se observa que `Linea` destruya los `Punto` explÃ­citamente, Â¿Por quÃ©?

### Respuesta


## 8. Pon un ejemplo de composicion dÃ©bil entre un departamento que tiene varios profesores. Implementa dos composiciones a la vez: entre el departamento y todos sus profesores y entre el departamento y su director, que es un profesor del departamento. Siempre debe haber un director en el departamento desde el inicio. Lanza excepciones si se viola la invariante. Emplea arrays primitivos de Java, estilo `Profesor[]`, con mÃ¡ximo 50, pero no rompas la encapsulaciÃ³n, no desveles que estÃ¡s empleando un array, permite aÃ±adir un `Profesor` al final de la lista, y eliminar un profesor dada su posiciÃ³n. Da acceso a los profesores con un mÃ©todo para saber cuÃ¡ntos hay y otro para obtener un profesor por posiciÃ³n. El director se puede cambiar por otro profesor del departamento. Sin embargo, ten en cuenta esta invariante de clase: el director debe formar siempre parte de la lista de profesores, es decir, ten cuidado al cambiar el director o al eliminar un profesor.

### Respuesta


## 9. En Java, existen tambiÃ©n `List`, cambia y muestra cÃ³mo serÃ­a el cÃ³digo anterior empleando `List` en vez de arrays primitivos. Â¿QuÃ© parte del cÃ³digo original te has ahorrado? AdemÃ¡s, fÃ­jate en el mÃ©todo `getProfesor(int pos)`: si en su lugar existiera un mÃ©todo que devolviera todos los profesores a la vez, Â¿quÃ© problema tendrÃ­a devolver directamente la lista interna? Â¿CÃ³mo lo resolverÃ­as?

### Respuesta


## 10. Al igual que ocurre con las excepciones en Java, que pueden encerrar causas (que son excepciones), de forma recursiva, suponen un tipo especial de composiciones, denominadas composiciones recursivas. Pon un ejemplo en Java de una `Persona`, que sea inmutable, y que tiene una madre, que es otra `Persona`. Haz un main con un ejemplo de uso con una familia de personas, desde el nieto hasta la abuela. Enumera algÃºn otro ejemplo clÃ¡sico de composiciones recursivas.

### Respuesta

## 11. Â¿QuÃ© son las relaciones de composiciÃ³n "bidireccionales"? Â¿QuÃ© habrÃ­a que hacer para implementar este tipo de relaciÃ³n en el ejemplo de `Profesor` y `Departamento`?

### Respuesta
