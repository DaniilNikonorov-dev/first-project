Написать функцию-промисификатор для функций, работающих с коллбеками. 


**
Функции, работающие с колбеками, обычно имеют следующий вид:`
`function loadScript(src: string, callback: <T>(error: Error | null, result?: T) => void) {
  /* ... */
}
При этом такая функция может принимать сколько угодно аргументов, последний из которых — коллбек.
Требуется написать функцию promisify, которая позволит работать с такими функциями как с промисами:

```JS
const loadScriptPromise = promisify(loadScript);`

`loadScriptPromise(``'url'``)`

  `.then(result =>` `/* ... */``)`

  `.``catch``(error =>` `/* ... */``)`

*/

const promisify = () => {`

}
```

Решение

```JS
const promisify = (fn) => {

    return function (...args) {

        return new Promise((resolve, reject) => {

            fn.call(this, ...args, (error, ...result) => {

                if (error) { reject(error) }

                else { resolve(result.length > 1 ? results : result[0]) }

            })

        })

    }
}
```

