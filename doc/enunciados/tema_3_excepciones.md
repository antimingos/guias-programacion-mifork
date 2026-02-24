<!--
Posible prompt:
<prompt>
Tengo un cuestionario con preguntas sobre "Excepciones". Debes tener en cuenta que los conocimientos previos que tengo (y por tanto tus respuestas deben ser adaptadas), son:
- C/C++ sin orientaci√≥n a objetos.
- Temas de Java previos: Clases y Objetos, Encapsulaci√≥n.

Cada respuesta debe tener entre 2 - 4 p√°rrafos de longitud (sin contar los trozos de c√≥digo).

Por favor, escribe en impersonal las respuestas.

</prompt>
----
-->
# TEMA 3. Excepciones

## 1. Empecemos un tema sobre control de errores en lenguajes de programaci√≥n, con algo b√°sico. En C, donde no existen las excepciones, pongamos un ejemplo de una ra√≠z que toma n√∫mero flotante positivo. Queremos controlar el error si la funci√≥n recibe un n√∫mero negativo. El usuario debe ser informado pero desde fuera de la funci√≥n `raiz` ¬øC√≥mo indicamos ese error?. Enumera dos opciones diferentes de dise√±ar, poniendo un ejemplo de c√≥digo de cada una.

### Respuesta

? OPCI”N 1: Usar el valor de retorno para indicar error

Es la forma m·s simple y com˙n en C.

La funciÛn devuelve un valor especial que indica que ocurriÛ un error.
Por ejemplo: -1 (si sabemos que nunca deberÌa ser negativo el resultado).

?? Idea

Si el n˙mero es negativo ? devolvemos -1

El usuario de la funciÛn debe comprobar el valor devuelto

?? Ejemplo
#include <stdio.h>
#include <math.h>

float raiz(float x) {
    if (x < 0) {
        return -1;  // valor especial que indica error
    }
    return sqrt(x);
}

int main() {
    float resultado = raiz(-4);

    if (resultado == -1) {
        printf("Error: no se puede calcular la raiz de un numero negativo\n");
    } else {
        printf("Resultado: %f\n", resultado);
    }

    return 0;
}
? Problema de este diseÒo

øQuÈ pasa si el valor -1 fuera un resultado v·lido?
No podemos distinguir entre error y resultado real.

? OPCI”N 2: Usar un par·metro adicional para indicar error

AquÌ separamos:

El valor de retorno ? resultado

Un par·metro adicional ? indica si hubo error

Esto es m·s robusto.

?? Idea

Pasamos un puntero a una variable int error

La funciÛn escribe en esa variable

?? Ejemplo
#include <stdio.h>
#include <math.h>

float raiz(float x, int *error) {
    if (x < 0) {
        *error = 1;  // indicamos error
        return 0;    // valor irrelevante
    }

    *error = 0;      // no hay error
    return sqrt(x);
}

int main() {
    int error;
    float resultado = raiz(-4, &error);

    if (error) {
        printf("Error: numero negativo\n");
    } else {
        printf("Resultado: %f\n", resultado);
    }

    return 0;
}
? Ventajas

No dependemos de un valor m·gico como -1

SeparaciÛn clara entre resultado y estado del error


## 2. Brevemente ¬øQu√© es una **"excepci√≥n"**? ¬øCon qu√© objetivo las usa un programador cuando implementa funciones o cuando las llama?

### Respuesta
? øQuÈ es una excepciÛn?

Una excepciÛn es un mecanismo para indicar que ha ocurrido un error o situaciÛn anormal durante la ejecuciÛn de un programa.

En lugar de devolver un valor especial (como en C), el programa interrumpe el flujo normal y envÌa un aviso de error.

? øCon quÈ objetivo se usan?

Un programador las usa para:

?? Separar el cÛdigo normal del cÛdigo de error

?? Obligar a quien llama a la funciÛn a tratar el error

?? Evitar que el programa contin˙e con datos incorrectos

En resumen: permiten un control de errores m·s seguro y organizado que en C.


## 3. Reescribe el mismo ejemplo de raiz, pero en Java, metiendo ese m√©todo en una clase `Calculadora` y llama a dicho m√©todo desde el m√©todo `main`, mostrando c√≥mo se puede controlar desde fuera.

### Respuesta
? Ejemplo en Java usando excepciones

Creamos una clase Calculadora con el mÈtodo raiz.
Si el n˙mero es negativo, lanzamos una excepciÛn.

class Calculadora {

    public static double raiz(double x) {
        if (x < 0) {
            throw new IllegalArgumentException("Numero negativo no permitido");
        }
        return Math.sqrt(x);
    }
}

public class Main {
    public static void main(String[] args) {

        try {
            double r = Calculadora.raiz(-5);
            System.out.println("Resultado: " + r);
        } catch (IllegalArgumentException e) {
            System.out.println("Error: " + e.getMessage());
        }

    }
}
?? Idea clave

throw ? lanza la excepciÛn.

try-catch ? permite controlarla desde fuera.

Si ocurre error, el flujo normal se interrumpe y pasa al catch.


## 4. ¬øQu√© es **"lanzar"** una excepci√≥n? ¬øQu√© es **"controlar"** o **"capturar"** una excepci√≥n? ¬øQu√© es que se **"propague"** una excepci√≥n? ¬øQu√© le va ocurriendo a las funciones en la pila de llamadas por donde se va propagando la excepci√≥n? ¬øLas funciones que no la controlan se reanudan despu√©s de alguna forma? Explica con el mismo ejemplo anterior en Java de la ra√≠z cuadrada.

### Respuesta
? Lanzar una excepciÛn

Es provocar el error explÌcitamente usando throw.

En el ejemplo:

if (x < 0) {
    throw new IllegalArgumentException("Numero negativo");
}

AquÌ el mÈtodo raiz lanza la excepciÛn.

? Capturar (controlar) una excepciÛn

Es manejar el error usando try-catch.

try {
    Calculadora.raiz(-5);
} catch (IllegalArgumentException e) {
    System.out.println("Error controlado");
}

AquÌ el catch la captura.

? Propagarse una excepciÛn

Si un mÈtodo no la captura, la excepciÛn sube al mÈtodo que lo llamÛ.

Ejemplo:

main ? llama a raiz()
raiz() lanza excepciÛn
main la captura

Si main tampoco la capturara ? el programa termina con error.

? øQuÈ pasa en la pila de llamadas?

Cuando se lanza la excepciÛn:

Se interrumpe el mÈtodo actual.

Se eliminan de la pila los mÈtodos que no la capturan.

Se busca un catch hacia arriba.

? øLas funciones que no la controlan contin˙an?

No.

Si un mÈtodo no la captura:

Se termina inmediatamente.

No contin˙a despuÈs de la llamada.

No se reanuda.

Es como si ìsaltaraî directamente al catch.


## 5. ¬øQu√© ventajas tiene frente a C, la **"propagaci√≥n natural"** de las excepciones a trav√©s de la pila (*stack*) de llamadas?

### Respuesta
? Ventajas frente a C

En C el error debe comprobarse manualmente en cada funciÛn.
Si olvidamos comprobarlo ? el programa sigue mal.

En Java, la excepciÛn:

?? Se propaga autom·ticamente por la pila.

?? No puede ignorarse ìsin quererî.

?? Separa claramente cÛdigo normal y cÛdigo de error.

?? Permite capturar el error en un nivel superior (m·s adecuado).

?? En resumen

En C ? el programador debe pasar y revisar el error en cada llamada.
En Java ? el error sube solo hasta que alguien lo capture o el programa termine.

Es m·s seguro y m·s limpio.


## 6. En orientaci√≥n a objetos, ¬ølas excepciones suelen ser objetos? ¬øQu√© ventajas tiene esto en t√©rminos de encapsulaci√≥n? ¬øPodemos entonces crear excepciones personalizadas?

### Respuesta
? øLas excepciones son objetos?

SÌ.
En Java, una excepciÛn es un objeto (una instancia de una clase).

? Ventajas (encapsulaciÛn)

Como es un objeto:

?? Puede guardar informaciÛn del error (mensaje, cÛdigo, datosÖ).

?? El detalle del error queda encapsulado dentro del objeto.

?? Solo accedemos a esa informaciÛn mediante mÈtodos (ej. getMessage()).

? øPodemos crear excepciones personalizadas?

SÌ.

Podemos crear nuestra propia clase de excepciÛn para representar errores especÌficos de nuestra aplicaciÛn.

? Esto permite definir errores m·s claros y organizados.


## 7. En relaci√≥n con las ventajas de la encapsulaci√≥n, comparando el ejemplo en C con Java. ¬øQu√© **informaci√≥n esencial** lleva cualquier **objeto excepci√≥n** que es muy √∫til tener cuando se llega a un manejador?

### Respuesta
? InformaciÛn esencial que lleva una excepciÛn (Java)

Comparado con C (donde solo devolvemos un n˙mero o cÛdigo), en Java el objeto excepciÛn incluye autom·ticamente:

?? Mensaje descriptivo del error (getMessage()).

?? Tipo de excepciÛn (quÈ clase de error es).

?? Pila de llamadas (stack trace) ? dÛnde ocurriÛ y cÛmo se llegÛ ahÌ.

?? Lo m·s importante

La stack trace es clave:
Permite saber exactamente en quÈ mÈtodo y lÌnea ocurriÛ el error, cosa que en C hay que investigar manualmente.

Esto hace el diagnÛstico mucho m·s f·cil y seguro.


## 8. En Java, sobre el bloque **"try-catch"**, ¬øse pueden tener m√°s de un bloque `catch`? ¬øcu√°ntos bloques `catch` se ejecutan?

### Respuesta
? Respuesta

SÌ, un try puede tener varios catch para distintos tipos de excepciÛn.

Solo se ejecuta uno, el primero que coincida con la excepciÛn lanzada.


## 9. Si las excepciones producen rupturas en el c√≥digo llamador, ¬øc√≥mo podemos garantizar que se ejecuta siempre finalmente un c√≥digo necesario para cierre de ficheros, liberacion de recursos, antes de que contin√∫e propag√°ndose la excepci√≥n? Pon un ejemplo en Java con `finally`, tanto con `catch` como sin √©l.

### Respuesta
? Garantizar cÛdigo de limpieza: finally

El bloque finally siempre se ejecuta, aunque haya excepciÛn, con o sin catch.
Se usa para liberar recursos (archivos, conexiones, memoriaÖ).

?? Ejemplo con catch
try {
    double r = Calculadora.raiz(-5);
    System.out.println(r);
} catch (IllegalArgumentException e) {
    System.out.println("Error: " + e.getMessage());
} finally {
    System.out.println("Se cierra recurso o archivo");
}
?? Ejemplo sin catch
try {
    double r = Calculadora.raiz(-5);
    System.out.println(r);
} finally {
    System.out.println("Se cierra recurso o archivo");
}

En ambos casos, el mensaje del finally siempre se imprime, incluso si la excepciÛn sigue propag·ndose.


## 10. En Java, el bloque `finally` puede ir sin `catch`? ¬øSe ejecuta siempre tanto si ocurre como si no ocurre una excepci√≥n? ¬øY si hay un `return` en medio del `try`?

### Respuesta
? Respuesta

SÌ, un bloque finally puede ir solo con try, sin catch.

Se ejecuta siempre, tanto si hay excepciÛn como si no.

Incluso si hay un return dentro del try, el finally se ejecuta antes de salir del mÈtodo.


## 11. En Java, qu√© son las excepciones **"controladas"** y las **"no controladas"**? ¬øQu√© papel juega `RuntimeException`? Pon un ejemplo de excepciones t√≠picas controladas y no controladas que incluso nosotros mismos podr√≠amos usar. Haz dos listas con 3 o 4 ejemplos de situaci√≥n donde se suele preferir una excepci√≥n controlada y donde se suele preferir una excepci√≥n no controlada.

### Respuesta


## 12. ¬øQu√© es y para qu√© se usa `throws`? ¬øPor qu√© es alternativa a capturar una excepci√≥n controlada?

### Respuesta


## 13. Pon un ejemplo en Java de firma de m√©todo que incluya `throws`, de una funci√≥n que abre un fichero pero que declara que no le interesa menejar la excepci√≥n de si el fichero no existe, sino que se propague hacia arriba. Eso s√≠, acu√©rdate del `finally`.

### Respuesta


## 14. ¬øPodemos poner en `throws` excepciones no controladas, como `RuntimeException`? ¬øDeber√≠a el m√©todo llamador entonces poner `try-catch` en ese caso? ¬øQu√© sentido tendr√≠a?

### Respuesta


## 15. ¬øCu√°ndo se recomienda usar excepciones controladas, como `IOException`, y cu√°ndo no controladas como `IllegalArgumentException`? ¬øExisten en todos los lenguajes ambas opciones? En los que s√≥lo existe una opci√≥n, ¬øcu√°l es la m√°s habitual?

### Respuesta


## 16. ¬øTiene sentido lanzar excepciones dentro del `catch`? ¬øSe puede relanzar la misma excepci√≥n capturada? ¬øCu√°ndo tendr√≠a sentido hacer esto √∫ltimo? Pon ejemplos de ambos casos.

### Respuesta


## 17. ¬øEn qu√© consiste que una excepci√≥n sea la **"causa"** de otra excepci√≥n? Pon un ejemplo en Java, donde capturemos una excepci√≥n de bajo nivel y la encapsulemos en otra personalizada de alto nivel. Cuando una excepci√≥n sale por pantalla y tiene una causa, ¬øse ve?

### Respuesta

