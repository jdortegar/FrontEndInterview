# Interview Questions Spanish

### 1. Qué es el hoisting?

Hoisting es una característica de JavaScript que empuja todas las declaraciones (no las asignaciones) de variables al inicio de su scope (Al momento de interpretar incialmente el código, previo a su ejecución)
```
function foo() {
	bar();
	var x = 1;
}
```
Es interpretada de la siguiente manera:
```
function foo() {
  var x;
  bar();
  x = 1;
}
```
Lo que se "mueve" hacia arriba es la declaración de la variable, no la asignación de un valor a ella.

En una declaración de función (Function Declaration), son "movidas" tanto su declaración como asignación, no así en una expresión de función (Function Expresion)

Por ejemplo:
```
function ejemploDeHoisting() {
  bar(); // Esto imprimirá "hola"
  foo(); // Esto imprimirá "foo is not a function"
  var foo = function () { // Esto es una `Function Expresion` asignada a la variable Foo.
		alert("Mundo");
	}
	function bar() { // `Function Declaration` con el nombre bar
		alert("Hola");
	}
}
ejemploDeHoisting();
```

### 2. Qué es un closure?

Un closure es una característica que tiene JavaScript de que una función al ejecutarse, recuerde el entorno en la que fue creada. Por ejemplo:
```
function bar() {
  var text = 'mundo';
  function foo() {
    console.log('hola ' + text);
  }
  foo();
}
bar();
```
Esta funcion imprimirá 'hola mundo', sin ningun problema.

Ahora, consideremos lo siguiente:
```
var text = 'fforres';
function bar() {
  var text = 'mundo';
  function foo() {
    console.log('hola ' + text);
  }
  return foo;
}
var willItPrint = bar();
willItPrint();
```
Si bien estamos definiendo en 2 lugares la variable text, al momento de definir la función foo la variable text tiene el valor de 'mundo'. La funcion foo la estamos devolviendo y guardando en la variable willItPrint por lo que independiente de el momento en el que llamemos a la funcion guardada en esa variable, el resultado será:
```
"hola mundo";
```
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
Kyle Simpson es uno de los ponentes más reputados y conocidos de JavaScript, autor de la famosa serie de libros “You don’t know JavaScript!”. Ha sido uno de los ponentes de la pasada edición de JSCamp y, además, de verle allí, en GFT tuvimos la oportunidad de aprender de él, en directo, en un taller que impartió en nuestras oficinas de Sant Cugat. En concreto, sobre “Deep JavaScript Foundation”, en el que nos estuvo hablando acerca de object wrappers, coercion, scope, closure, types, prototype system, características de ES6 features, y mucho más.

### 6. Describir un poco de programación orientada a objetos en JS.

La programación orientada a objetos es un paradigma de programación que utiliza la abstracción para crear modelos basados ​​en el mundo real. Utiliza diversas técnicas de paradigmas previamente establecidas, incluyendo la modularidad, polimorfismo y encapsulamiento. Hoy en día, muchos lenguajes de programación (como Java, JavaScript, C#, C++, Python, PHP, Ruby y Objective-C) soportan programación orientada a objetos (POO).

La programación orientada a objetos puede considerarse como el diseño de software a través de un conjunto de objetos que cooperan, a diferencia de un punto de vista tradicional en el que un programa puede considerarse como un conjunto de funciones, o simplemente como una lista de instrucciones para la computadora. En la programación orientada a objetos, cada objeto es capaz de recibir mensajes, procesar datos y enviar mensajes a otros objetos. Cada objeto puede verse como una pequeña máquina independiente con un papel o responsabilidad definida.

POO pretende promover una mayor flexibilidad y facilidad de mantenimiento en la programación y es muy popular en la ingeniería de software a gran escala. Gracias a su fuerte énfasis en la modularidad, el código orientado a objetos está concebido para ser más fácil de desarrollar y más fácil de entender posteriormente, prestándose a un análisis más directo, a una mayor codificación y comprensión de situaciones y procedimientos complejos que otros métodos de programación menos modulares. 2

### Terminología

**Clase**

Define las características del Objeto.

**Objeto**

Una instancia de una Clase.

**Propiedad**

Una característica del Objeto, como el color.

**Método**

Una capacidad del Objeto, como caminar.

**Constructor**

Es un método llamado en el momento de la creación de instancias.

**Herencia**

Una Clase puede heredar características de otra Clase.

**Encapsulamiento**

Una Clase sólo define las características del Objeto, un Método sólo define cómo se ejecuta el Método.

**Abstracción**

La conjunción de herencia compleja, métodos y propiedades que un objeto debe ser capaz de simular en un modelo de la realidad.

**Polimorfismo**

Diferentes Clases podrían definir el mismo método o propiedad.

### 7. Qué es un patrón de diseño en programación?

Es la base para la búsqueda de soluciones a problemas muy comunes en el desarrollo de aplicativos y otros ámbitos referentes al diseño de interacciones o interfaces.

Se podría resumir de una manera más sencilla como “una manera de resolver una problemática”, un patrón de diseño tiene que cumplir por lo menos con los siguientes objetivos.

* Estandarizar el lenguaje entre desarrolladores.
* Evitar perder tiempo en soluciones a problemas ya resueltos o conocidos.
* Crear código que se pueda reutilizar.

8. Qué patrones de diseño conoces?

* Patrón Object Literals
* Patrón Module
* Patrón Prototype
* Patrón factory de singletons


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
### 22. Se puede (debe) mutar una prop? Por qué?

No! En realidad, es todo lo contrario: la mutabilidad complica las cosas, al less a largo ploop. Sí, hace que su encoding inicial sea más fácil porque puede simplemente cambiar las cosas donde quiera, pero cuando su progtwig crece, se convierte en un problema. Si un valor cambia, ¿qué lo cambió?

Cuando haces que todo sea inmutable, significa que los datos ya no pueden cambiarse por sorpresa. Usted sabe con certeza que si transfiere un valor a una function, no puede modificarse en esa function.

En pocas palabras: si usa valores inmutables, es muy fácil razonar acerca de su código: todos obtienen una copy * única de sus datos, por lo que no pueden utilizarla y romper otras partes de su código. ¡Imagínese lo fácil que es trabajar en un entorno con múltiples subprocesss!

Nota 1: Existe un costo de performance potencial para la inmutabilidad dependiendo de lo que esté haciendo, pero cosas como Immutable.js optimizan lo mejor que pueden.

Nota 2: en el improbable caso de que no estés seguro, Immutable.js y ES6 const significan cosas muy diferentes.

23. Cómo se puede actualizar el State de un componente?
24. Qué precauciones hay que tener al asignar un nuevo State?
### 25. Qué lifecycles son importantes/comunes/principales en un componente?

Mounting — It is at this phase the component is created (your code, and react’s internals) then inserted into the DOM
Updating — A React component “grows”
Unmounting — Final phase
Error Handling — Sometimes code doesn’t run or there’s a bug somewhere

### 26. Qué hay que tener en cuenta cuando se iteran datos para renderizar multiples veces un componente? (Keys)

Las keys ayudan a React a identificar que ítems han cambiado, son agregados, o son eliminados. Las keys deben ser dadas a los elementos dentro del array para darle a los elementos una identidad estable:
```
const numbers = [1, 2, 3, 4, 5];
const listItems = numbers.map((number) =>
  <li key={number.toString()}>
    {number}
  </li>
);
```
La mejor forma de elegir una key es usando un string que identifique únicamente a un elemento de la lista entre sus hermanos. Habitualmente vas a usar IDs de tus datos como key:
```
const todoItems = todos.map((todo) =>
  <li key={todo.id}>
    {todo.text}
  </li>
);
```
Cuando no tengas IDs estables para renderizar, puedes usar el índice del ítem como una key como último recurso:
```
const todoItems = todos.map((todo, index) =>
  // Only do this if items have no stable IDs
  <li key={index}>
    {todo.text}
  </li>
);
```
No recomendamos usar índices para keys si el orden de los ítems puede cambiar. Esto puede impactar negativamente el rendimiento y puede causar problemas con el estado del componente. Revisa el artículo de Robin Pokorny para una explicación en profundidad de los impactos negativos de usar un índice como key. Si eliges no asignar una key explícita a la lista de ítems, React por defecto usará índices como keys.


29. Que es el Virtual DOM?
30. Qué diferencias tiene el Virtual DOM con el DOM del browser?
31. Por qué React usa Virtual DOM?
32. Describir qué es lo que sucede en el Browser DOM cuando se renderiza multiples veces un componente utilizando el “index” del iterador como Key.
33. Ahora describir qué sucede en el Browser DOM cuando se utiliza un valor único como Key.
### 34. De qué otras formas podrías gestionar el estado de la aplicación? Diferencias con patron MVC? (en este caso usaban Redux en el equipo)




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
### 54. Diferencia entre base de datos relacional y no relacional?
**Bases de datos relacionales**

El principio de las bases de datos relacionales se basa en la organización de la información en trozos pequeños, que se relacionan entre ellos mediante la relación de identificadores.

En el ámbito informático se habla mucho de ACID, cuyas siglas vienen de las palabras en inglés: atomicidad, consistencia, aislamiento y durabilidad. Son propiedades que las bases de datos relacionales aportan a los sistemas y les permiten ser más robustos y menos vulnerables ante fallos.

La base de datos relacional más usada y conocida es MySQL junto con Oracle, seguida por SQL Server y PostgreSQL, entre otras.

**Bases de datos no relacionales**

Como su propio nombre indica, las bases de datos no relacionales son las que, a diferencia de las relacionales, no tienen un identificador que sirva de relación entre un conjunto de datos y otros. Como veremos, la información se organiza normalmente mediante documentos y es muy útil cuando no tenemos un esquema exacto de lo que se va a almacenar.

La indiscutible reina del reciente éxito de las bases de datos no relacionales es MongoDB seguida por Redis, Elasticsearch y Cassandra.

### 55. Que son los React Hooks ?

Hooks son funciones que te permiten “enganchar” el estado de React y el ciclo de vida desde componentes funcionales. Los hooks no funcionan dentro de las clases — te permiten usar React sin clases.

Hooks son funciones de JavaScript, pero imponen dos reglas adicionales:

* Solo llamar Hooks en el nivel superior. No llames Hooks dentro de loops, condiciones o funciones anidadas.
* Solo llamar Hooks desde componentes funcionales de React. No llames Hooks desde las funciones regulares de JavaScript. (Solo hay otro lugar válido para llamar Hooks: tus propios Hooks personalizados. En un momento aprenderemos sobre estos).

#### Basic Hooks

* useState
* useEffect
* useContext

#### Additional Hooks

* useReducer
* useCallback
* useMemo
* useRef
* useImperativeHandle
* useLayoutEffect
useDebugValue

### 56. Ques es cors y como se prevenirlo ?

El Intercambio de Recursos de Origen Cruzado (CORS) es un mecanismo que utiliza cabeceras HTTP adicionales para permitir que un user agent obtenga permiso para acceder a recursos seleccionados desde un servidor, en un origen distinto (dominio) al que pertenece. Un agente crea una petición HTTP de origen cruzado cuando solicita un recurso desde un dominio distinto, un protocolo o un puerto diferente al del documento que lo generó.

Para prevernilo hay que hablitar el permiso, en express usar cors dependency

### 57. Async Functions

ES5 callback-hell

```
function AsyncTask() {
   asyncFuncA(function(err, resultA){
      if(err) return cb(err);

      asyncFuncB(function(err, resultB){
         if(err) return cb(err);

          asyncFuncC(function(err, resultC){
               if(err) return cb(err);

               // And so it goes....
          });
      });
   });
}
```

ES6 Promises

```
function asyncTask(cb) {

   asyncFuncA.then(AsyncFuncB)
      .then(AsyncFuncC)
      .then(AsyncFuncD)
      .then(data => cb(null, data)
      .catch(err => cb(err));
}
```

ES7 Async/await
```
async function asyncTask(cb) {
    try {
       const user = await UserModel.findById(1);
       if(!user) return cb('No user found');
    } catch(e) {
        return cb('Unexpected error occurred');
    }

    try {
       const savedTask = await TaskModel({userId: user.id, name: 'Demo Task'});
    } catch(e) {
        return cb('Error occurred while saving task');
    }

    if(user.notificationsEnabled) {
        try {
            await NotificationService.sendNotification(user.id, 'Task Created');  
        } catch(e) {
            return cb('Error while sending notification');
        }
    }

    if(savedTask.assignedUser.id !== user.id) {
        try {
            await NotificationService.sendNotification(savedTask.assignedUser.id, 'Task was created for you');
        } catch(e) {
            return cb('Error while sending notification');
        }
    }

    cb(null, savedTask);
}
```


