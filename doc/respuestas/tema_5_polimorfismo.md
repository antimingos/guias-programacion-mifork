<!--
Posible prompt:
<prompt>
Tengo un cuestionario con preguntas sobre "Polimorfismo". Debes tener en cuenta que los conocimientos previos que tengo (y por tanto tus respuestas deben ser adaptadas), son:
- C/C++ sin orientaciÃ³n a objetos.
- Temas de Java previos: Clases y Objetos, EncapsulaciÃ³n, Excepciones, ComposiciÃ³n y Herencia.

Cada respuesta debe tener entre 2 - 4 pÃ¡rrafos de longitud (sin contar los trozos de cÃ³digo).

Por favor, escribe en impersonal las respuestas.

</prompt>
----
-->
# Tema 5. Polimorfismo

## 1. Brevemente, Â¿quÃ© es el **"polimorfismo"** y para quÃ© sirve en programaciÃ³n orientada a objetos? Â¿quÃ© es la **"sobreescritura"** de mÃ©todos?

### Respuesta
El polimorfismo es una característica de la programación orientada a objetos que permite tratar objetos de distintas clases de manera uniforme a través de una misma referencia (por ejemplo, una clase padre). Es decir, diferentes objetos pueden responder de forma distinta a una misma llamada de método. Esto resulta útil para escribir código más flexible, reutilizable y fácil de mantener, ya que permite trabajar con tipos generales sin depender de implementaciones concretas.

En Java, el polimorfismo se observa principalmente cuando se usa una referencia de una clase base para apuntar a objetos de clases derivadas. Aunque la referencia sea del tipo padre, el método que se ejecuta depende del tipo real del objeto en tiempo de ejecución.

La sobreescritura de métodos (override) ocurre cuando una clase hija redefine un método heredado de su clase padre, manteniendo el mismo nombre, parámetros y tipo de retorno. Esto permite modificar o especializar el comportamiento del método original según las necesidades de la subclase.

class Animal {
    void hacerSonido() {
        System.out.println("Sonido genérico");
    }
}

class Perro extends Animal {
    @Override
    void hacerSonido() {
        System.out.println("Ladrido");
    }
}


## 2. Â¿En quÃ© consiste la **"ligadura dinÃ¡mica"** o **"enlace tardÃ­o"**? Â¿quÃ© relaciÃ³n tiene con el polimorfismo? Â¿hay que indicarlos explÃ­citamente al programar o depende esto del lenguaje? Compara C++ y Java. Indicalo despuÃ©s tambiÃ©n para Python.

### Respuesta
La ligadura dinámica o enlace tardío es el mecanismo por el cual la llamada a un método se resuelve en tiempo de ejecución, en lugar de en tiempo de compilación. Esto significa que no se decide qué método ejecutar hasta que el programa está en marcha, dependiendo del tipo real del objeto y no del tipo de la referencia.

Está directamente relacionada con el polimorfismo, ya que es lo que permite que una misma llamada a un método tenga comportamientos distintos según el objeto concreto. Sin ligadura dinámica, el polimorfismo no funcionaría correctamente, porque siempre se ejecutaría la versión del método asociada al tipo declarado de la variable.

En cuanto a su uso, depende del lenguaje. En Java, la ligadura dinámica es el comportamiento por defecto para los métodos (no hace falta indicarlo explícitamente). En cambio, en C++, solo ocurre si se usan métodos declarados como virtual; si no, se utiliza enlace temprano (en tiempo de compilación).

En Python, la ligadura dinámica también es el comportamiento por defecto. Todos los métodos se resuelven en tiempo de ejecución, por lo que el polimorfismo se aplica de forma automática sin necesidad de palabras clave especiales.


## 3. Pon un ejemplo sencillo en Java, de un `Soldado`, con un mÃ©todo `saluda`, con dos subclases: `Zapador` y `Artillero`, donde `Zapador` sobreescribe el mÃ©todo `saludar`, sustituyendo por completo su comportamiento. Ilustra el funcionamiento del polimorfismo creando un array de `Soldados` de dos tipos y luego recorriÃ©ndolo empleando referencias de tipo `Soldado` y llamando a `saludar`.

### Respuesta
Se puede definir una clase base Soldado con un método saludar, y dos subclases Zapador y Artillero. La subclase Zapador sobreescribe completamente el método para cambiar su comportamiento, mientras que Artillero puede mantener el comportamiento original (o redefinirlo también, si se desea).

El polimorfismo se observa al usar un array de tipo Soldado que contiene objetos de distintas subclases. Aunque la referencia sea del tipo base, el método que se ejecuta en cada caso depende del tipo real del objeto en tiempo de ejecución.

class Soldado {
    void saludar() {
        System.out.println("Saludo general de soldado");
    }
}

class Zapador extends Soldado {
    @Override
    void saludar() {
        System.out.println("Zapador: listo para abrir camino");
    }
}

class Artillero extends Soldado {
    // Usa el método heredado (no lo sobreescribe)
}

public class Main {
    public static void main(String[] args) {
        Soldado[] ejercito = new Soldado[2];
        ejercito[0] = new Zapador();
        ejercito[1] = new Artillero();

        for (Soldado s : ejercito) {
            s.saludar(); // polimorfismo
        }
    }
}


## 4. Si sobreescribo un mÃ©todo, Â¿puedo invocar el mÃ©todo base para trabajar a partir de su resultado? Haz que zapador cambie ligeramente la forma de saludar, que salude de forma normal, tal cual hace el soldado base, pero que ademÃ¡s aÃ±ada un "ZAPADOR A SUS ORDENES" Â¿quÃ© palabra clave del lenguaje has usado para invocar al mÃ©todo de la clase base?

### Respuesta
Sí, cuando un método es sobreescrito se puede invocar el método de la clase base para reutilizar su comportamiento y construir encima de él. Esto permite modificar o ampliar la funcionalidad sin tener que reescribir todo el código del método original.

En Java se utiliza la palabra clave super para llamar a la implementación del método en la clase padre. De esta forma, primero se ejecuta el comportamiento base y luego se añade el comportamiento específico de la subclase.

En el caso del Zapador, se puede llamar primero a super.saludar() y después añadir el mensaje adicional.

class Soldado {
    void saludar() {
        System.out.println("Saludo general de soldado");
    }
}

class Zapador extends Soldado {
    @Override
    void saludar() {
        super.saludar(); 
        System.out.println("ZAPADOR A SUS ÓRDENES");
    }
}


## 5. Al sobreescribir un mÃ©todo en Java, Â¿quÃ© restricciones existen sobre los tipos de los parÃ¡metros y el tipo de retorno? Â¿QuÃ© diferencia hay entre sobreescritura (*overriding*) y sobrecarga (*overloading*)? Â¿Para quÃ© sirve la anotaciÃ³n `@Override` y por quÃ© es recomendable usarla siempre?

### Respuesta
Al sobrescribir un método en Java, los parámetros deben ser exactamente los mismos que en el método de la clase padre (mismo número, tipo y orden). Si cambian los parámetros, ya no es sobreescritura. En cuanto al tipo de retorno, debe ser el mismo o un tipo derivado (covariante) en caso de objetos.

La diferencia entre overriding (sobreescritura) y overloading (sobrecarga) es que la sobreescritura ocurre entre clase padre e hija, redefiniendo el mismo método. En cambio, la sobrecarga ocurre dentro de la misma clase, creando métodos con el mismo nombre pero con distintos parámetros.

La anotación @Override indica al compilador que se está intentando sobrescribir un método de la clase padre. Es recomendable usarla siempre porque detecta errores, como escribir mal el nombre del método o cambiar mal los parámetros, evitando que el método se considere uno nuevo por error.


## 6. Entonces, cuando se estudia Java, Â¿se emplea el polimorfismo desde el principio? Por ejemplo, sobreescribiendo `toString` o sobreescribiendo `equals`, Â¿ya estoy usando polimorfismo?

### Respuesta
Sí, el polimorfismo se utiliza desde los primeros pasos en Java, aunque no siempre se identifique de forma explícita. Cada vez que se sobrescribe un método heredado de Object, como toString() o equals(), ya se está aplicando polimorfismo, porque se está redefiniendo el comportamiento de un método según la clase concreta del objeto.
En estos casos, aunque la referencia sea de tipo Object o de una clase padre, el método que se ejecuta depende del tipo real del objeto en tiempo de ejecución. Esto es exactamente el principio del polimorfismo mediante sobreescritura.
Por tanto, incluso en ejemplos básicos de Java, el polimorfismo ya está presente, aunque de forma implícita. No se limita a jerarquías complejas, sino que aparece en cualquier uso de métodos heredados que se redefinen.


## 7. Â¿QuÃ© es una **"clase abstracta"**? Â¿QuÃ© es un **"mÃ©todo abstracto"**? Â¿Puedo crear instancias de una clase abstracta? Pongamos un ejemplo en Java: Redefinamos `Soldado`, hagamos que, ademÃ¡s del mÃ©todo `saluda` que ya tenÃ­a, tenga un mÃ©todo `atacar`, que sea abstracto y que cada tipo de soldado haga su acciÃ³n cuando se le pida atacar. Â¿Donde debemos poner `abstract`?

### Respuesta


## 8. Â¿QuÃ© efecto tiene la palabra clave `final` sobre mÃ©todos y clases en Java? Â¿CÃ³mo se relaciona con el polimorfismo? Â¿Conoces algÃºn ejemplo de clase `final` en la propia API estÃ¡ndar de Java?

### Respuesta


## 9. En Java, quÃ© son las **"interfaces"**? Â¿Son como clases abstractas? Â¿Una clase puede implementar mÃ¡s de una interfaz?

### Respuesta


## 10. Vamos a poner un ejemplo nuevo con polimorfismo. Queremos implementar una clase `Punto`, con un mÃ©todo `calcularDistanciaA`, que permite calcular la distancia a otro `Punto`. Sin embargo, como queremos trabajar con puntos 2D y 3D, haz que ese mÃ©todo sea abstracto y haya dos implementaciones de ese cÃ¡lculo de distancia. Emplea `instanceof` y *downcasting* para verificar que se recibe un punto compatible y poder calcular correctamente la distancia siempre entre puntos del mismo subtipo. Aprovecha este diseÃ±o para crear ahora una clase `Linea`, que acepta `Punto`, sin saber de quÃ© tipo es, y es capaz de dar su longitud independientemente de las dimensiones de sus puntos (las cuales desconoce).

### Respuesta


## 11. Â¿QuÃ© es la **"herencia de interfaces"** en Java? Â¿Existe **"herencia mÃºltiple de interfaces"**? Pon un ejemplo de una interfaz `Fichero` que tenga un mÃ©todo para leer su contenido en forma de `String` y luego dicha interfaz sea extendida por otra que sea `FicheroEscribible` que permita enviar contenido e incluso eliminar el fichero.

### Respuesta
