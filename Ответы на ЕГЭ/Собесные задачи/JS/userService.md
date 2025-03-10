1. Что выведет код? Что ожидалось? Как исправить? Предложите несколько вариантов.
2. Исправить программу так, чтобы она падала при выполнении данного кода.

```JS
const userService = {
    currentFilter: 'active',
    users: [
        {name: 'Alex', status: 'active'},
        {name: 'Nick', status: 'deleted'},
    ],
    getFilteredUsers: function() {
        return this.users.filter(function (user) {
            return user.status === this.currentFilter;
        });
    }
};
 
console.log(userService.getFilteredUsers());
```

1 Выведет пустой массив, хотелось бы `{ name: 'Alex' }` . Проблема в том, что функция в фильтре имеет глобальный контекст или `undefined`  при наличии  `use strict`   
Исправить проще всего в порядке простоты:

##### Использование стрелочной функции (самый современный и понятный способ):`
```JS
const userService = {
    currentFilter: 'active',
    users: [
        {name: 'Alex', status: 'active'},
        {name: 'Nick', status: 'deleted'},
    ],
    getFilteredUsers: function() {
        return this.users.filter(user => user.status === this.currentFilter);
    }
};

console.log(userService.getFilteredUsers()); // [{ name: 'Alex', status: 'active' }]
```

##### Сохранение контекста через переменную (const self = this):
```JS
const userService = {
    currentFilter: 'active',
    users: [
        {name: 'Alex', status: 'active'},
        {name: 'Nick', status: 'deleted'},
    ],
    getFilteredUsers: function() {
        const self = this;
        return this.users.filter(function (user) {
            return user.status === self.currentFilter;
        });
    }
};

console.log(userService.getFilteredUsers()); // [{ name: 'Alex', status: 'active' }]
```

##### Привязка this через bind:
```JS
const userService = {
    currentFilter: 'active',
    users: [
        {name: 'Alex', status: 'active'},
        {name: 'Nick', status: 'deleted'},
    ],
    getFilteredUsers: function() {
        return this.users.filter(function (user) {
            return user.status === this.currentFilter;
        }.bind(this)); // Привязываем this через bind
    }
};

console.log(userService.getFilteredUsers()); // [{ name: 'Alex', status: 'active' }]
```

##### Передача this вторым аргументом в filter (наименее известный, но самый короткий способ):
```JS
const userService = {
    currentFilter: 'active',
    users: [
        {name: 'Alex', status: 'active'},
        {name: 'Nick', status: 'deleted'},
    ],
    getFilteredUsers: function() {
        return this.users.filter(function (user) {
            return user.status === this.currentFilter;
        }, this); // Передаем this вторым аргументом в filter
    }
};

console.log(userService.getFilteredUsers()); // [{ name: 'Alex', status: 'active' }]
```

##### Варианты
- анонимной функцией внутри `filter` 
- `const self = this` 
- `bind/call/apply` 
- передать `this`  вторым аргументом в `filter`  (мало кто знает)
-
1. Добавить вверху файла `use strict` .

