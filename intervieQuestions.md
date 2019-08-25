# Interview Questions Spanish

### 1. Qué es el hoisting?
### 2. Qué es un closure?
### 3. Cuál es la diferencia entre una variable: null, undefined y no declarada?

undefined: Como JavaScript es un lenguaje de programación débilmente tipado nos permite hacer cosas muy flexibles como por ejemplo declarar una variable sin especificar su tipo. En términos prácticos sería declarar una variable sin valor. (Cabe destacar que JS en tiempo de ejecución asigna el tipo de variable dependiendo del valor que esta tenga)

Ejemplo:
```
var a = 123; // El valor que contiene es un numero por ende JavaScript cataloga a la variable "a" de type Number.
var b; // La variable "b" fue declarada pero no fue definido ningún valor en ella, por ende es de caracter undefined.
```
En resumen, si declaras una variable en JS y no le asignas valor alguno, por defecto es una variable undefined.

null: Representa la ausencia de contenido. Esto quiere decir que en sí mismo null es un valor el cual no tiene contenido. Por otra parte el intérprete de JS a las variables null le asigna el tipo de variable Object. Este es un comportamiento extraño en el que puedes ver una explicación más detallada en el libro de Nicholas C. Zakas "THE PRINCIPLES OF OBJECT-ORIENTED JAVASCRIPT". Aquí un pequeño extracto del libro donde explica un poco este comportamiento:

When you run typeof null, the result is "object". But why an object when the type is null? (In fact, this has been acknowledged as an error by TC39, the committee that designs and maintains JavaScript.

no declarada: Como la expresión lo dice, son variables que no han sido declaradas con la palabra reservada var, (en ES6 también podemos declarar variables con let y const). Si queremos guardar el resultado de una operación en una variable no declarada, JavaScript crea una variable global con el identificador no declarado (nombre de la variable) y le asigna el valor de la operación

Ejemplo:
```
number = 3 + 6; // La variable number no ha sido declarada y por lo que JavaScript crea la variable global `number` y le asigna el resultado de la operación.
```
Por otra parte si solo queremos acceder a una variable no declarada sin pasarle ningún valor nuestro código fallara, ya que JavaScript no tiene conocimiento de dicha variable. Puedes hacer la prueba abriendo tu consola del navegador, escribir una palabra y darle enter; Deberías ver un mensaje como: Uncaught ReferenceError: variable_no_declarada is not defined

### 4. Qué es y para qué sirve THIS? (la mejor explicación la leí en You Don’t Know JS — Kyle Simpson)

La palabra reservada `this` hace referencia al contexto de ejecución actual, y en la mayoría de los casos, su valor es determinado dependiendo de como se llamó a la función en que se declaró. Existen una serie de factores que cambian el comportamiento de `this` en javascript
Modo estricto

En modo estricto (usando 'use strict'), el valor de this es por defecto undefined, esto debido a razones de performance y seguridad, aunque el valor de this aún puede modificarse usando bind, call o apply. Este no es el caso para el modo no estricto. Por ejemplo

```
function f1(){
    return this;
}
// En el browser
f1() === window; // En modo estricto, esto retorna false 
```  
**this en objetos**

Cuando se usa this en el método de un objeto, su valor hace referencia al objeto en que es invocado, independiente del contexto en que se declara el método. Por ejemplo,
```
var o = {p: 37};

function fn() {
  return this.p;
}

o.f = fn;

console.log(o.f()); // 37
```
**bind, call y apply** 

El valor de this puede ser manualmente modificado al momento de ejecutar una función, usando los métodos mencionados. call y apply funcionan de forma similar, llaman a una función pasando como parametro el valor de this de forma explicita
```
function add(c, d){
  return this.a + this.b + c + d;
}

var o = {a:1, b:3};

add.call(o, 5, 7); // 1 + 3 + 5 + 7 = 16

add.apply(o, [10, 20]); // 1 + 3 + 10 + 20 = 34
```
Por otro lado, bind asigna un valor al this de una función de forma permanente a una nueva función
```
var add2 = add.bind({a:1, b:3})
add2(1, 2) // 1 + 3 + 1 + 2 = 7
```
**arrow functions**

Las funciones de flecha asignan el valor de this al contexto 'padre' del contexto de ejecución. Independiente de si son llamadas directamente, o como método de un objeto, tampoco se puede cambiar el valor de this con las funciones bind, call y apply.

### 5. Sabes quién es Kyle Simpson
6. Describir un poco de programación orientada a objetos en JS.
7. Qué es un patrón de diseño en programación?
8. Qué patrones de diseño conoces?
9. Que es una Class?
10. Por qué se pueden usar Class en ES6+?
11. Que es Functional Programming (FP)?
12. Para que sirve o con qué propósito se usa el FP?
13. Explicar qué es React a una persona que no sabe nada de programación.
14. Ahora explicar con términos más técnicos qué es React.
15. Qué tipos de componentes existen en React?
16. Usaste alguna librería de componentes para React? Cuáles? (les recomiendo ant.design)
17. Qué significa que un componente sea Stateless?
18. Qué diferencia hay entre un componente Statefull y Stateless?
19. Qué es el State de un componente?
20. Qué es una Prop?
21. Qué diferencia hay entre State y Props?
22. Se puede (debe) mutar una prop? Por qué?
23. Cómo se puede actualizar el State de un componente?
24. Qué precauciones hay que tener al asignar un nuevo State?
25. Qué lifecycles son importantes/comunes/principales en un componente?
26. Qué hay que tener en cuenta cuando se iteran datos para renderizar multiples veces un componente? (la Key)
27. Qué precauciones hay que tener con la Key?
28. Por qué debe ser única?
29. Que es el Virtual DOM?
30. Qué diferencias tiene el Virtual DOM con el DOM del browser?
31. Por qué React usa Virtual DOM?
32. Describir qué es lo que sucede en el Browser DOM cuando se renderiza multiples veces un componente utilizando el “index” del iterador como Key.
33. Ahora describir qué sucede en el Browser DOM cuando se utiliza un valor único como Key.
34. De qué otras formas podrías gestionar el estado de la aplicación? Diferencias con patron MVC? (en este caso usaban Redux en el equipo)
35. Como se construye un Store en React-Redux?
36. Por qué decimos que en Redux importa la inmutabilidad?
37. Por qué una prop debe ser inmutable?
38. Qué es un High Order Component (HOC)?
39. Nombra alguno. (Connect de Redux)
40. Usaste algún middleware en Redux? Cuál?
41. Para qué sirven?
42. Usaste alguna vez Redux Saga?
43. Usaste alguna vez Re-Ducks?
44. Qué tipos de test existen?
45. En que consiste un test unitario?
46. Qué es el coverage?
47. Qué aspectos son cruciales para el coverage?
48. Qué usaste para hacer tests?
49. Usaste JEST y Enzyme?
50. Cómo haces refactoring de un código?
51. Cómo haces code reviews?
52. Cómo mantenés un código límpio?
53. Usaste Jira o similares?
