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
Las cuatro características básicas de la programación orientada a objetos son abstracción, encapsulación, herencia y polimorfismo. Estas características permiten organizar el código de forma más estructurada, facilitando su reutilización, mantenimiento y comprensión, especialmente en programas de gran tamaño.

La abstracción consiste en identificar las características y comportamientos relevantes de un elemento del mundo real y representarlos en el programa, ignorando los detalles innecesarios. En lugar de centrarse en cómo se implementa algo internamente, se pone el foco en qué hace. Esto permite trabajar con conceptos de alto nivel, de forma similar a cómo en C se usan funciones para ocultar la implementación de ciertas operaciones.

La encapsulación implica agrupar datos y las operaciones que los manipulan dentro de una misma unidad, llamada objeto, y controlar el acceso a dichos datos. Normalmente, los atributos de un objeto no se acceden directamente desde el exterior, sino a través de métodos. Esto evita usos incorrectos y dependencias innecesarias, mejorando la seguridad y el mantenimiento del código.

La herencia permite crear nuevas clases a partir de otras existentes, reutilizando sus atributos y métodos, mientras que el polimorfismo permite tratar objetos de diferentes clases relacionadas de manera uniforme. Gracias al polimorfismo, una misma operación puede comportarse de forma distinta según el objeto concreto que la ejecute, lo que aporta flexibilidad y extensibilidad al diseño del programa.

## 2. Cita cuatro lenguajes populares que permitan la programaciÃ³n orientada a objetos

### Respuesta
Existen numerosos lenguajes de programación que soportan la programación orientada a objetos, tanto de forma nativa como combinada con otros paradigmas. Estos lenguajes permiten definir clases, crear objetos y aplicar conceptos como encapsulación, herencia y polimorfismo.

Entre los lenguajes más populares se encuentra Java, que está diseñado específicamente bajo el paradigma orientado a objetos y en el que prácticamente todo se organiza en torno a clases y objetos. También destaca C++, que extiende el lenguaje C añadiendo soporte para orientación a objetos, permitiendo combinar programación procedural y orientada a objetos en un mismo programa.

Otro lenguaje ampliamente utilizado es Python, que soporta orientación a objetos de forma flexible y sencilla, y donde incluso los tipos básicos se tratan como objetos. Por último, C# es un lenguaje moderno orientado a objetos desarrollado por Microsoft, muy usado en el desarrollo de aplicaciones de escritorio, web y videojuegos, especialmente dentro del entorno .NET.

## 3. Los paradigmas anteriores a la POO, Â¿QuÃ© es la **programaciÃ³n estructurada**? y, todavÃ­a mejor, Â¿QuÃ© es la **programaciÃ³n modular**?

### Respuesta
La programación estructurada es un paradigma que propone organizar el código usando estructuras de control bien definidas, evitando saltos incontrolados como goto. Se basa principalmente en tres construcciones básicas: secuencia, selección (condicionales) e iteración (bucles). Este enfoque mejora la legibilidad y facilita el razonamiento sobre el flujo del programa, algo especialmente relevante frente a estilos de programación más antiguos y caóticos.

En lenguajes como C, la programación estructurada se apoya en el uso de funciones para dividir un programa en partes más pequeñas y comprensibles. Cada función realiza una tarea concreta y se invoca cuando es necesario, lo que permite reutilizar código y reducir duplicaciones. Sin embargo, los datos suelen ser globales o se pasan explícitamente entre funciones, lo que puede generar dependencias fuertes y dificultar el mantenimiento en programas grandes.

La programación modular va un paso más allá y se centra en dividir el programa en módulos independientes, cada uno con una responsabilidad clara. Un módulo agrupa funciones y datos relacionados, y define una interfaz pública a través de la cual otros módulos pueden interactuar con él. En C, este enfoque se refleja en el uso de archivos .h y .c, donde se separa la declaración de la implementación.

La principal ventaja de la programación modular es que reduce el acoplamiento entre distintas partes del programa y mejora la escalabilidad del software. Aunque no es orientación a objetos, comparte con ella la idea de ocultar detalles internos y exponer solo lo necesario, sirviendo como base conceptual para entender posteriormente conceptos como encapsulación y abstracción en la POO.

## 4. Â¿QuÃ© tres elementos definen a un objeto en programaciÃ³n orientada a objetos?

### Respuesta
En programación orientada a objetos, un objeto se define a partir de tres elementos fundamentales: identidad, estado y comportamiento. Estos elementos permiten distinguir un objeto de otro, describir su situación en un momento dado y especificar qué acciones puede realizar.

La identidad es lo que diferencia a un objeto de cualquier otro, incluso aunque tengan el mismo estado y comportamiento. Dos objetos pueden representar el mismo concepto y contener los mismos valores en sus atributos, pero siguen siendo entidades distintas en memoria. Este concepto no suele ser explícito en lenguajes procedurales como C, donde se trabaja más directamente con direcciones de memoria y estructuras de datos.

El estado de un objeto está formado por el conjunto de datos que almacena, normalmente mediante atributos o campos. Estos datos representan la información interna del objeto y pueden cambiar a lo largo del tiempo. Desde una perspectiva similar a C, el estado podría compararse con una struct, aunque en la orientación a objetos el acceso a estos datos suele estar controlado.

El comportamiento se refiere a las operaciones que el objeto puede realizar, definidas mediante métodos. Estos métodos pueden consultar o modificar el estado interno del objeto y representan las acciones asociadas a él. A diferencia de la programación estructurada, donde las funciones están separadas de los datos, en la POO ambos conceptos se agrupan dentro del propio objeto.

## 5. Â¿QuÃ© es una clase? Â¿Es lo mismo que un objeto? Â¿QuÃ© es una instancia? Â¿Todos los lenguajes orientados a objetos manejan el concepto de clase?

### Respuesta


## 6. Â¿DÃ³nde se almacenan en memoria los objetos? Â¿Es igual en todos los lenguajes? Â¿QuÃ© es la **recolecciÃ³n de basura**? 

### Respuesta


## 7. Â¿QuÃ© es un mÃ©todo? Â¿QuÃ© es la **sobrecarga de mÃ©todos**? 

### Respuesta


## 8. Ejemplo mÃ­nimo de clase en Java, que se llame Punto, con dos atributos, x e y, con un mÃ©todo que se llame `calculaDistanciaAOrigen`, que calcule la distancia a la posiciÃ³n 0,0. Por sencillez, los atributos deben tener visibilidad por defecto. Crea ademÃ¡s un ejemplo de uso con una instancia y uso del mÃ©todo

### Respuesta


## 9. Â¿CuÃ¡l es el punto de entrada en un programa en Java? Â¿QuÃ© es `static` y para quÃ© vale? Â¿SÃ³lo se emplea para ese mÃ©todo `main`? Â¿Para quÃ© se combina con `final`?

### Respuesta

## 10. Intenta ejecutar un poco de Java de forma bÃ¡sica, con los comandos `javac` y `java`. Â¿CÃ³mo podemos compilar el programa y ejecutarlo desde linea de comandos? Â¿Java es compilado? Â¿QuÃ© es la **mÃ¡quina virtual**? Â¿QuÃ© es el *byte-code* y los ficheros `.class`?

### Respuesta


## 11. En el cÃ³digo anterior de la clase `Punto` Â¿QuÃ© es `new`? Â¿QuÃ© es un **constructor**? Pon un ejemplo de constructor en una clase `Empleado` que tenga DNI, nombre y apellidos

### Respuesta


## 12. Â¿QuÃ© es la referencia `this`? Â¿Se llama igual en todos los lenguajes? Pon un ejemplo del uso de `this` en la clase `Punto`

### Respuesta


## 13. AÃ±ade ahora otro nuevo mÃ©todo que se llame `distanciaA`, que reciba un `Punto` como parÃ¡metro y calcule la distancia entre `this` y el punto proporcionado

### Respuesta


## 14. El paso del `Punto` como parÃ¡metro a un mÃ©todo, es **por copia** o **por referencia**, es decir, si se cambia el valor de algÃºn atributo del punto pasado como parÃ¡metro, dichos cambios afectan al objeto fuera del mÃ©todo? Â¿QuÃ© ocurre si en vez de un `Punto`, se recibiese un entero (`int`) y dicho entero se modificase dentro de la funciÃ³n? 

### Respuesta


## 15. Â¿QuÃ© es el mÃ©todo `toString()` en Java? Â¿Existe en otros lenguajes? Pon un ejemplo de `toString()` en la clase `Punto` en Java

### Respuesta


## 16. Reflexiona: Â¿una clase es como un `struct` en C? Â¿QuÃ© le falta al `struct` para ser como una clase y las variables de ese tipo ser instancias?


### Respuesta


## 17. Quitemos un poco de magia a todo esto: Â¿Como se podrÃ­a â€œemularâ€, con `struct` en C, la clase `Punto`, con su funciÃ³n para calcular la distancia al origen? Â¿QuÃ© ha pasado con `this`?

### Respuesta
