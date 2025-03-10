 Реализуйте функцию "deep copy" (глубокое копирование) для объекта в JavaScript. Глубокое копирование означает, что все значения объекта копируются и любое изменение данных исходного объекта не влияет на копию, и наоборот.  
  
Кандидат можем вспомнить про способе копирования с помощью JSON.parse(JSON.stringify()) / structuredClone(). Спрашиваем про нюансы рботы с этими способами. Спрашиваем про нюансы работы с функциями, что хотим услышать:

###### **JSON.parse(JSON.stringify()):**

- Если объект содержит функции, undefined, символы (Symbol) или циклические ссылки, они будут потеряны в процессе копирования
    
- Объекты Date будут преобразованы в строки, а регулярные выражения потеряны.
    
- Объекты Map, Set, WeakMap, RegExp, WeakSet и ArrayBuffer не могут быть скопированы с использованием

###### **structuredClone():**

- Выбросит ошибку "could not be cloned" если в объекте копирования будет присутсвовать функции, prototype, классы
- В отличии от JSON поддерживает Date, RegExp, Map, Set


После этого просим реализовать свою функцию.  
  
В ходе решения можно обсудить с кандидатом следующие вопросы (не обязательно все):

##### - Как проверить, что в переменной лежит объект?
Есть несколько способов:
**Используем `typeof`**
```JS
typeof value === 'object' && value !== null
```
- `typeof null === 'object'`, поэтому нужен `value !== null`.
- Но `typeof` не различает `Array`, `Date`, `RegExp`, `Map`, `Set` и обычные объекты.

**Проверяем через `Object.prototype.toString.call(value)`**
```JS
Object.prototype.toString.call(value) === '[object Object]'
```
Это точный способ, который отсекает массивы, `null` и другие объекты.


##### - Как проверить, что в переменной лежит массив?
```JS
Array.isArray(value)
```


##### - Что возвращает typeof?
`typeof` возвращает строку с типом переменной. Вот основные значения:

|Выражение|`typeof` возвращает|
|---|---|
|`typeof 42`|`'number'`|
|`typeof 'hello'`|`'string'`|
|`typeof true`|`'boolean'`|
|`typeof undefined`|`'undefined'`|
|`typeof Symbol()`|`'symbol'`|
|`typeof BigInt(10)`|`'bigint'`|
|`typeof null`|**`'object'`** (ошибка JS)|
|`typeof {}`|`'object'`|
|`typeof []`|`'object'` (но это массив)|
|`typeof function() {}`|`'function'`|

⚠️ **Важно:**

- `typeof null === 'object'` — исторический баг в JS.
- `typeof NaN === 'number'` — NaN технически число.


##### - Как проверить, что объект X является наследником Y?
Используем `instanceof`:
```JS
class Animal {}
class Dog extends Animal {}

const dog = new Dog();

console.log(dog instanceof Dog);    // true
console.log(dog instanceof Animal); // true
console.log(dog instanceof Object); // true
console.log(dog instanceof Array);  // false

```

##### Эталонное решение:

```JS
function deepCopy(obj) {
    if (obj === null || typeof obj !== 'object') {
        return obj;
    }
 
    let copy;
 
    if (Array.isArray(obj)) {
        copy = [];
        obj.forEach((elem, index) => {
            copy[index] = deepCopy(elem);
        });
        return copy;
    }
 
    copy = Object.getPrototypeOf(obj) === null ?    Object.create(null) : {};
    for (const key in obj) {
        if (Object.hasOwn(obj, key)) {
            copy[key] = deepCopy(obj[key]);
        }
    }
    return copy;
}
```

