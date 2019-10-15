# Promesas (WIP)

Una _promesa_ es un **objeto** que representa un valor que puede estar disponible en algún momento del futuro, o nunca. 
Este valor representa a su vez el resultado exitoso o fracaso de ejecutar una tarea **asincrónica**.

## Métodos

Al tratarse de un objeto, las promesas tienen una _interfaz_ que nos permite interactuar con estas. 
En particular, vamos a estar estar usando los metodos `.then()` y `.catch()`

Estos métodos nos van a permitir operar con un eventual valor en caso de éxito (el `.then()`), o de falla (el ´catch()´). Esto permite que métodos _asincrónicos_ devuelvan valores como si fueran _sincrónicos_: en vez de inmediatamente retornar el valor final, el método asincrónico devuelve una promesa de darnos el valor en algún momento en el futuro.

- `then()`: se va a ejecutar sólo
- `catch()`: se va a ejecutar en caso de error

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

### Ejemplo usando [Fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API)

```js
fetch('https://pokeapi.co/api/v2/pokemon/ditto/')
  .then(x => console.log('success! 😸'))
  .catch(x => console.log('fail. 😿'));
```

## Estados de una promesa

Una Promesa se encuentra siempre en uno de los siguientes estados:

- pendiente (pending): estado inicial de cualquier promesa, no cumplida o rechazada aún
- resuelta (fulfilled): significa que la operación se completó exitosamente
- rechazada (rejected): significa que la operación falló

## Para qué sirven?

- Nos permiten escribir _código asincrónico_ de forma más legible, evitando el [_Callback Hell_](http://callbackhell.com/)
- Nos permite un mejor manejo de los errores

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
