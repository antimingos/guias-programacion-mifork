<!--
Posible prompt:
<prompt>
Tengo un cuestionario con preguntas sobre "Aspectos funcionales". Debes tener en cuenta que los conocimientos previos que tengo (y por tanto tus respuestas deben ser adaptadas), son:
- C/C++ sin orientaciÃ³n a objetos.
- Temas de Java previos: clases y objetos, encapsulaciÃ³n, excepciones, composiciÃ³n, herencia, polimorfismo y genericidad.

Cada respuesta debe tener entre 2 - 4 pÃ¡rrafos de longitud (sin contar los trozos de cÃ³digo).

Por favor, escribe en impersonal las respuestas.

</prompt>
----
-->

# TEMA 7. Aspectos funcionales

## 1. Â¿QuÃ© es un puntero a una funciÃ³n? Pon un ejemplo de cÃ³digo en C, donde se define una funciÃ³n y que reciba una cadena de caracteres como parÃ¡metro y devuelva la cadena en mayÃºsculas. Crea un puntero en una variable local a dicha funciÃ³n llamado `aMayusculas` e invÃ³cala con el puntero.

### Respuesta
Un puntero a una función es una variable que almacena la dirección de memoria de una función. En C, las funciones también ocupan memoria, por lo que es posible referenciarlas igual que se hace con variables. Esto permite pasar funciones como parámetros, almacenarlas en estructuras o invocarlas indirectamente, lo cual resulta útil para implementar comportamientos dinámicos.

Para declarar un puntero a función, se debe indicar el tipo de retorno y los tipos de los parámetros de la función a la que apuntará. La sintaxis puede parecer compleja al principio, pero sigue la misma lógica que la declaración de funciones. Una vez declarado, se puede asignar la dirección de una función compatible y llamarla como si fuera una función normal.

A continuación se muestra un ejemplo donde se define una función que convierte una cadena a mayúsculas, se crea un puntero llamado `aMayusculas` y se invoca a través de él:

```c
#include <stdio.h>
#include <ctype.h>

char* convertirAMayusculas(char* str) {
    for (int i = 0; str[i] != '\0'; i++) {
        str[i] = toupper(str[i]);
    }
    return str;
}

int main() {
    char texto[] = "hola mundo";

    // Declaración del puntero a función
    char* (*aMayusculas)(char*);

    // Asignación de la función al puntero
    aMayusculas = convertirAMayusculas;

    // Invocación de la función a través del puntero
    char* resultado = aMayusculas(texto);

    printf("%s\n", resultado);

    return 0;
}
```

En este ejemplo, el puntero `aMayusculas` apunta a la función `convertirAMayusculas` y se utiliza para invocarla. El uso de punteros a función permite desacoplar la llamada de la implementación concreta, facilitando la reutilización y flexibilidad del código.


## 2. Â¿QuÃ© es una **funciÃ³n lambda** en un lenguaje de programaciÃ³n? Pon un ejemplo similar al anterior en Javascript y otro en Java con funciones lambda. Usa una variable local `aMayusculas` para apuntar a la funciÃ³n lambda. Por simplicidad, en Java, emplea `Function<String, String>` para el tipo de la referencia a la funciÃ³n lambda.

### Respuesta
Una función lambda es una función anónima que puede definirse en el mismo lugar donde se utiliza, sin necesidad de darle un nombre explícito. Se emplea principalmente para expresar comportamientos simples de forma concisa y para pasar funciones como datos. Este tipo de funciones es común en lenguajes que soportan programación funcional o características funcionales.

Las funciones lambda permiten reducir código repetitivo y mejorar la legibilidad cuando se necesitan operaciones pequeñas. En lugar de definir una función completa, se escribe directamente la lógica. Suelen utilizarse junto con estructuras que aceptan funciones como parámetros, como colecciones o APIs de procesamiento de datos.

Ejemplo en JavaScript:

```javascript
const aMayusculas = (str) => {
    return str.toUpperCase();
};

const resultado = aMayusculas("hola mundo");
console.log(resultado);
```

Ejemplo en Java usando `Function<String, String>`:

```java
import java.util.function.Function;

public class Main {
    public static void main(String[] args) {
        Function<String, String> aMayusculas = (str) -> {
            return str.toUpperCase();
        };

        String resultado = aMayusculas.apply("hola mundo");
        System.out.println(resultado);
    }
}
```

En ambos casos, la variable `aMayusculas` referencia una función lambda que recibe una cadena y devuelve su versión en mayúsculas. Esto permite tratar funciones como valores, de forma similar a los punteros a función en C, pero con una sintaxis más sencilla y segura.


## 3. Â¿QuÃ© es el **paradigma funcional**? Â¿Por quÃ© a algunos lenguajes orientados a objetos como Java 8, se les llama multi-paradigma? Â¿QuÃ© quiere decir que las funciones son "ciudadanos de primera clase"?

### Respuesta
El paradigma funcional es un estilo de programación donde el cálculo se basa en la evaluación de funciones, evitando en lo posible el uso de estado mutable y efectos secundarios. En este enfoque, las funciones reciben datos de entrada y producen resultados sin modificar variables externas, lo que facilita el razonamiento sobre el programa y reduce errores. Se promueve el uso de funciones puras, composición de funciones y estructuras de datos inmutables.

Algunos lenguajes orientados a objetos, como Java a partir de su versión 8, se consideran multi-paradigma porque incorporan características propias de otros estilos de programación, como el funcional. Esto permite combinar clases y objetos con funciones lambda, interfaces funcionales y operaciones sobre colecciones (como streams), ofreciendo más formas de resolver un mismo problema según convenga.

Decir que las funciones son “ciudadanos de primera clase” significa que se pueden tratar como cualquier otro valor del lenguaje. Es decir, pueden almacenarse en variables, pasarse como argumentos a otras funciones, devolverse como resultado y construirse dinámicamente. Esta capacidad es fundamental en la programación funcional, ya que permite escribir código más flexible, reutilizable y expresivo.


## 4. Explica la sintaxis bÃ¡sica de una funciÃ³n lambda en Java.

### Respuesta
En Java, una función lambda es una forma concisa de representar una implementación de una interfaz funcional (es decir, una interfaz con un único método abstracto). Su sintaxis básica es: `(parámetros) -> expresión` o `(parámetros) -> { bloque de código }`. La parte izquierda indica los parámetros de entrada y la derecha define el cuerpo de la función.

Cuando la lambda contiene una sola expresión, no es necesario usar llaves ni la palabra `return`, ya que el valor se devuelve implícitamente. En cambio, si el cuerpo tiene varias instrucciones, se deben usar llaves y `return` explícito. Los tipos de los parámetros pueden omitirse si el compilador puede inferirlos a partir del contexto (por ejemplo, del tipo de la interfaz funcional).

Las lambdas se asignan normalmente a variables cuyo tipo es una interfaz funcional, como `Function`, `Predicate` o `Consumer`. Por ejemplo:
`Function<String, String> f = s -> s.toUpperCase();`
Aquí, se recibe una cadena y se devuelve su versión en mayúsculas. Esto permite escribir código más breve y expresivo, especialmente al trabajar con colecciones y APIs funcionales.


## 5. Ahora recibamos una funciÃ³n como parÃ¡metro a un mÃ©todo y la llamaremos desde dentro. Amplia los ejemplos anteriores de Java y JavaScript con un mÃ©todo llamado `transformar`, que reciba un `String` como parÃ¡metro y luego una funciÃ³n transformadora como lo es `aMayÃºsculas` y la invoque desde dentro.

### Respuesta
Para recibir una función como parámetro, se define un método que acepte tanto el dato como la función transformadora. Internamente, el método invoca esa función sobre el dato recibido y devuelve el resultado. Este enfoque permite desacoplar la lógica de transformación del método que la utiliza, haciendo el código más reutilizable.

En lenguajes con soporte funcional, como JavaScript o Java (desde la versión 8), esto se realiza pasando funciones o lambdas como argumentos. En JavaScript se pasan directamente, mientras que en Java se emplean interfaces funcionales como `Function<String, String>`, que definen el tipo de la función a recibir.

Ejemplo en JavaScript:

```javascript id="m3x8r1"
const aMayusculas = (str) => {
    return str.toUpperCase();
};

function transformar(texto, funcion) {
    return funcion(texto);
}

const resultado = transformar("hola mundo", aMayusculas);
console.log(resultado);
```

Ejemplo en Java:

```java id="n92kdl"
import java.util.function.Function;

public class Main {

    public static String transformar(String texto, Function<String, String> funcion) {
        return funcion.apply(texto);
    }

    public static void main(String[] args) {
        Function<String, String> aMayusculas = (str) -> {
            return str.toUpperCase();
        };

        String resultado = transformar("hola mundo", aMayusculas);
        System.out.println(resultado);
    }
}
```

En ambos casos, el método `transformar` recibe una cadena y una función, y aplica dicha función sobre la cadena. Esto ilustra cómo las funciones pueden pasarse como parámetros, igual que cualquier otro dato.


## 6. Ahora, invoca `transformar`, con una nueva funciÃ³n lambda directamente en la llamada a `transformar`, por ejemplo, una funciÃ³n lambda que invierta la cadena. Define la funciÃ³n de inversiÃ³n justo cuando la estÃ¡s pasando como parÃ¡metro.

### Respuesta
Se puede pasar una función lambda directamente en la llamada a `transformar` sin necesidad de asignarla previamente a una variable. Esto permite definir el comportamiento en el mismo punto donde se utiliza, lo que resulta útil para operaciones simples o puntuales. En este caso, se define una lambda que invierte la cadena recibida.

La idea es que `transformar` sigue recibiendo un `String` y una función, pero ahora la función se construye “al vuelo”. Esto muestra claramente cómo las funciones pueden crearse dinámicamente y pasarse como argumentos, una característica clave del paradigma funcional.

Ejemplo en JavaScript:

```javascript id="k2p9zx"
function transformar(texto, funcion) {
    return funcion(texto);
}

const resultado = transformar("hola mundo", (str) => {
    return str.split("").reverse().join("");
});

console.log(resultado);
```

Ejemplo en Java:

```java id="q8v3lm"
import java.util.function.Function;

public class Main {

    public static String transformar(String texto, Function<String, String> funcion) {
        return funcion.apply(texto);
    }

    public static void main(String[] args) {
        String resultado = transformar("hola mundo", (str) -> {
            return new StringBuilder(str).reverse().toString();
        });

        System.out.println(resultado);
    }
}
```

En ambos ejemplos, la función lambda que invierte la cadena se define directamente en la llamada a `transformar`, sin necesidad de variables intermedias. Esto hace el código más compacto y enfocado en la operación concreta que se desea realizar.


## 7. Â¿QuÃ© se entiende por cierre o "closure" en el contexto de las funciones lambda? Pon un ejemplo en Java de cÃ³mo una funciÃ³n lambda es capaz de acceder a una variable local en el contexto donde fue definida. Modifica el ejemplo anterior, creando otra funciÃ³n lambda para transformar una cadena, pero que lo que haga es concatenar a la cadena de entrada otra cadena que estÃ¡ en una variable local definida fuera de la funciÃ³n lambda.

### Respuesta
Un cierre o *closure* es una función que “recuerda” el entorno donde fue creada, pudiendo acceder a variables externas a ella. En el contexto de funciones lambda, esto significa que la lambda puede usar variables locales definidas fuera de su cuerpo. En Java, estas variables deben ser *finales* o *efectivamente finales* (es decir, que no cambien después de su inicialización).

Esto permite que la función lambda utilice información del contexto sin necesidad de recibirla como parámetro explícito. De este modo, se pueden construir funciones más flexibles y expresivas, manteniendo el código sencillo y evitando pasar demasiados argumentos.

A continuación se muestra una modificación del ejemplo anterior, donde se define una variable local externa y la lambda la utiliza para concatenar su contenido a la cadena de entrada:

```java id="z7n4qp"
import java.util.function.Function;

public class Main {

    public static String transformar(String texto, Function<String, String> funcion) {
        return funcion.apply(texto);
    }

    public static void main(String[] args) {
        String sufijo = "!!!"; // variable local (efectivamente final)

        String resultado = transformar("hola mundo", (str) -> {
            return str + sufijo;
        });

        System.out.println(resultado);
    }
}
```

En este ejemplo, la lambda accede a la variable `sufijo`, definida fuera de ella. Esto es posible gracias al mecanismo de *closure*, que captura el valor de esa variable en el momento de la creación de la lambda.


## 8. Reflexiona: Â¿en quÃ© se diferencia entonces una funciÃ³n lambda de los punteros a funciones que hay en C?

### Respuesta
La diferencia principal es que una función lambda no es solo una referencia a código, sino que también puede capturar el contexto donde se define (closure). En C, un puntero a función únicamente almacena la dirección de una función ya definida, sin ninguna información adicional sobre variables externas. Por tanto, no puede acceder automáticamente a variables locales del entorno donde se usa.

Otra diferencia importante es el nivel de abstracción y seguridad. En C, los punteros a función requieren una sintaxis más compleja y son menos seguros, ya que no existe verificación estricta más allá del tipo de la firma. En cambio, las lambdas en lenguajes como Java o JavaScript tienen una sintaxis más simple y se integran con el sistema de tipos (en Java, mediante interfaces funcionales), lo que reduce errores.

Además, las lambdas permiten definir funciones de forma anónima en el mismo punto donde se necesitan, sin tener que declarar una función aparte. En C, siempre es necesario definir la función previamente y luego referenciarla mediante el puntero. Esto hace que las lambdas sean más flexibles y expresivas, especialmente en contextos donde se requiere pasar comportamientos de forma dinámica.


## 9. Devolvamos ahora funciones. Creemos ahora una funciÃ³n que sea capaz de crear funciones "descuento". Una funciÃ³n "descuento", decrementa un porcentaje pasado como parÃ¡metro. Por simplicidad, usa `Function<Double, Double>` para su tipo. La funciÃ³n `crearDescuento(porcentaje)`, recibe solo el porcentaje de descuento a aplicar y devuelve la funciÃ³n de descuento. Prueba a crear dos descuentos distintos y aplicarlos a una cantidad. Explica la closure en la funciÃ³n descuento.

### Respuesta
Se puede definir una función que devuelva otra función utilizando lambdas. En este caso, `crearDescuento(porcentaje)` recibe un valor y devuelve una función que aplica ese porcentaje a cualquier cantidad. Esto es posible gracias a que en Java las lambdas pueden implementarse como valores de tipo `Function<Double, Double>`.

La función devuelta será distinta según el porcentaje recibido, ya que ese valor queda “capturado” en la lambda. De este modo, se pueden generar múltiples funciones especializadas (por ejemplo, 10% o 20% de descuento) sin necesidad de escribir varias funciones diferentes.

Ejemplo en Java:

```java id="d4k9pz"
import java.util.function.Function;

public class Main {

    public static Function<Double, Double> crearDescuento(double porcentaje) {
        return (precio) -> {
            return precio - (precio * porcentaje / 100.0);
        };
    }

    public static void main(String[] args) {
        Function<Double, Double> descuento10 = crearDescuento(10);
        Function<Double, Double> descuento20 = crearDescuento(20);

        double precio = 100.0;

        double precioCon10 = descuento10.apply(precio);
        double precioCon20 = descuento20.apply(precio);

        System.out.println(precioCon10); // 90.0
        System.out.println(precioCon20); // 80.0
    }
}
```

En este ejemplo, cada lambda devuelta por `crearDescuento` forma un *closure*, ya que captura el valor de `porcentaje` definido en el contexto donde se creó. Así, cada función recuerda su propio porcentaje incluso después de que haya terminado la ejecución de `crearDescuento`, permitiendo aplicar descuentos diferentes de forma independiente.


## 10. En Java, que es un lenguaje con comprobaciÃ³n estÃ¡tica de tipos, donde los tipos se declaran, toda funciÃ³n lambda tiene un tipo, que se conoce como **interfaz funcional**. Â¿QuÃ© es una **interfaz funcional**? Â¿QuÃ© requisitos tiene?

### Respuesta
Una interfaz funcional es una interfaz de Java que contiene exactamente un único método abstracto. Este método define el “contrato funcional” que puede ser implementado por una función lambda. Gracias a esto, el compilador puede asociar una lambda a ese único método y tratarla como una implementación de la interfaz.

El requisito principal es que la interfaz tenga un solo método abstracto. Puede, sin embargo, incluir varios métodos por defecto (`default`) o estáticos, ya que estos no afectan a la naturaleza funcional de la interfaz. Si se añade más de un método abstracto, la interfaz deja de ser funcional y ya no puede usarse directamente con lambdas.

Además, es común (aunque no obligatorio) usar la anotación `@FunctionalInterface` para indicar explícitamente la intención. Esta anotación ayuda al compilador a verificar que se cumple la restricción de un solo método abstracto, evitando errores por diseño. Un ejemplo típico es `Function<T, R>`, que representa una función que recibe un tipo `T` y devuelve un tipo `R`.


## 11. Creemos una interfaz funcional a mano. Por ejemplo, define la interfaz funcional del ejemplo que transforma la cadena en otra. LlÃ¡male `Transformador`, que define una funciÃ³n que convierte una cadena de texto (`String`) en otra (`String`).

### Respuesta
Una interfaz funcional puede definirse manualmente en Java indicando un único método abstracto que represente la operación funcional. En este caso, la interfaz `Transformador` representa una función que recibe un `String` y devuelve otro `String`. Esto permite que cualquier lambda compatible pueda implementarla.

El objetivo de esta interfaz es servir como tipo para funciones lambda, de forma similar a como `Function<String, String>` lo hace en la API estándar. Al tener un solo método abstracto, el compilador puede asociar directamente una lambda a ese método.

Ejemplo de definición:

```java id="t5k2mn"
@FunctionalInterface
public interface Transformador {
    String transformar(String texto);
}
```

Con esta interfaz, se pueden definir lambdas que cumplan su contrato, por ejemplo:

```java id="r8p1xz"
public class Main {

    public static String aplicar(String texto, Transformador t) {
        return t.transformar(texto);
    }

    public static void main(String[] args) {
        Transformador aMayusculas = (str) -> str.toUpperCase();

        String resultado = aplicar("hola mundo", aMayusculas);

        System.out.println(resultado);
    }
}
```

En este caso, la interfaz `Transformador` actúa como tipo funcional. La lambda implementa su único método, permitiendo transformar cadenas de forma flexible y reutilizable.


## 12. Ahora hagamos la interfaz funcional algo mÃ¡s genÃ©rica y empleando generics, para que permita definir un `Transformador` de un tipo en otro. Pon un ejemplo de un transformador que redondea un `Double` en un `Integer`.

### Respuesta
Una interfaz funcional genérica permite definir transformaciones entre tipos distintos utilizando *generics*. En este caso, se puede parametrizar la interfaz con dos tipos: uno de entrada y otro de salida. Esto hace que el transformador sea reutilizable para cualquier tipo de conversión sin necesidad de redefinir la interfaz.

Al mantener un único método abstracto, la interfaz sigue siendo funcional y puede usarse directamente con expresiones lambda. El uso de generics permite que el compilador verifique la coherencia de tipos en tiempo de compilación, lo que aporta seguridad y flexibilidad.

Definición de la interfaz genérica:

```java id="g7k3lp"
@FunctionalInterface
public interface Transformador<T, R> {
    R transformar(T entrada);
}
```

Ejemplo de uso para convertir `Double` a `Integer` redondeando:

```java id="h2m9qr"
public class Main {

    public static void main(String[] args) {
        Transformador<Double, Integer> redondear = (valor) -> {
            return (int) Math.round(valor);
        };

        Integer resultado1 = redondear.transformar(4.6);
        Integer resultado2 = redondear.transformar(3.2);

        System.out.println(resultado1); // 5
        System.out.println(resultado2); // 3
    }
}
```

En este ejemplo, la interfaz `Transformador<T, R>` permite definir una función que convierte un tipo en otro. La lambda implementa la transformación de `Double` a `Integer`, capturando el comportamiento de redondeo. Esto muestra cómo los generics combinados con funciones permiten crear abstracciones muy reutilizables.


## 13. `Transformador`, en su versiÃ³n genÃ©rica, parece muy Ãºtil y reutilizable, hasta el punto de que es igual a una interfaz funcional que ya hay, que es `Function<T, R>`. Muestra las interfaces funcionales predefinidas que hay en Java.

### Respuesta
En Java ya existen varias interfaces funcionales predefinidas en el paquete `java.util.function`, diseñadas para cubrir los casos de uso más comunes al trabajar con programación funcional. Estas interfaces evitan tener que definir interfaces propias como `Transformador`, ya que proporcionan tipos genéricos reutilizables y bien integrados con la API del lenguaje.

La más general es `Function<T, R>`, que representa una función que recibe un valor de tipo `T` y devuelve un valor de tipo `R`. A partir de ella se construyen muchas operaciones habituales. También existen otras interfaces especializadas según el tipo de entrada, salida o comportamiento esperado.

Algunas de las interfaces funcionales más utilizadas en Java son:

* `Function<T, R>`: recibe un tipo y devuelve otro distinto.
* `Predicate<T>`: recibe un tipo y devuelve un `boolean` (condición).
* `Consumer<T>`: recibe un tipo y no devuelve nada (efecto lateral).
* `Supplier<T>`: no recibe nada y devuelve un tipo (generador de valores).
* `UnaryOperator<T>`: recibe y devuelve el mismo tipo (`T -> T`).
* `BinaryOperator<T>`: recibe dos valores del mismo tipo y devuelve uno del mismo tipo.

Estas interfaces permiten expresar de forma clara distintos patrones funcionales sin necesidad de crear nuevas definiciones. Por ejemplo, el `Transformador<Double, Integer>` del ejercicio anterior equivale directamente a `Function<Double, Integer>`.


## 14. Vamos a ver ejemplos expresivos de funcional en Java. Estudiemos el `List.forEach`, como versiÃ³n funcional del bucle `for`. Emplea el `forEach` para recorrer una lista de `Integer` y que muestre un mensaje si el entero es positivo.

### Respuesta
El método `forEach` en Java es una forma funcional de recorrer colecciones, ya que recibe una función (normalmente una lambda) que se aplica a cada elemento de la lista. Sustituye al bucle `for` tradicional, haciendo el código más declarativo y centrado en la operación que se quiere realizar en cada elemento, en lugar de en el control del recorrido.

En este caso, se puede usar `forEach` sobre una lista de `Integer` para comprobar si cada valor es positivo. La lambda recibida se ejecuta una vez por cada elemento de la lista, recibiendo dicho elemento como parámetro.

Ejemplo en Java:

```java id="f3k8lm"
import java.util.Arrays;
import java.util.List;

public class Main {

    public static void main(String[] args) {
        List<Integer> numeros = Arrays.asList(-2, 5, 0, 8, -1, 3);

        numeros.forEach((n) -> {
            if (n > 0) {
                System.out.println(n + " es positivo");
            }
        });
    }
}
```

En este ejemplo, `forEach` aplica la lambda a cada elemento de la lista. La lambda actúa como una función que recibe un número y ejecuta una acción si cumple la condición de ser positivo. Esto elimina la necesidad de escribir un bucle `for` explícito y hace el código más directo y expresivo.

## 15. Repasando el tema de genericidad, fÃ­jate en la firma de `forEach`, Â¿por quÃ© se usa `Consumer<? super T>` y no `Consumer<T>`? Explica quÃ© significa **PECS**, y explÃ­calo para el caso de mejorar el ejemplo del mÃ©todo `transformar` la hora de definir el tipo de la funciÃ³n transformadora.

### Respuesta
En `forEach`, la firma usa `Consumer<? super T>` en lugar de `Consumer<T>` debido a reglas de *wildcards* en generics. La idea es permitir mayor flexibilidad en la compatibilidad de tipos. Si se usara `Consumer<T>` de forma estricta, solo se podrían aceptar consumidores exactamente del tipo de la colección, lo que sería más restrictivo.

El uso de `? super T` está relacionado con el principio **PECS** (*Producer Extends, Consumer Super*). Este principio indica que si una estructura **produce** valores, se debe usar `extends`, y si **consume** valores, se debe usar `super`. En el caso de `Consumer`, la función consume valores, por lo que tiene sentido usar `super T`, permitiendo que el consumidor acepte tipos más generales que `T`.

En el caso de `forEach`, esto permite, por ejemplo, que una lista de `Integer` pueda aceptar un `Consumer<Number>` o `Consumer<Object>`, ya que ambos pueden consumir enteros sin problema. Esto hace la API más flexible y reutilizable sin perder seguridad de tipos.

Aplicando esto al método `transformar`, que recibe una función que consume un `String` y devuelve otro `String`, el tipo puede mejorarse usando PECS en la parte de entrada de la función. Es decir, en lugar de fijar estrictamente `Function<String, String>`, se puede generalizar la entrada:

```java id="p9k2ab"
public static <R> R transformar(
        String texto,
        Function<? super String, ? extends R> funcion) {
    return funcion.apply(texto);
}
```

Aquí se aplica PECS así:

* `? super String` indica que la función puede aceptar `String` o un supertipo (más general) como entrada.
* `? extends R` indica que el resultado puede ser `R` o un subtipo, aumentando flexibilidad.

Esto mejora la reutilización del método `transformar`, ya que permite pasar funciones más genéricas sin perder seguridad de tipos, manteniendo el sistema de tipos estático de Java más expresivo y flexible.

## 16. Referencias a mÃ©todos. Podemos obtener una referencia a mÃ©todos de objetos o clases. Pon un ejemplo en JavaScript y en Java, de una clase `Persona` con un mÃ©todo `saludar`. En el cÃ³digo principal, crea una `Persona` con un nombre, y obtÃ©n una referencia a su mÃ©todo `saludar` en una variable local. Invoca `saludar` con esa referencia a su mÃ©todo `saludar`.

### Respuesta
Las referencias a métodos permiten reutilizar un método existente como si fuera una función, sin necesidad de envolverlo en una lambda explícita. En JavaScript se obtienen directamente a partir de objetos, mientras que en Java se utilizan referencias a métodos con la sintaxis `::`, siempre asociadas a un contexto compatible con una interfaz funcional.

En ambos casos, la idea es separar la invocación del método de su ejecución inmediata, almacenando la referencia en una variable y utilizándola posteriormente como una función. Esto es especialmente útil en programación funcional, ya que permite pasar métodos como parámetros o reutilizarlos en estructuras como streams o callbacks.

Ejemplo en JavaScript:

```javascript id="jsref1"
class Persona {
    constructor(nombre) {
        this.nombre = nombre;
    }

    saludar() {
        return "Hola, soy " + this.nombre;
    }
}

const persona = new Persona("Ana");

// referencia al método
const saludarRef = persona.saludar.bind(persona);

// invocación a través de la referencia
console.log(saludarRef());
```

Ejemplo en Java:

```java id="javaref1"
import java.util.function.Supplier;

class Persona {
    private String nombre;

    public Persona(String nombre) {
        this.nombre = nombre;
    }

    public String saludar() {
        return "Hola, soy " + nombre;
    }
}

public class Main {
    public static void main(String[] args) {
        Persona persona = new Persona("Ana");

        // referencia al método
        Supplier<String> saludarRef = persona::saludar;

        // invocación a través de la referencia
        System.out.println(saludarRef.get());
    }
}
```

En este ejemplo, el método `saludar` se referencia sin ejecutarse inmediatamente. En Java, `persona::saludar` se asigna a un `Supplier<String>`, que permite invocarlo posteriormente con `get()`. Esto muestra cómo los métodos pueden tratarse como valores funcionales reutilizables.


## 17. Â¿QuÃ© tipos de referencias a mÃ©todo se pueden hacer en Java? Pon un ejemplo de referencia a mÃ©todo estÃ¡tico, a constructor, a mÃ©todo de instancia de una instancia concreta y a mÃ©todo de instancia sobre cualquier instancia.

### Respuesta
En Java existen cuatro tipos principales de referencias a métodos. Todas ellas permiten tratar métodos como funciones asociadas a interfaces funcionales, evitando escribir lambdas explícitas cuando ya existe un método compatible. La diferencia entre ellas depende de si el método pertenece a una clase, a una instancia concreta o si se trata de un constructor.

El primer tipo es la referencia a método estático, que se escribe como `Clase::metodoEstatico`. El segundo es la referencia a constructor, que se escribe como `Clase::new` y permite crear objetos de forma funcional. El tercero es la referencia a método de una instancia concreta, que se escribe como `objeto::metodo`. El cuarto es la referencia a método de instancia de cualquier objeto de un tipo concreto, que se escribe como `Clase::metodoInstancia`.

Ejemplo en Java con todos los casos:

```java id="ref17a"
import java.util.function.Function;
import java.util.function.Supplier;
import java.util.function.Consumer;

class Persona {
    private String nombre;

    public Persona() {
        this.nombre = "Sin nombre";
    }

    public Persona(String nombre) {
        this.nombre = nombre;
    }

    public String saludar() {
        return "Hola, soy " + nombre;
    }

    public void mostrar() {
        System.out.println(saludar());
    }

    public static String despedida(String nombre) {
        return "Adiós, " + nombre;
    }
}

public class Main {
    public static void main(String[] args) {

        // 1. Referencia a método estático
        Function<String, String> refEstatico = Persona::despedida;
        System.out.println(refEstatico.apply("Ana"));

        // 2. Referencia a constructor
        Supplier<Persona> refConstructor = Persona::new;
        Persona p1 = refConstructor.get();

        // 3. Método de instancia de una instancia concreta
        Persona persona = new Persona("Luis");
        Supplier<String> refInstanciaConcreta = persona::saludar;
        System.out.println(refInstanciaConcreta.get());

        // 4. Método de instancia de cualquier instancia
        Consumer<Persona> refInstanciaGenerica = Persona::mostrar;
        refInstanciaGenerica.accept(persona);
    }
}
```

En estos ejemplos se observa que cada tipo de referencia depende del contexto en el que se invoca el método. Las referencias a métodos permiten reutilizar código existente de forma más declarativa, integrándose de manera natural con interfaces funcionales.


## 18. Otro ejemplo expresivo. Ordena una lista de `Persona`, cada persona tiene un nombre y una edad (de tipo entero). Ordena la lista de `Persona` con `Collections.sort`, pasÃ¡ndole como comparador una expresiÃ³n lambda que compare la edad de ambas personas y si tienen la misma edad, se ordene por orden alfabÃ©tico del nombre. Crea dos versiones: Una con la funciÃ³n de comparaciÃ³n hecha manualmente, y otra empleando `Comparator`.

### Respuesta
En este ejercicio se utiliza `Collections.sort`, que permite ordenar listas en Java a partir de un criterio de comparación. Dicho criterio puede definirse mediante una expresión lambda, lo que evita tener que crear clases adicionales como ocurría antes de Java 8. La comparación debe establecer primero el criterio principal (edad) y, en caso de empate, un criterio secundario (nombre).

En la primera versión se implementa la comparación manualmente dentro de la lambda, comparando explícitamente los campos `edad` y `nombre`. En la segunda versión se utiliza la API de `Comparator`, que proporciona métodos auxiliares como `comparing` y `thenComparing`, haciendo el código más declarativo y legible.

Ejemplo de implementación manual:

```java id="sort18a"
import java.util.*;

class Persona {
    String nombre;
    int edad;

    public Persona(String nombre, int edad) {
        this.nombre = nombre;
        this.edad = edad;
    }
}

public class Main {
    public static void main(String[] args) {

        List<Persona> lista = new ArrayList<>();
        lista.add(new Persona("Ana", 30));
        lista.add(new Persona("Luis", 25));
        lista.add(new Persona("Carlos", 30));
        lista.add(new Persona("Bea", 25));

        Collections.sort(lista, (p1, p2) -> {
            if (p1.edad != p2.edad) {
                return p1.edad - p2.edad;
            } else {
                return p1.nombre.compareTo(p2.nombre);
            }
        });

        for (Persona p : lista) {
            System.out.println(p.nombre + " " + p.edad);
        }
    }
}
```

Ejemplo usando `Comparator`:

```java id="sort18b"
import java.util.*;

class Persona {
    String nombre;
    int edad;

    public Persona(String nombre, int edad) {
        this.nombre = nombre;
        this.edad = edad;
    }
}

public class Main {
    public static void main(String[] args) {

        List<Persona> lista = new ArrayList<>();
        lista.add(new Persona("Ana", 30));
        lista.add(new Persona("Luis", 25));
        lista.add(new Persona("Carlos", 30));
        lista.add(new Persona("Bea", 25));

        Collections.sort(
            lista,
            Comparator.comparingInt((Persona p) -> p.edad)
                      .thenComparing(p -> p.nombre)
        );

        for (Persona p : lista) {
            System.out.println(p.nombre + " " + p.edad);
        }
    }
}
```

En la primera versión se controla manualmente la lógica de comparación, mientras que en la segunda se delega en `Comparator`, que permite expresar el orden de forma más clara y modular. Ambas soluciones son equivalentes, pero la segunda es más legible y escalable cuando aumentan los criterios de ordenación.
