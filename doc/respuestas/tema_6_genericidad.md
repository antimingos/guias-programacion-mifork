<!--
Posible prompt:
<prompt>
Tengo un cuestionario con preguntas sobre "Genericidad". Debes tener en cuenta que los conocimientos previos que tengo (y por tanto tus respuestas deben ser adaptadas), son:
- C/C++ sin orientaciÃ³n a objetos.
- Temas de Java previos: clases y objetos, encapsulaciÃ³n, excepciones, composiciÃ³n, herencia y polimorfismo.

Cada respuesta debe tener entre 2 - 4 pÃ¡rrafos de longitud (sin contar los trozos de cÃ³digo).

Por favor, escribe en impersonal las respuestas.

</prompt>
----
-->
# TEMA 6. Genericidad

## 1. Empleando `void*` en C o `Object` en Java, pon un ejemplo de una estructura de datos, que empleando un array primitivo, permita alojar cualquier tipo de dato.

### Respuesta
En C, se puede lograr una estructura genérica usando un array de punteros `void*`, ya que este tipo puede apuntar a cualquier dato. Sin embargo, es necesario gestionar manualmente la memoria y conocer el tipo real al recuperar los valores, lo que puede provocar errores si se usa incorrectamente.

```c
#include <stdio.h>

int main() {
    void* array[3];

    int a = 10;
    float b = 3.14;
    char c = 'x';

    array[0] = &a;
    array[1] = &b;
    array[2] = &c;

    printf("%d\n", *(int*)array[0]);
    printf("%f\n", *(float*)array[1]);
    printf("%c\n", *(char*)array[2]);

    return 0;
}
```

En Java, se puede usar un array de `Object`, ya que todas las clases heredan de esta. Esto permite almacenar cualquier tipo de objeto, pero obliga a hacer conversiones de tipo (casting) al recuperar los elementos, con el riesgo de errores en tiempo de ejecución.

```java
public class Ejemplo {
    public static void main(String[] args) {
        Object[] array = new Object[3];

        array[0] = 10;       // autoboxing a Integer
        array[1] = 3.14;     // Double
        array[2] = "hola";   // String

        int a = (Integer) array[0];
        double b = (Double) array[1];
        String c = (String) array[2];

        System.out.println(a);
        System.out.println(b);
        System.out.println(c);
    }
}
```

## 2. Brevemente, Â¿QuÃ© significa la **programaciÃ³n genÃ©rica**? Â¿Es el ejemplo anterior un ejemplo bÃ¡sico de programaciÃ³n genÃ©rica? 

### Respuesta
La **programación genérica** consiste en escribir código que pueda trabajar con distintos tipos de datos sin necesidad de duplicarlo para cada tipo. Se basa en abstraer el tipo concreto y permitir que este se especifique más adelante, aumentando la reutilización y la seguridad del código (especialmente en lenguajes como Java con genéricos).

El ejemplo anterior es solo un caso muy básico y limitado. Permite almacenar distintos tipos, pero no es verdadera programación genérica, ya que no hay control de tipos en compilación y se requieren conversiones explícitas (casts), lo que puede producir errores en tiempo de ejecución.

Por tanto, se considera más bien una simulación de genericidad. La programación genérica real (como los *generics* en Java) evita estos problemas proporcionando verificación de tipos en compilación y eliminando la necesidad de casts inseguros.


## 3. Indica los problemas respecto al chequeo de tipos, de emplear `void*` o `Object` cuando se crean estructuras de datos genÃ©ricas. 

### Respuesta
El principal problema es que se pierde el **chequeo de tipos en tiempo de compilación**. Al usar `void*` en C o `Object` en Java, el compilador no puede verificar si el tipo almacenado y el tipo recuperado coinciden, por lo que muchos errores pasan desapercibidos hasta la ejecución.

Además, es necesario realizar conversiones de tipo explícitas (casts) al recuperar los datos. Si se hace un cast incorrecto, el programa puede fallar: en C puede provocar comportamiento indefinido (errores difíciles de detectar), y en Java una excepción en tiempo de ejecución (`ClassCastException`).

Por tanto, este enfoque reduce la seguridad del código y hace más probable introducir errores, ya que la responsabilidad del control de tipos recae completamente en el programador en lugar del compilador.


## 4. Vamos entonces con mecanismos de mejora de la programaciÃ³n genÃ©rica Â¿QuÃ© son los **parÃ¡metros de tipo**? 

### Respuesta
Los **parámetros de tipo** son símbolos (como `T`, `E`, `K`, `V`) que se usan en clases, métodos o interfaces para representar un tipo de dato que no se especifica en el momento de escribir el código, sino al utilizarlo. Permiten definir estructuras y algoritmos que funcionan con distintos tipos sin perder seguridad de tipos.

De esta forma, el compilador puede comprobar que los tipos usados son correctos, evitando errores que aparecerían en ejecución. Esto elimina la necesidad de usar `Object` y de hacer *casts* explícitos, haciendo el código más seguro y claro.

Por ejemplo, una clase `Caja<T>` puede almacenar un objeto de tipo `T`, y al crearla se decide si será `Caja<Integer>`, `Caja<String>`, etc., manteniendo el control de tipos en compilación.


## 5. En Java existe "generics", en C++ existen "templates". Pon un ejemplo de uso de programaciÃ³n genÃ©rica en ambos, instanciando una lista o vector dinÃ¡mico que solo admite `String`. Introduce valores, y luego haz un recorrido de ellos mostrando cÃ³mo cada elemento es del tipo concreto con seguridad.

### Respuesta
En Java, los *generics* permiten definir estructuras de datos parametrizadas por tipo, asegurando en compilación que solo se usen elementos del tipo indicado. Por ejemplo, una lista de `String` impide insertar otros tipos y evita la necesidad de *casts* al recuperar los elementos.

```java id="k2n8sd"
import java.util.ArrayList;

public class Ejemplo {
    public static void main(String[] args) {
        ArrayList<String> lista = new ArrayList<>();

        lista.add("uno");
        lista.add("dos");
        lista.add("tres");

        for (String s : lista) {
            System.out.println(s.toUpperCase());
        }
    }
}
```

En C++, los *templates* permiten un comportamiento similar, generando código específico para cada tipo en compilación. Un `std::vector<std::string>` solo admite cadenas, y cualquier intento de insertar otro tipo produce error de compilación, garantizando seguridad de tipos.

```cpp id="p9x4lm"
#include <iostream>
#include <vector>
#include <string>

int main() {
    std::vector<std::string> v;

    v.push_back("uno");
    v.push_back("dos");
    v.push_back("tres");

    for (const std::string& s : v) {
        std::cout << s << std::endl;
    }

    return 0;
}
```

En ambos casos, el tipo concreto (`String` en Java y `std::string` en C++) se conoce en compilación, lo que permite evitar errores de tipo y elimina la necesidad de conversiones explícitas, a diferencia de usar `Object` o `void*`.


## 6. Sobre el funcionamiento de la programaciÃ³n genÃ©rica. Â¿QuÃ© hace el compilador cuando se instancia una clase que tiene parÃ¡metros de tipo? Â¿Hace lo mismo C++ y Java? Â¿QuÃ© es el "type erasure" de Java y la "instanciaciÃ³n de plantillas" de C++?

### Respuesta
Cuando se instancia una clase con parámetros de tipo, el compilador adapta el código genérico al tipo concreto indicado. Esto permite que las operaciones sean verificadas en compilación y que el uso del tipo sea seguro, evitando errores típicos de los *casts* manuales.

Sin embargo, Java y C++ no hacen lo mismo internamente. En Java se utiliza **type erasure** (borrado de tipos): el compilador comprueba los tipos en compilación, pero luego elimina la información genérica y sustituye los parámetros por `Object` (o su límite). Por tanto, en tiempo de ejecución no existen realmente los tipos genéricos.

En C++, se usa la **instanciación de plantillas**: el compilador genera una versión específica del código para cada tipo utilizado (por ejemplo, una para `int` y otra para `std::string`). Esto mantiene la información de tipos también en el código generado.

En resumen, Java mantiene la seguridad de tipos solo en compilación mediante borrado, mientras que C++ genera código especializado para cada tipo, lo que puede ser más eficiente pero también aumenta el tamaño del código compilado.


## 7. Vamos a crear una nueva clase con parÃ¡metros de tipo. Define en Java una clase `Par`, que permite alojar dos valores de tipos diferentes. Incluye un constructor y un getter para cada tipo. Pon un ejemplo de uso de ese `Par`, por ejemplo para especificar el tipo de retorno de una funciÃ³n que devuelve en un `Par` la media y desviaciÃ³n tÃ­pica de un array de `double`. 

### Respuesta
Se puede definir una clase genérica `Par` con dos parámetros de tipo (por ejemplo `T` y `U`), lo que permite almacenar dos valores de tipos distintos con seguridad en compilación. El compilador comprobará que los tipos usados son correctos y no será necesario hacer *casts* al recuperar los valores.

```java id="a1b2c3"
public class Par<T, U> {
    private T primero;
    private U segundo;

    public Par(T primero, U segundo) {
        this.primero = primero;
        this.segundo = segundo;
    }

    public T getPrimero() {
        return primero;
    }

    public U getSegundo() {
        return segundo;
    }
}
```

Un uso típico sería devolver dos resultados relacionados desde una función, como la media y la desviación típica de un array de `double`. En este caso, ambos valores serían `Double`, y el tipo concreto del `Par` se indica al usarlo.

```java id="d4e5f6"
public class Estadistica {
    public static Par<Double, Double> calcular(double[] datos) {
        double suma = 0;
        for (double d : datos) suma += d;
        double media = suma / datos.length;

        double sumaDif = 0;
        for (double d : datos) sumaDif += Math.pow(d - media, 2);
        double desviacion = Math.sqrt(sumaDif / datos.length);

        return new Par<>(media, desviacion);
    }

    public static void main(String[] args) {
        double[] datos = {1, 2, 3, 4, 5};
        Par<Double, Double> resultado = calcular(datos);

        System.out.println("Media: " + resultado.getPrimero());
        System.out.println("Desviación: " + resultado.getSegundo());
    }
}
```

De este modo, se consigue devolver varios valores con tipos bien definidos, manteniendo la seguridad de tipos en compilación y evitando errores de conversión.


## 8. En Java, se pueden declarar parÃ¡metros de tipo tambiÃ©n a nivel de mÃ©todo, no solo a nivel de clase. Pon un ejemplo con un mÃ©todo genÃ©rico `seleccionaUno`, que pasados dos objetos del mismo tipo, te devuelva aleatoriamente uno de ellos. Muestra la diferencia de definirlo con dos `Object`, a definirlo con dos parÃ¡metros de tipo, en terminos de (i) evitar downcasting y (ii) forzar que ambos objetos sean del mismo tipo. 

### Respuesta
Se puede definir un método genérico usando un parámetro de tipo `<T>`, de forma que ambos argumentos y el valor de retorno sean del mismo tipo. Esto permite que el compilador garantice que los dos objetos son compatibles y evita conversiones posteriores.

```java id="g7h8i9"
import java.util.Random;

public class Ejemplo {

    public static <T> T seleccionaUno(T a, T b) {
        return new Random().nextBoolean() ? a : b;
    }

    public static void main(String[] args) {
        String s = seleccionaUno("uno", "dos"); // correcto, sin casts
        System.out.println(s);
    }
}
```

Si se define con `Object`, se pierde esa seguridad. Aunque permite pasar cualquier tipo, obliga a hacer *downcasting* al recuperar el valor, lo que puede provocar errores en ejecución si el tipo no coincide.

```java id="j1k2l3"
import java.util.Random;

public class Ejemplo {

    public static Object seleccionaUno(Object a, Object b) {
        return new Random().nextBoolean() ? a : b;
    }

    public static void main(String[] args) {
        Object res = seleccionaUno("uno", "dos");
        String s = (String) res; // requiere cast
        System.out.println(s);
    }
}
```

Con el método genérico, se evita el *downcasting* porque el compilador ya conoce el tipo de retorno. Además, se fuerza que ambos parámetros sean del mismo tipo (`T`), mientras que con `Object` se podrían mezclar tipos distintos sin error en compilación, aumentando el riesgo de fallos en tiempo de ejecución.


## 9. Â¿Se pueden establecer restricciones en los parÃ¡metros de tipo? Por ejemplo, si quiero definir un tipo genÃ©rico `<T>`, Â¿puedo decir que tenga que ser, al menos, un nÃºmero para poder tratarlo como tal? Pon un ejemplo en Java de un `Punto` con dos coordenadas, metodos `getX`, `getY`, y una funciÃ³n `calcularDistanciaA` otro `Punto`. Permite que esas coordenadas sean cualquier tipo de nÃºmero. Pon dos soluciones: una simplemente creando coordenadas de tipo `Number` y otra aÃ±adiendo generics para reforzar el chequeo de tipos y saber exactamente con quÃ© tipo de nÃºmero trabaja el `Punto`. En este caso y respecto al "type erasure", Â¿cuÃ¡l es el tipo final tras la compilaciÃ³n?

### Respuesta


## 10. Sobre las soluciones anteriores. Si bien ambas permiten trabajar con distintos tipos de nÃºmero sin duplicar la clase `Punto`, reflexiona sobre el refuerzo del chequeo de tipos con generics. Â¿Permiten ambas crear un punto con una coordenada de tipo entero y la otra coordenada de tipo real? Â¿QuÃ© tipo devuelve el `getX` con la solucion sin generics y quÃ© tipo devuelve el que tiene la soluciÃ³n con generics?

### Respuesta


## 11. Hagamos un ejemplo avanzado. El siguiente cÃ³digo, con interfaz `Punto`, que define un mÃ©todo `calcularDistanciaA(Punto p)`, junto con las implementaciones `Punto2D` y `Punto3D`. AÃ±ade generics para asegurarnos que la sobreescritura del mÃ©todo calcular distancia a otro `Punto` siempre es sobre un `Punto` del mismo tipo, evitando `instanceof` y el downcasting.
```java
public interface Punto { 
    public double distanciaA(Punto p); 
} 

public class Punto2D implements Punto { 
     private final double x, y; 
     public Punto2D(double x, double y) { 
        this.x = x; this.y = y; 
    } 

    @Override 
    public double distanciaA(Punto p) { 
        if (p instanceof Punto2D) { 
            Punto2D p2d = (Punto2D) p; 
            return Math.sqrt(Math.pow(x - p2d.x, 2) 
                    + Math.pow(y - p2d.y, 2)); 
        } else { 
            throw new RuntimeException("p debe ser Punto 2D"); 
        } 
    } 
} 
public class Punto3D implements Punto { 
    // Igual que Punto2D, pero con tres coordenadas
    ...
} 
```

### Respuesta


## 12. Dado que `String` es subtipo de `Object`, Â¿significa eso que `List<String>` es subtipo de `List<Object>`? Â¿Y que `String[]` es subtipo de `Object[]`? Razona por quÃ© la respuesta es diferente en cada caso y quÃ© problema en tiempo de ejecuciÃ³n puede aparecer con los arrays. A partir de estos ejemplos, define quÃ© significa que un tipo genÃ©rico sea **covariante**, **contravariante** o **invariante** respecto a su parÃ¡metro de tipo.

### Respuesta


## 13. Java permite recuperar covarianza y contravarianza en tipos genÃ©ricos de forma controlada mediante **wildcards**. Â¿QuÃ© es un wildcard (`?`)? Muestra la diferencia entre `List<? extends T>` y `List<? super T>`, indicando en quÃ© casos se usa cada uno. Pon dos ejemplos: (i) un mÃ©todo que reciba una lista de nÃºmeros y calcule su suma, usando `? extends`; (ii) un mÃ©todo que reciba una lista y le aÃ±ada varios nÃºmeros enteros, usando `? super`.

### Respuesta
