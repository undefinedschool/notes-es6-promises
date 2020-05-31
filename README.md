# ![Notas de ES6: Promises](https://i.imgur.com/8b9NlbD.png)


<div align="center">  
  <p align="center">
  <sub>Hola! Soy Nico (<strong>nhsz</strong>), <strong>Dev Full Stack JavaScript y mentor</strong>.</sub>
  </p>
  
  <p align="center">
    <sub>
      Hace un tiempo (principios de 2019) empecé un proyecto llamado <a href="https://undefinedschool.io"><strong>undefined school</strong></a>, una <strong>escuela de Desarrollo Web Full Stack JavaScript</strong>, 100% Open Source, con mentorías personalizadas para grupos reducidos y el foco puesto en los <strong>fundamentos</strong> y <strong>conceptos avanzados</strong>.
    </sub>
  </p>

  <p align="center">
    <sub>
      Me interesa mucho la intersección entre la educación y la tecnología, por eso también participo en proyectos como <a href="https://freecodecampba.org">freeCodeCampBA</a> (co-founder y co-organizador) y <a href="https://twitter.com/LXBA_">Learning Experience BA</a> (co-founder y co-organizador).
    </sub>
  </p>

 <p align="center">
    <sub>
  👉 Si estás arrancando en el mundo del desarrollo web y necesitás una mano, podés encontrarme en <a href="https://twitter.com/_nhsz/">Twitter</a> (también para hablar sobre cualquier tema relacionado a JavaScript o <em>#nerdeadas</em> en general 😛).
  </sub>
  </p>
  
  <p align="center">
  <sub>
    Por último, te cuento que soy muy fan del café (obvio que negro y sin azúcar), asi que si las notas te resultaron útiles y querés colaborar para que no me quede dormido y siga escribiendo guías, apuntes y más <strong>contenido Open Source en español</strong>, podés invitarme uno, gracias! ❤️
  </sub>
  </p>
  
  <p align="center">
  ☕
  <code> 
  <a href="https://cafecito.app/nhsz">
    <strong>Invitame 1 café!</strong>
  </a>
  </code>
  </p>
  <hr>
</div>

👉 Ver [todas las notas](https://github.com/undefinedschool/notes)

## Contenido

- [Intro](https://github.com/undefinedschool/notes-es6-promises#intro)
- [Métodos](https://github.com/undefinedschool/notes-es6-promises#m%C3%A9todos)
- [tl;dr Para qué sirven las Promises?](https://github.com/undefinedschool/notes-es6-promises#tldr-para-qu%C3%A9-sirven-las-promises)
- [Estados de una promesa](https://github.com/undefinedschool/notes-es6-promises#estados-de-una-promesa)
- [Crear promesas](https://github.com/undefinedschool/notes-es6-promises#crear-promesas)
- [Promise Chaining](https://github.com/undefinedschool/notes-es6-promises#promise-chaining)
  - [`.then()`](https://github.com/undefinedschool/notes-es6-promises#then)
- [`Promise.all`](https://github.com/undefinedschool/notes-es6-promises#promiseall)
- [Error handling](https://github.com/undefinedschool/notes-es6-promises#error-handling)
  - [Ejemplo usando _Fetch API_](https://github.com/undefinedschool/notes-es6-promises#ejemplo-usando-fetch-api)
- [Promises, _microtasks_ y el _Event Loop_](https://github.com/undefinedschool/notes-es6-promises#promises-microtasks-y-el-event-loop)
- [Compatibilidad y soporte](https://github.com/undefinedschool/notes-es6-promises#compatibilidad-y-soporte)

---

## Intro

**Una _promesa_ en JavaScript es como una promesa en la vida real: nos comprometemos a hacer algo y esta acción tiene 2 resultados posibles, que se cumpla (_se resuelve exitosamente_) o no (_es rechazada_)**.

> 👉 Mas técnicamente, una _promesa_ es un **objeto** que representa un valor que puede estar disponible en algún momento del futuro, o nunca. Es una _promesa de un valor futuro_. Este valor representa a su vez el resultado exitoso o fracaso de ejecutar una tarea **asincrónica**.

**Vamos a utilizar _promises_ para escribir _código asincrónico_**, es decir, tareas que sabemos no van a tener un resultado inmediato, sino que van a tomar cierto tiempo, por ejemplo hacer un request a una API por medio de `fetch`, descargar una imagen o realizar una consulta a una base de datos. 

👉 La principal ventaja frente a usar _callbacks_ (otra forma que tenemos de manejar asincronismo en JavaScript) es que las _promises_ nos proveen una alternativa para evitar caer en el [_callback hell_](http://callbackhell.com/), a través de una sintaxis más concisa, limpia y fácil de razonar. 

Además, a diferencia de los _callbacks_, **las promesas se pueden _componer_**, utilizando el resultado o _output_ de una como el _input_ de otra.


[↑ Ir al inicio](https://github.com/undefinedschool/notes-es6-promises#contenido)

## Métodos

Al tratarse de un objeto, las promesas tienen una _interfaz_ que nos permite interactuar con estas. 
En particular, vamos a estar estar usando los metodos `.then()` y `.catch()`

👉 Estos métodos nos van a permitir operar con un eventual valor en caso de éxito (el `.then()`), o de falla (el ´catch()´). Esto permite que métodos _asincrónicos_ devuelvan valores como si fueran _sincrónicos_: **en vez de inmediatamente retornar el valor final, _el método asincrónico devuelve una promesa de darnos el valor en algún momento en el futuro_**.

- `then()`: el código dentro se va a ejecutar _sólo si la promesa se resuelva de forma exitosa_
- `catch()`: el código dentro se va a ejecutar en caso de error (_la promesa es rechazada_)
- `all()`: permite ejecutar varias promesas de forma [concurrente](https://www.youtube.com/watch?v=kMr3mF71Kp4)

Los métodos `then()` y `catch()` **devuelven** a su vez **promesas**, **que pueden ser encadenadas**

```js
promise
  .then(...)
  .then(...)
  .then(...)
  .catch(...)
```

**Nota:**

![](https://i.imgur.com/xA4ea9r.png)

[↑ Ir al inicio](https://github.com/undefinedschool/notes-es6-promises#contenido)

## tl;dr Para qué sirven las Promises?

- nos permiten escribir _código asincrónico_ de forma más legible, evitando el [_Callback Hell_](http://callbackhell.com/)
- nos permiten un [mejor manejo de los errores](https://github.com/undefinedschool/notes-es6-promises#error-handling)
- las promesas se pueden _componer_, utilizando el resultado o _output_ de una como el _input_ de otra.

[![JavaScript Promise in 100 Seconds](https://img.youtube.com/vi/RvYYCGs45L4/0.jpg)](https://www.youtube.com/watch?v=RvYYCGs45L4)
> Ver [JavaScript Promise in 100 Seconds](https://www.youtube.com/watch?v=RvYYCGs45L4)

[↑ Ir al inicio](https://github.com/undefinedschool/notes-es6-promises#contenido)

## Estados de una promesa

Una Promesa se encuentra siempre en uno de los siguientes estados:

- pendiente (_pending_): estado inicial de cualquier promesa, no cumplida o rechazada aún
- resuelta (_fulfilled_): significa que la operación se completó exitosamente
- rechazada (_rejected_): significa que la operación falló

[↑ Ir al inicio](https://github.com/undefinedschool/notes-es6-promises#contenido)

## Crear promesas

Cuando creamos una _Promise_ (objeto), le tenemos que pasar una función _callback_ como argumento. Dentro de este _callback_, tenemos 2 parámetros: `resolve()` y `reject()`.

- `resolve()`: cuando el estado de la promesa pasa a estar _resuelto_ (`fullfiled`), se ejecuta el método `resolve()`. Podemos pasar argumentos que serán llevados al _callback_ del `.then()` en el método `resolve()`
- `reject()`: es el método que ejecutamos si consideramos que la promesa _falló_ (o que debe ser _rechazada_). Podemos pasar cualquier mensaje de error como argumento, el cual será tomado en el _callback_ del método `catch()` (que se ejecuta sólo si la promesa falla)

👉 Entonces, **cualquier valor que le pasemos al `resolve` va a poder ser accedido en el `then` cuando estemos _usando la promesa_ (y si esta se resuelve exitosamente) y cualquier valor que le pasemos al `reject` va a poder ser accedido en el `catch`, en el caso de que falle**. Por ejemplo

```js
const promise = new Promise((resolve, reject) => {
  const a = 2;
  
  if (a === 2) {
    resolve('success!');
  } else {
    reject('FAIL.');
  }
});

promise
  .then(res => console.log(res))     // acá tenemos acceso al valor que retorna el `resolve`, loguea 'success!'
  .catch(err => console.error(err)); // acá tenemos acceso al valor que retorna el `reject`, loguea 'FAIL.'
```

[↑ Ir al inicio](https://github.com/undefinedschool/notes-es6-promises#contenido)

## Promise Chaining 

### `then()`

Una promesa también puede devolver otra promesa (después de todo, son objetos), que también encadenaremos usando `then()` y se ejecutará _sólo cuando la promesa anterior esté resuelta_. Por lo tanto, _las promesas se pueden componer_, es decir, usar los resultados de unas como input de otras.

Si la promesa falla y tenemos un método `catch()`, se ejecutará para cualquier promesa que tengamos en la cadena.

[↑ Ir al inicio](https://github.com/undefinedschool/notes-es6-promises#contenido)

## `Promise.all` 

👉 Este método **recibe un array de _promises_, las ejecuta y retorna una (nueva) _promesa a un array con los resultados_, si y sólo si todas las promesas se resuelven de forma exitosa**.

Permite ejecutar varias promesas de forma [_concurrente_](https://www.youtube.com/watch?v=kMr3mF71Kp4).

Si `p1`, `p2`, y `p3` son funciones que retornan promesas, entonces podríamos hacer

```js
Promise.all([p1(), p2(), p3()])
  .then(([res1, res2, res3]) => {
  console.log(res1);
  console.log(res2);
  console.log(res3);
})
```

donde `res1`, `res2` y `res3` se corresponden con los valores de las promesas resueltas.

> 👉 Como la respuesta es una promesa a un array, también podemos simplificar el código usando métodos de array, como `forEach`

```js
Promise.all([p1(), p2(), p3()])
  .then(results => results.forEach(res => console.log(res)));
```

> 👉 **Vamos a utilizar `Promise.all()` cuando nos interese esperar a tener todas las promesas resueltas, independientemente del orden en que esto suceda** (podrían ser promesas que no tengan relación entre si), por eso resulta especialmente útil si estamos utilizando [`async/await`](https://github.com/undefinedschool/notes-es2017-async-await/), para de esta forma evitar esperas innecesarias en la ejecución

[↑ Ir al inicio](https://github.com/undefinedschool/notes-es6-promises#contenido)

## Error handling

A través del método `catch()`, podemos centralizar el manejo de errores, resultando mucho más simple de mantener que utilizando, por ejemplo _callbacks_, ya que cualquier promesa que falle (sea rechazada) en una cadena de operaciones, va a terminar siendo manejada en un `catch()` al final y ya no necesitamos manejar los errores en cada operación asincrónica de forma separada.

[↑ Ir al inicio](https://github.com/undefinedschool/notes-es6-promises#contenido)

### Ejemplo usando [Fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API)

```js
fetch('https://pokeapi.co/api/v2/pokemon/ditto/')
  .then(x => console.log('success! 😸'))
  .catch(x => console.log('fail. 😿'));
```

[↑ Ir al inicio](https://github.com/undefinedschool/notes-es6-promises#contenido)

## Promises, _microtasks_ y el _Event Loop_

Resolver una Promise cuenta como una micro tarea (_micro tasks_), por lo que van a ejecutarse al inicio de la próxima iteración del _Event Loop_, teniendo prioridad sobre otras tareas (_macrotasks_).

Para más detalles, ver [Notas sobre el _Event Loop_](https://github.com/undefinedschool/notes-event-loop)

[![JavaScript Promises In 10 Minutes](https://img.youtube.com/vi/DHvZLI7Db8E/0.jpg)](https://www.youtube.com/watch?v=DHvZLI7Db8E)
> Ver [JavaScript Promises In 10 Minutes](https://www.youtube.com/watch?v=DHvZLI7Db8E)

[↑ Ir al inicio](https://github.com/undefinedschool/notes-es6-promises#contenido)

## Compatibilidad y soporte

Esta feature de _ES6_ tiene soporte en todos los browsers modernos, pero no en IE. 

Para navegadores sin soporte, podemos usar [polyfills](https://github.com/stefanpenner/es6-promise).

[↑ Ir al inicio](https://github.com/undefinedschool/notes-es6-promises#contenido)
