<!--
Posible prompt:
<prompt>
Tengo un cuestionario con preguntas sobre "EncapsulaciÃ³n". Debes tener en cuenta que los conocimientos previos que tengo (y por tanto tus respuestas deben ser adaptadas), son:
- C/C++ sin orientaciÃ³n a objetos.
- Temas de Java previos: Clases y Objetos.

Cada respuesta debe tener entre 2 - 4 pÃ¡rrafos de longitud (sin contar los trozos de cÃ³digo).

Por favor, escribe en impersonal las respuestas.

</prompt>
----
-->
# TEMA 2. EncapsulaciÃ³n

## 1. En ProgramaciÃ³n Orientada a Objetos (POO), Â¿QuÃ© buscan la **encapsulaciÃ³n** y **la ocultaciÃ³n** de informaciÃ³n? Enumera brevemente algunas ventajas de la ocultaciÃ³n de informaciÃ³n.

### Respuesta
La encapsulación y la ocultación de información buscan agrupar datos y métodos en una clase y proteger los datos internos, permitiendo acceder a ellos solo a través de métodos controlados.

Ventajas de la ocultación de información:

Protege los datos de usos incorrectos.

Reduce la dependencia entre partes del programa.

Facilita el mantenimiento y cambios internos.

Mejora la organización del código.

Favorece la reutilización de clases.


## 2. Â¿QuÃ© se entiende por la **interfaz pÃºblica** de un objeto o clase en POO? Describe brevemente cÃ³mo se relaciona con la ocultaciÃ³n de informaciÃ³n.

### Respuesta
La interfaz pública de una clase es el conjunto de métodos públicos que otros objetos pueden usar para interactuar con ella.

Es decir, define qué se puede hacer con el objeto, sin mostrar cómo está implementado internamente.

?? Se relaciona con la ocultación de información porque la clase expone solo lo necesario a través de su interfaz pública y mantiene ocultos sus datos y detalles internos, protegiéndolos y permitiendo cambiar la implementación sin afectar a quien usa la clase.


## 3. Brevemente: Â¿Por quÃ© hay que ser conscientes y diseÃ±ar con cuidado la **interfaz pÃºblica** de una clase? Â¿Es fÃ¡cil cambiarla?

### Respuesta
Hay que diseñar con cuidado la interfaz pública porque es el contrato entre la clase y el resto del programa: otros objetos dependen de ella para funcionar.

?? No es fácil cambiarla, porque cualquier modificación puede romper el código que ya la usa. Por eso debe diseñarse bien desde el principio, para que sea clara, estable y fácil de usar.


## 4. Â¿QuÃ© son las **invariantes de clase** y por quÃ© la ocultaciÃ³n de informaciÃ³n nos ayuda?

### Respuesta
Las invariantes de clase son condiciones o reglas que siempre deben cumplirse para que un objeto esté en un estado válido.

Por ejemplo, en una cuenta bancaria: el saldo no puede ser negativo.

?? La ocultación de información ayuda porque impide que otras partes del programa modifiquen directamente los datos. Así, solo los métodos de la clase pueden cambiarlos y pueden comprobar que las invariantes se cumplan, manteniendo el objeto en un estado correcto.


## 5. Pon un ejemplo de una clase `Punto` en `Java`, con dos coordenadas, `x` e `y`, de tipo `double`, con un mÃ©todo `calcularDistanciaAOrigen`, y que haga uso de la ocultaciÃ³n de informaciÃ³n. Â¿CuÃ¡l es la interfaz pÃºblica de la clase `Punto`? Â¿QuÃ© significa `public` y `private`?

### Respuesta
public class Punto {
    // Atributos ocultos
    private double x;
    private double y;

    // Constructor
    public Punto(double x, double y) {
        this.x = x;
        this.y = y;
    }

    // Método público
    public double calcularDistanciaAOrigen() {
        return Math.sqrt(x * x + y * y);
    }
}
¿Qué significa public y private?

public: el elemento es accesible desde cualquier otra clase. Forma parte de la interfaz pública.

private: el elemento solo puede usarse dentro de la propia clase. Sirve para ocultar los datos internos.

?? Gracias a private, las coordenadas no pueden modificarse directamente desde fuera, lo que protege el estado del objeto.


## 6. En Java, Â¿A quiÃ©nes se pueden aplicar los modificadores `public` o `private`?

### Respuesta
En Java, los modificadores public y private se pueden aplicar a los miembros de una clase, es decir:

Atributos (variables de instancia)

Métodos

Constructores

Clases (con algunas restricciones)

?? public permite que el elemento sea accesible desde otras clases, mientras que private solo permite el acceso dentro de la propia clase, ayudando a la ocultación de información.

## 7. En POO, la visibilidad puede ser pÃºblica o privada, pero Â¿existen mÃ¡s tipos de visibilidad? Â¿QuÃ© ocurre en Java? Â¿Y en otros lenguajes?

### Respuesta
Sí — además de pública y privada, existen otros tipos de visibilidad en POO.

?? La visibilidad controla desde dónde se puede acceder a los miembros de una clase.

?? En Java

Java tiene cuatro niveles de visibilidad:

public ? accesible desde cualquier clase.

private ? accesible solo dentro de la propia clase.

protected ? accesible dentro del mismo paquete y por subclases.

(sin modificador) (package-private) ? accesible solo dentro del mismo paquete.

?? En otros lenguajes

Otros lenguajes de POO (como C++ o C#) también tienen varios niveles de visibilidad, normalmente incluyendo:

public

private

protected

Aunque los detalles exactos pueden cambiar según el lenguaje.

?? En general, los lenguajes modernos ofrecen varios niveles de acceso para controlar mejor la ocultación de información.


## 8. Responde: Los miembros de instancia privados de un objeto estÃ¡n ocultos para (a) otras clases o (b) otras instancias, aunque sean de la misma clase. Pon un ejemplo aÃ±adiendo un mÃ©todo `calcularDistanciaAPunto(Punto otro)` y explica la respuesta.

### Respuesta
Los miembros privados están ocultos para (a) otras clases, pero no para (b) otras instancias de la misma clase.

Es decir, un objeto puede acceder a los miembros private de otro objeto de su misma clase.
public class Punto {
    private double x;
    private double y;

    public Punto(double x, double y) {
        this.x = x;
        this.y = y;
    }

    public double calcularDistanciaAPunto(Punto otro) {
        double dx = this.x - otro.x;
        double dy = this.y - otro.y;
        return Math.sqrt(dx * dx + dy * dy);
    }
}

## 9. Â¿QuÃ© son los mÃ©todos "getter" y "setter" en los lenguajes orientados a objetos?

### Respuesta
Los getters y setters son métodos públicos que permiten leer y modificar atributos privados de una clase de forma controlada.

Getter ? devuelve el valor de un atributo.

Setter ? modifica el valor de un atributo (normalmente validándolo).

Sirven para mantener la encapsulación, evitando el acceso directo a los datos.


## 10. Cuando nos referimos a que la ocultaciÃ³n de informaciÃ³n mejora la "seguridad" del programa, Â¿nos referimos a que no pueda ser "hackeado"?

### Respuesta
No. Cuando decimos que la ocultación de información mejora la “seguridad”, no nos referimos a evitar que el programa sea hackeado.

?? Nos referimos a seguridad interna del programa: prevenir errores, usos incorrectos de los objetos y estados inválidos.

Es una seguridad relacionada con la robustez y fiabilidad del código, no con la ciberseguridad.


## 11. Â¿QuÃ© diferencia hay entre **miembro de instancia** y **miembro de clase**? Â¿Los miembros de clase tambiÃ©n se pueden ocultar?

### Respuesta
Miembro de instancia: pertenece a cada objeto creado de la clase. Cada objeto tiene su propia copia del atributo o método.
Ejemplo: en Punto, x y y son miembros de instancia; cada punto tiene sus propias coordenadas.

Miembro de clase (también llamado static en Java): pertenece a la clase en sí, no a los objetos. Solo hay una copia compartida por todos los objetos.
Ejemplo: static int contadorDePuntos; que lleva la cuenta de todos los puntos creados.

Sí, los miembros de clase también se pueden ocultar usando private. Esto permite controlar su acceso a través de métodos public de la clase.

## 12. Brevemente: Â¿Tiene sentido que los constructores sean privados?

### Respuesta
Sí, tiene sentido.

Un constructor privado evita que otros creen objetos directamente. Esto se usa, por ejemplo, para:

Clases de utilidad (solo métodos estáticos, sin instancias).

Patrones de diseño como Singleton, donde solo puede existir un único objeto de la clase.

?? Así se mantiene control total sobre la creación de objetos.


## 13. Â¿CÃ³mo se indican los **miembros de clase** en Java? Pon un ejemplo, en la clase `Punto` definida anteriormente, para que incluya miembros de clase que permitan saber cuÃ¡les son los valores `x` e `y` mÃ¡ximos que se han establecido en todos los puntos que se hayan creado hasta el momento.

### Respuesta
13. Respuesta

En Java, los miembros de clase se indican con la palabra clave static.

Son compartidos por todos los objetos de la clase.

Se accede a ellos mediante el nombre de la clase (Clase.miembro) o desde los métodos de instancia.

Ejemplo con la clase Punto:
public class Punto {
    private double x;
    private double y;

    // Miembros de clase
    private static double maxX = Double.NEGATIVE_INFINITY;
    private static double maxY = Double.NEGATIVE_INFINITY;

    public Punto(double x, double y) {
        this.x = x;
        this.y = y;

        // Actualizar los máximos si es necesario
        if (x > maxX) maxX = x;
        if (y > maxY) maxY = y;
    }

    // Método de instancia
    public double calcularDistanciaAOrigen() {
        return Math.sqrt(x * x + y * y);
    }

    // Métodos de clase para acceder a los máximos
    public static double getMaxX() {
        return maxX;
    }

    public static double getMaxY() {
        return maxY;
    }
}

## 14. Como serÃ­a un mÃ©todo factorÃ­a dentro de la clase `Punto` para construir un `Punto` a partir de dos coordenadas, pero que las redondee al entero mÃ¡s cercano. Escribe sÃ³lo el cÃ³digo del mÃ©todo, no toda la clase Â¿Has usado `static`? 

### Respuesta
Sí, un método factoría debe ser static, porque crea un objeto sin necesidad de tener uno existente.

Ejemplo:

public static Punto crearRedondeado(double x, double y) {
    int xRedondeado = (int) Math.round(x);
    int yRedondeado = (int) Math.round(y);
    return new Punto(xRedondeado, yRedondeado);
}


static permite llamar al método como Punto.crearRedondeado(3.7, 4.2) sin tener un objeto Punto previo.

El método devuelve un nuevo objeto Punto con las coordenadas redondeadas


## 15. Cambia la implementaciÃ³n de `Punto`. En vez de dos `double`, emplea un array interno de dos posiciones, intentando no modificar la interfaz pÃºblica de la clase.

### Respuesta
Podemos reemplazar los atributos x e y por un array de dos posiciones y mantener la interfaz pública igual (constructores y métodos siguen funcionando).

public class Punto {
    // Array interno para las coordenadas
    private double[] coordenadas = new double[2];

    // Miembros de clase para los máximos
    private static double maxX = Double.NEGATIVE_INFINITY;
    private static double maxY = Double.NEGATIVE_INFINITY;

    // Constructor
    public Punto(double x, double y) {
        coordenadas[0] = x;
        coordenadas[1] = y;

        // Actualizar los máximos
        if (x > maxX) maxX = x;
        if (y > maxY) maxY = y;
    }

    // Método de instancia
    public double calcularDistanciaAOrigen() {
        return Math.sqrt(coordenadas[0] * coordenadas[0] + coordenadas[1] * coordenadas[1]);
    }

    // Método de instancia para calcular distancia a otro punto
    public double calcularDistanciaAPunto(Punto otro) {
        double dx = coordenadas[0] - otro.coordenadas[0];
        double dy = coordenadas[1] - otro.coordenadas[1];
        return Math.sqrt(dx * dx + dy * dy);
    }

    // Métodos de clase para acceder a los máximos
    public static double getMaxX() {
        return maxX;
    }

    public static double getMaxY() {
        return maxY;
    }

    // Método factoría estático
    public static Punto crearRedondeado(double x, double y) {
        int xRedondeado = (int) Math.round(x);
        int yRedondeado = (int) Math.round(y);
        return new Punto(xRedondeado, yRedondeado);
    }
}


? Observaciones:

La interfaz pública no cambia: los métodos y constructores siguen igual.

Internamente usamos coordenadas[0] para x y coordenadas[1] para y.

Esto permite futuras extensiones (por ejemplo, a puntos en 3D) sin romper la interfaz.


## 16. Si un atributo va a tener un mÃ©todo "getter" y "setter" pÃºblicos, Â¿no es mejor declararlo pÃºblico? Â¿CuÃ¡l es la convenciÃ³n mÃ¡s habitual sobre los atributos, que sean pÃºblicos o privados? Â¿Tiene esto algo que ver con las "invariantes de clase"?

### Respuesta


## 17. Â¿QuÃ© significa que una clase sea **inmutable**? Â¿quÃ© es un mÃ©todo modificador? Â¿Un mÃ©todo modificador es siempre un "setter"? Â¿Tiene ventajas que una clase sea inmutable?

### Respuesta


## 18. Â¿Es recomendable incluir mÃ©todos "setter" siempre y como convenciÃ³n?

### Respuesta


## 19. Â¿La clase `String` en Java es mutable o inmutable? Â¿QuÃ© ocurre al concatenar dos cadenas? Â¿QuÃ© debemos hacer si vamos a hacer una operaciÃ³n que implique concatenar muchas veces para construir paso a paso una cadena muy larga?

### Respuesta


## 20. En POO Â¿CÃ³mo se comparan objetos de una misma clase? Â¿Por su contenido o por su identidad? Â¿QuÃ© es el mÃ©todo equals en Java? Â¿QuÃ© hace por defecto? Â¿CÃ³mo se deben comparar dos cadenas en Java? 

### Respuesta


## 21. Â¿QuÃ© son las clases "wrapper" en un lenguaje de programaciÃ³n orientado a objetos? Â¿CÃ³mo se hace? Â¿Es un proceso automÃ¡tico? Â¿QuÃ© ventajas tienen? Â¿Todos los lenguajes orientados a objetos tienen tipos primitivos y necesitan wrappers? 

### Respuesta


## 22. Â¿En POO quÃ© es un **tipo de dato enumerado**? Â¿En Java, un tipo de dato enumerado es una clase? Â¿QuÃ© ventajas tienen en tÃ©rminos de encapsulaciÃ³n los enumerados en Java?

### Respuesta


## 23. Crea un tipo enumerado en Java que se llame `Mes`, con doce posibles instancias y que ademÃ¡s proporcione mÃ©todos para obtener cuÃ¡ntos dÃ­as tiene ese mes, el ordinal de ese mes en el aÃ±o (1-12), empleando atributos privados y constructores del tipo enumerado. AÃ±ade ademÃ¡s cuatro mÃ©todos para devolver si ese mes tiene algunos dÃ­as de invierno, primavera, verano u otoÃ±o, indicando con un booleano el hemisferio (norte o sur, parÃ¡metro `enHemisferioNorte`). Es decir: `esDePrimavera(boolean esHemisferioNorte)`, `esDeVerano(boolean esHemisferioNorte)`, `esDeOtoÃ±o(boolean esHemisferioNorte)`, `esDeInvierno(boolean esHemisferioNorte)`

### Respuesta
