# Что появится в консоли?

```JS
for (var i = 0; i < 10; i++) {
    setTimeout(function() {
        console.log(i);
    }, 1000);
}
```
Классическая задача, кандидаты часто с ней сталкиваются.

_Усложнение_: назвать все возможные методы исправить поведение (замыкание, область видимости переменной, передача аргумента через setTimeout, каррирование через bind)

Решение:
Через 1 секунду появится 10 раз число 10

Цикл `for` выполняется с переменной `i`, которая объявлена с помощью `var`. Это значит, что `i` имеет функциональную область видимости, а не блочную. Иными словами, существует только одна переменная `i`, общая для всех итераций цикла.

### 1. **Использование `let` вместо `var`**

Замена `var` на `let` обеспечивает блочную область видимости переменной `i`. Таким образом, каждая итерация создаёт собственную копию переменной.

```JS
for (let i = 0; i < 10; i++) {
    setTimeout(function() {
        console.log(i);
    }, 1000);
}
```

2. **Создание замыкания с помощью функции**

Можно обернуть `setTimeout` в функцию, которая создаёт собственную область видимости для текущего значения `i`.

```JS
for (var i = 0; i < 10; i++) {
    (function(i) {
        setTimeout(function() {
            console.log(i);
        }, 1000);
    })(i);
}
```

3. **Передача аргумента в `setTimeout`**
Функция `setTimeout` позволяет передавать дополнительные аргументы, которые затем будут доступны в её колбэке. Мы можем передать `i` как аргумент.

```JS
for (var i = 0; i < 10; i++) {
    setTimeout(function(i) {
        console.log(i);
    }, 1000, i);
}
```



# Что появится в консоли и почему?

```JS
var a = 1;
 
function foo() {
  console.log(a);
}
 
function foo2() {
  var a = 2;
  foo();
}
 
foo2();
```

Решение:
Консоль выведет 1
- Локальная переменная `a` в `foo2()` **не используется** функцией `foo()`.
- Функция `foo()` всегда использует ту область видимости, в которой была определена, то есть глобальную, где `a = 1`.



# Что появится в консоли? Изменится ли результат, если мы заменим функцию на стрелочную?

```JS
const user = {
    getName: function() {
         console.log(this.userName);
    },
    userName: 'Alex'
};
  
user.getName.userName = 'Nick';
user.getName(); // ?
 
const { getName } = user;
getName(); // ?
```

### Итоговые выводы:

1. **Исходный код:**
    - `user.getName();` → `Alex`
    - `getName();` → `undefined`
2. **При замене на стрелочную функцию:**
    - `user.getName();` → `undefined`
    - `getName();` → `undefined`







В каком порядке будут выполнены функции и какие аргументы получат, если все 3 функции возвращают промис?

getPromise1().then(function () {
    return getPromise2();
}).then(finalHandler);
   
getPromise1().then(function () {
    getPromise2();
}).then(finalHandler);
   
getPromise1()
    .then(getPromise2())
    .then(finalHandler);
   
getPromise1()
    .then(getPromise2)
    .then(finalHandler);

Решение


Что появится в консоли и почему?


Promise.reject('a')
    .catch(p => p + 'b')
    .catch(p => p + 'с')
    .then(p => p + 'd')
    .finally(p => p + 'e')
    .then(p => console.log(p))
 
console.log('f');

Решение



Как упростить код?

function getCompanyInfo() {
    return new Promise(function (resolve, reject) {
        return userService.companyInfo().then(function (response) {
            resolve(response);
        }, function (rejection) {
            reject(rejection);
        });
    });
}


Решение