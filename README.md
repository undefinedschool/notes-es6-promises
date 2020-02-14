# [WIP] ✨ ES6: Promises

**Una _promesa_ en JavaScript es como una promesa en la vida real: nos comprometemos a hacer algo y esta acción tiene 2 resultados posibles, que se cumpla (_se resuelve exitosamente_) o no (_es rechazada_)**.

Mas técnicamente, una _promesa_ es un **objeto** que representa un valor que puede estar disponible en algún momento del futuro, o nunca. Este valor representa a su vez el resultado exitoso o fracaso de ejecutar una tarea **asincrónica**.

Vamos a utilizar _promises_ para escribir código asincrónico, como hacer un re  uest a una API por medio de `fetch` o una consulta a una base de datos. 

👉 La principal ventaja frente a usar _callbacks_ (otra forma que tenemos de manejar asincronismo en JavaScript) es que las _promises_ nos proveen una alternativa para evitar caer en el [_callback hell_](http://callbackhell.com/), a través de una sintaxis más concisa, limpia y fácil de razonar. 

Además diferencia de los _callbacks_, **las promesas se puede _componer_**, utilizando el resultado o _output_ de una como el _input_ de otra.

## Métodos

Al tratarse de un objeto, las promesas tienen una _interfaz_ que nos permite interactuar con estas. 
En particular, vamos a estar estar usando los metodos `.then()` y `.catch()`

👉 Estos métodos nos van a permitir operar con un eventual valor en caso de éxito (el `.then()`), o de falla (el ´catch()´). Esto permite que métodos _asincrónicos_ devuelvan valores como si fueran _sincrónicos_: **en vez de inmediatamente retornar el valor final, _el método asincrónico devuelve una promesa de darnos el valor en algún momento en el futuro_**.

- `then()`: el código dentro se va a ejecutar _sólo si la promesa se resuelva de forma exitosa_
- `catch()`: el código dentro se va a ejecutar en caso de error (_la promesa es rechazada_)

Los métodos `then()` y `catch()` devuelven a su vez promesas, que pueden ser encadenadas

```js
promise
  .then(...)
  .then(...)
  .then(...)
  .catch(...)
```

**Nota:**

![](https://i.imgur.com/xA4ea9r.png)

## Error handling

A través del método `catch()`, podemos centralizar el manejo de errores, resultando mucho más simple de mantener que utilizando, por ejemplo _callbacks_, ya que cualquier promesa que falle (sea rechazada) en una cadena de operaciones, va a terminar siendo manejada en un `catch()` al final y ya no necesitamos manejar los errores en cada operación asincrónica de forma separada.

### Ejemplo usando [Fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API)

```js
fetch('https://pokeapi.co/api/v2/pokemon/ditto/')
  .then(x => console.log('success! 😸'))
  .catch(x => console.log('fail. 😿'));
```

## Estados de una promesa

Una Promesa se encuentra siempre en uno de los siguientes estados:

- pendiente (_pending_): estado inicial de cualquier promesa, no cumplida o rechazada aún
- resuelta (_fulfilled_): significa que la operación se completó exitosamente
- rechazada (_rejected_): significa que la operación falló

## Para qué sirven?

- Nos permiten escribir _código asincrónico_ de forma más legible, evitando el [_Callback Hell_](http://callbackhell.com/)
- Nos permite un [mejor manejo de los errores]()

## Crear promesas

Cuando creamos una _Promise_, le pasamos una función _callback_ como argumento. Dentro de este _callback_, tenemos 2 parámetros: `resolve()` y `reject()`.

### `resolve()` 

Cuando el estado de la promesa pasa a estar _resuelto_ (`fullfiled`), se ejecuta el método `resolve()`. Podemos pasar argumentos que serán llevados al _callback_ del `.then()` en el método `resolve()`

### `reject()`

Es el método que ejecutamos si consideramos que la promesa _falló_ (o que debe ser rechazada). Podemos pasar cualquier mensaje de error como argumento, el cual será tomado en el _callback_ del método `catch()` (que se ejecuta sólo si la promesa falla).

```js
const promise = new Promise((resolve, reject) => {
  resolve('success!');
  reject('FAIL.')
});

promise
  .then()
  .catch()
```

## Chaining 

### `then()`

Podemos encadenar múltiples métodos `.then()` y se ejecutarán secuencialmente.

Lo que sea que retornemos del `.then()` actual, se va a pasar como argumento del próximo.

### Promesas

Una promesa también puede devolver otra promesa (después de todo, son objetos), que también encadenaremos usando `then()` y se ejecutará _sólo cuando la promesa anterior esté resuelta_.

Si la promesa falla y tenemos un método `catch()`, se ejecutará para cualquier promesa que tengamos en la cadena.

## Compatibilidad y soporte

Esta feature de _ES6_ tiene soporte en todos los browsers modernos, pero no en IE. 

Para navegadores sin soporte, podemos usar [polyfills](https://github.com/stefanpenner/es6-promise).

## `Promise.all` 

Recibe un array de _promises_, las ejecuta y retorna una (nueva) _promesa a un array con los resultados_, si y sólo si todas las promesas se resuelven de forma exitosa.

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

👉 Como la respuesta es una promesa a un array, también podemos simplificar el código usando métodos de array, como `forEach`

```js
Promise.all([p1(), p2(), p3()])
  .then(results => results.forEach(res => console.log(res)));
```

[![JavaScript Promises In 10 Minutes](https://img.youtube.com/vi/DHvZLI7Db8E/0.jpg)](https://www.youtube.com/watch?v=DHvZLI7Db8E)
