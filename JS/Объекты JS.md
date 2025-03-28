# Копирование и объединение 
1. ## [Object.assign](https://learn.javascript.ru/object-copy#cloning-and-merging-object-assign)
`Object.``assign``(dest, [src1, src2, src3...``]``)` не работает в глубоким копированием

2. С глубоким копированием нужно использовать цикл клонирования, лучше вместе с рекурсией, есть готовая реализация от lodash

3. Также, есть метод [structuredClone()](https://developer.mozilla.org/en-US/docs/Web/API/structuredClone), но он работает только с современными браузерами


# Конструктор


Это и является основной целью конструкторов – реализовать код для многократного создания однотипных объектов.

Давайте ещё раз отметим – технически любая функция (кроме стрелочных функций, поскольку у них нет `this`) может использоваться в качестве конструктора. Его можно запустить с помощью `new`, и он выполнит выше указанный алгоритм. Подобные функции должны начинаться с заглавной буквы – это общепринятое соглашение, чтобы было ясно, что функция должна вызываться с помощью «new».
## [Итого](https://learn.javascript.ru/constructor-new#itogo)

- Функции-конструкторы или просто конструкторы, являются обычными функциями, но существует общепринятое соглашение именовать их с заглавной буквы.
- Функции-конструкторы следует вызывать только с помощью `new`. Такой вызов подразумевает создание пустого `this` в начале и возврат заполненного в конце.

Мы можем использовать конструкторы для создания множества похожих объектов.

JavaScript предоставляет функции-конструкторы для множества встроенных объектов языка: таких как `Date`, `Set`, и других, которые нам ещё предстоит изучить.

# Опциональная цепочка
## [Итого](https://learn.javascript.ru/optional-chaining#itogo)

Синтаксис опциональной цепочки `?.` имеет три формы:

1. `obj?.prop` – возвращает `obj.prop` если `obj` существует, в противном случае `undefined`.
2. `obj?.[prop]` – возвращает `obj[prop]` если `obj` существует, в противном случае `undefined`.
3. `obj.method?.()` – вызывает `obj.method()`, если `obj.method` существует, в противном случае возвращает `undefined`.

Как мы видим, все они просты и понятны в использовании. `?.` проверяет левую часть на `null/undefined` и позволяет продолжить вычисление, если это не так.

Цепочка `?.` позволяет безопасно получать доступ к вложенным свойствам.

Тем не менее, мы должны использовать `?.` осторожно, только там, где по логике кода допустимо, что левая часть не существует. Чтобы он не скрывал от нас ошибки программирования, если они возникнут.


# Преобразование объекта в примитивы
**Чтобы выполнить преобразование, JavaScript пытается найти и вызвать три следующих метода объекта:**

1. Вызвать `obj[Symbol.toPrimitive](hint)` – метод с символьным ключом `Symbol.toPrimitive` (системный символ), если такой метод существует,
2. Иначе, если хинт равен `"string"`
    - попробовать вызвать `obj.toString()` или `obj.valueOf()`, смотря какой из них существует.
3. Иначе, если хинт равен `"number"` или `"default"`
    - попробовать вызвать `obj.valueOf()` или `obj.toString()`, смотря какой из них существует.
## [Итого](https://learn.javascript.ru/object-toprimitive#itogo)

Преобразование объекта в примитив вызывается автоматически многими встроенными функциями и операторами, которые ожидают примитив в качестве значения.

Существует всего 3 типа (хинта) для этого:

- `"string"` (для `alert` и других операций, которым нужна строка)
- `"number"` (для математических операций)
- `"default"` (для некоторых других операторов, обычно объекты реализуют его как `"number"`)

Спецификация явно описывает для каждого оператора, какой ему следует использовать хинт.

Алгоритм преобразования таков:

1. Сначала вызывается метод `obj[Symbol.toPrimitive](hint)`, если он существует,
2. В случае, если хинт равен `"string"`
    - происходит попытка вызвать `obj.toString()` и `obj.valueOf()`, смотря что есть.
3. В случае, если хинт равен `"number"` или `"default"`
    - происходит попытка вызвать `obj.valueOf()` и `obj.toString()`, смотря что есть.

Все эти методы должны возвращать примитив (если определены).

На практике часто бывает достаточно реализовать только `obj.toString()` в качестве универсального метода для преобразований к строке, который должен возвращать удобочитаемое представление объекта для целей логирования или отладки.


# Геттеры и сеттеры
**Геттеры** и **сеттеры** в JavaScript — это специальные методы для управления доступом к свойствам объекта.

- **Геттеры** позволяют получать значение свойства с дополнительной логикой, при этом доступ к свойству выглядит как обычное обращение.
    
    - **Синтаксис геттера**:
        
        javascript
        
        Копировать код
        
        `get свойство() {     // Логика получения значения }`
        
- **Сеттеры** позволяют изменять значение свойства с дополнительной логикой, при этом присваивание значения выглядит как обычное присваивание.
    
    - **Синтаксис сеттера**:
        
        javascript
        
        Копировать код
        
        `set свойство(значение) {     // Логика изменения значения }`
        

### Преимущества:

- **Инкапсуляция**: позволяет скрыть сложную логику работы с данными.
- **Контроль доступа**: даёт возможность проверять или изменять данные при их получении или изменении.