<!--
Posible prompt:
<prompt>
Tengo un cuestionario con preguntas sobre "Herencia". Debes tener en cuenta que los conocimientos previos que tengo (y por tanto tus respuestas deben ser adaptadas), son:
- C/C++ sin orientaciÃ³n a objetos.
- Temas de Java previos: Clases y Objetos, EncapsulaciÃ³n, Excepciones y ComposiciÃ³n.

Cada respuesta debe tener entre 2 - 4 pÃ¡rrafos de longitud (sin contar los trozos de cÃ³digo).

Por favor, escribe en impersonal las respuestas.

</prompt>
----
-->
## 1. En orientaciÃ³n a objetos, Â¿quÃ© es la **herencia** y su relaciÃ³n con "A es-un B"?. Explica las dos implicaciones principales: (1) **compatibilidad de tipos** y (2) **herencia de estado y comportamiento**. Pon un ejemplo en Java muy sencillo, donde un `Soldado` tiene un `nombre` (privado) y un mÃ©todo `saludar()` que muestra su nombre. Hay dos subtipos: un `Artillero`, que es capaz de disparar cohetes y un `Zapador` que pone minas, ambos heredan el atributo nombre y la capacidad de saludar. AdemÃ¡s, y de forma especÃ­fica, el artillero tiene un nÃºmero de cohetes y el zapador un nÃºmero de minas, accesibles mediante "getters" especÃ­ficos. Respecto a la compatibilidad de tipos, aprovechÃ©mosla: crea un array de `Soldado`, mete varios de distinto tipo (son todos compatibles con `Soldado`). RecÃ³rrela y que todos te saluden.

### Respuesta
La herencia en orientación a objetos permite crear una clase nueva a partir de otra, reutilizando sus atributos y métodos. La relación “A es-un B” significa que una subclase es un caso particular de la superclase; por ejemplo, un Artillero es-un Soldado. Esto implica que comparten una misma base conceptual.

La primera implicación es la compatibilidad de tipos: un objeto de una subclase puede usarse como si fuera de la superclase. Por ejemplo, se pueden guardar Artillero y Zapador en un array de Soldado y tratarlos igual. La segunda es la herencia de estado y comportamiento: las subclases heredan atributos (como nombre) y métodos (como saludar()), y además pueden añadir los suyos propios.

class Soldado {
    private String nombre;

    public Soldado(String nombre) {
        this.nombre = nombre;
    }

    public void saludar() {
        System.out.println("Hola, soy " + nombre);
    }
}

class Artillero extends Soldado {
    private int numCohetes;

    public Artillero(String nombre, int numCohetes) {
        super(nombre);
        this.numCohetes = numCohetes;
    }

    public int getNumCohetes() {
        return numCohetes;
    }
}

class Zapador extends Soldado {
    private int numMinas;

    public Zapador(String nombre, int numMinas) {
        super(nombre);
        this.numMinas = numMinas;
    }

    public int getNumMinas() {
        return numMinas;
    }
}

public class Main {
    public static void main(String[] args) {
        Soldado[] ejercito = {
            new Artillero("Carlos", 5),
            new Zapador("Luis", 3),
            new Artillero("Ana", 2)
        };

        for (Soldado s : ejercito) {
            s.saludar();
        }
    }
}


## 2. Al crear los soldados concretos, Â¿cuÃ¡ntos constructores se ejecutan y en quÃ© orden? Â¿QuÃ© significa `super` dentro de un constructor? Si la clase base no tiene visible el constructor sin parÃ¡metros, Â¿debo llamar a `super` siempre? 

### Respuesta
Al crear un objeto de una subclase (por ejemplo, Artillero o Zapador), se ejecutan dos constructores: primero el de la superclase (Soldado) y después el de la subclase. Este orden es obligatorio, ya que primero debe inicializarse la parte común del objeto (heredada) y luego la parte específica. Es decir, siempre se construye “de arriba hacia abajo” en la jerarquía.

La palabra clave super dentro de un constructor se usa para llamar al constructor de la superclase. Permite inicializar los atributos heredados (como nombre) desde la subclase. Por ejemplo, super(nombre) llama al constructor de Soldado que recibe ese parámetro.

Si la clase base no tiene un constructor sin parámetros accesible, entonces es obligatorio llamar a super(...) explícitamente. Si no se hace, el compilador dará error, ya que intenta llamar automáticamente a un constructor vacío que no existe o no es visible.

## 3. Respecto a los objetos de subclases en memoria, los atributos privados de la superclase, Â¿forman parte de una instancia de la subclase en memoria? En caso afirmativo Â¿implica que se puedan usar desde el cÃ³digo de la subclase? ExplÃ­calo con el ejemplo de `Soldado` y alguna de sus subclases.

### Respuesta
Sí, los atributos privados de la superclase sí forman parte de la instancia de la subclase en memoria. Por ejemplo, un objeto Artillero contiene internamente tanto su propio atributo (numCohetes) como el atributo nombre heredado de Soldado. Es decir, el objeto completo incluye toda la información definida en la jerarquía.

Sin embargo, esto no implica que puedan usarse directamente desde el código de la subclase. Al ser nombre un atributo private en Soldado, no es accesible directamente desde Artillero. Solo puede manipularse a través de métodos públicos o protegidos definidos en la superclase (como saludar() o posibles getters).

Por tanto, aunque el estado está presente en memoria, el acceso está controlado por la encapsulación. Esto obliga a usar la interfaz de la superclase para interactuar con esos datos, manteniendo el diseño seguro y coherente.

## 4. Â¿QuÃ© implica en tÃ©rminos de **extensibilidad** de cÃ³digo el hecho de que sean compatibles a nivel de tipos? Ilustra esto aÃ±adiendo un nuevo tipo de `Soldado` y demostrando que el cÃ³digo para pedir el saludo a todos los soldados no se modifica.

### Respuesta
La compatibilidad de tipos permite escribir código más extensible, ya que se puede trabajar con la superclase (Soldado) sin depender de las subclases concretas. Esto significa que se pueden añadir nuevos tipos de soldados sin tener que modificar el código existente que ya trabaja con Soldado. El código queda abierto a ampliaciones, pero cerrado a modificaciones.

Por ejemplo, se puede añadir un nuevo tipo de soldado, como Medico, que también hereda de Soldado. Este nuevo tipo tendrá su propio estado y comportamiento, pero seguirá siendo compatible con Soldado, por lo que puede usarse en el mismo array sin cambiar nada del código que recorre y hace saludar a los soldados.

class Medico extends Soldado {
    private int botiquines;

    public Medico(String nombre, int botiquines) {
        super(nombre);
        this.botiquines = botiquines;
    }

    public int getBotiquines() {
        return botiquines;
    }
}

public class Main {
    public static void main(String[] args) {
        Soldado[] ejercito = {
            new Artillero("Carlos", 5),
            new Zapador("Luis", 3),
            new Medico("Eva", 4) // nuevo tipo añadido
        };

        for (Soldado s : ejercito) {
            s.saludar(); // no se modifica
        }
    }
}

De esta forma, el código que usa Soldado no necesita cambiar al añadir nuevas subclases, lo que facilita el mantenimiento y la evolución del programa.


## 5. En Java, cuando trabajo con referencias y herencia. Â¿Puedo tener una referencia del supertipo que apunte a objetos reales de un subtipo? Â¿Puedo invocar con la referencia del supertipo a mÃ©todos pÃºblicos del subtipo? Â¿En quÃ© consiste el **"upcasting"** y el **"downcasting"**? Â¿QuÃ© es el `instanceof`? Pon un ejemplo de recorrido de un array de `Soldado`, comprobando que, si el objeto real es un `Artillero`, solicite el nÃºmero de cohetes que tiene y los imprima.

### Respuesta
Sí, en Java se puede tener una referencia del supertipo (Soldado) que apunte a objetos reales de un subtipo (Artillero, Zapador). Esto es lo habitual en herencia y permite tratar objetos distintos de forma uniforme. Sin embargo, con una referencia de tipo Soldado solo se pueden invocar métodos definidos en Soldado, aunque el objeto real sea más específico.

El upcasting consiste en tratar un objeto de una subclase como si fuera de la superclase (por ejemplo, guardar un Artillero en una variable Soldado). Es automático y seguro. El downcasting es lo contrario: convertir una referencia de superclase a subclase. Este sí requiere comprobación, porque no todos los Soldado son Artillero. Para eso se usa instanceof, que permite verificar el tipo real del objeto antes de hacer el cast.

public class Main {
    public static void main(String[] args) {
        Soldado[] ejercito = {
            new Artillero("Carlos", 5),
            new Zapador("Luis", 3),
            new Artillero("Ana", 2)
        };

        for (Soldado s : ejercito) {
            s.saludar();

            if (s instanceof Artillero) {
                Artillero a = (Artillero) s; // downcasting
                System.out.println("Cohetes: " + a.getNumCohetes());
            }
        }
    }
}

En este ejemplo, el array es de tipo Soldado (upcasting), pero mediante instanceof se detecta si el objeto real es un Artillero y se hace downcasting para acceder a su método específico.


## 6. Respecto a la ocultaciÃ³n de informaciÃ³n y herencia, Â¿quÃ© significa acceso **"protegido"** de mÃ©todos y/o atributos? Â¿CÃ³mo se implementa en Java? Pon un ejemplo de uso de en la clase `Soldado` para que su nombre sea protegido y pueda usarse en el mÃ©todo de poner bombas del `Zapador`.

### Respuesta
El acceso protegido (protected) permite que un atributo o método sea accesible dentro de su propia clase y también desde sus subclases, aunque estén en otros paquetes. Es un nivel intermedio entre private (solo accesible en la propia clase) y public (accesible desde cualquier sitio). Se utiliza cuando se quiere permitir que las subclases reutilicen directamente ciertos datos o comportamientos.

En Java se implementa usando la palabra clave protected. A diferencia de private, los atributos protegidos sí pueden ser usados directamente en las subclases. Esto facilita extender la funcionalidad sin necesidad de getters, aunque debe usarse con cuidado para no romper la encapsulación.

class Soldado {
    protected String nombre; // ahora accesible en subclases

    public Soldado(String nombre) {
        this.nombre = nombre;
    }

    public void saludar() {
        System.out.println("Hola, soy " + nombre);
    }
}

class Zapador extends Soldado {
    private int numMinas;

    public Zapador(String nombre, int numMinas) {
        super(nombre);
        this.numMinas = numMinas;
    }

    public void ponerMinas() {
        System.out.println(nombre + " está poniendo minas");
    }
}

En este ejemplo, nombre es protected, por lo que Zapador puede usarlo directamente en su método ponerMinas(). Esto no sería posible si fuera private, donde solo podría accederse mediante métodos públicos o protegidos.


## 7. En los lenguajes orientados a objetos Â¿hay una **clase base** para todos los objetos? Â¿Ocurre en todos los lenguajes? Â¿QuÃ© ocurre en Java?

### Respuesta
En muchos lenguajes orientados a objetos existe una clase base común de la que heredan todas las demás clases, pero no ocurre en todos los lenguajes. Depende del diseño del lenguaje: algunos lo imponen (como Java) y otros no tienen una jerarquía única obligatoria.

En Java, sí existe una clase base para todos los objetos, llamada Object. Todas las clases heredan directa o indirectamente de Object, incluso aunque no se indique explícitamente con extends. Esto significa que cualquier objeto en Java comparte ciertos métodos comunes definidos en Object.

Por ejemplo, métodos como toString(), equals() o hashCode() están disponibles en cualquier objeto. Esto permite tratar todos los objetos de forma uniforme en ciertos contextos, ya que todos comparten una misma base en la jerarquía de herencia.


## 8. Â¿QuÃ© es la **"herencia mÃºltiple"**? Â¿Existe en Java herencia mÃºltiple?

### Respuesta
La herencia múltiple ocurre cuando una clase puede heredar de más de una superclase al mismo tiempo, recibiendo atributos y métodos de todas ellas. Esto puede generar conflictos si varias superclases tienen miembros con el mismo nombre, por lo que no todos los lenguajes la permiten.

En Java no existe herencia múltiple de clases. Una clase solo puede extender de una única superclase. Sin embargo, Java permite que una clase implemente varias interfaces, lo que proporciona un mecanismo similar para compartir comportamientos sin heredar estado, evitando los problemas típicos de la herencia múltiple.


## 9. Las excepciones en los lenguajes orientados a objetos son objetos. Por tanto, se pueden crear excepciones personalizadas. Pon un ejemplo en Java de una excepciÃ³n personalizada (`UsuarioNoEncontradoException`), que sea *no controlada* y que ademÃ¡s este compuesto con un `Usuario`, para saber quÃ© `Usuario` dio el problema. Permite ademÃ¡s que se pueda incluir la causa, es decir, sobrecarga el constructor para tener una versiÃ³n que permita aÃ±adir la causa subyacente. 

### Respuesta


## 10. Herencia vs. ComposiciÃ³n. Se dice que no se debe emplear herencia simplemente por reutilizar cÃ³digo, es decir, que si quiero reutilizar cÃ³digo simplemente, no debo pensar en herencia como primera opciÃ³n Â¿por quÃ©?

### Respuesta


## 11. Herencia vs. ComposiciÃ³n. Se dice que se debe *"favorecer la composiciÃ³n frente a la herencia"*, Â¿por quÃ©?

### Respuesta


## 12. Herencia vs. ComposiciÃ³n. Se dice que la *"herencia rompe la encapsulaciÃ³n"*, Â¿a quÃ© se refiere esto?

### Respuesta


## 13. Pongamos un ejemplo de dos alternativas para lo mismo. Tenemos un `Estudiante` y un `Trabajador`, ambos tienen datos en comÃºn: el DNI y el nombre. Modelemos esto de dos formas: uno por herencia, con una superclase `Persona`, y otro con composiciÃ³n, con una clase `DatosPersonales`. Se debe recibir una instancia de `DatosPersonales` en el constructor de la clase `Estudiante` y `Trabajador`.

### Respuesta
