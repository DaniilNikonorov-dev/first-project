##### Напишите класс Person:

```JS
const person = new Person('Alex', 'Petrov');
person.fullName(); // 'Alex Petrov'
```
Решение
```JS
class Person {
    constructor(firstName, lastName) {
        this.firstName = firstName;
        this.lastName = lastName;
    }

    fullName() {
        return `${this.firstName} ${this.lastName}`;
    }
}

const person = new Person('Alex', 'Petrov');
console.log(person.fullName()); // 'Alex Petrov'
```

##### Унаследуйте от Person класс Employee:

```JS
const employee = new Employee('Alex', 'Petrov', 'developer');
employee.fullName(); // 'Alex Petrov (developer)'
```
Решение
```JS
class Person {
    constructor(firstName, lastName) {
        this.firstName = firstName;
        this.lastName = lastName;
    }

    fullName() {
        return `${this.firstName} ${this.lastName}`;
    }
}

class Employee extends Person {
    constructor(firstName, lastName, position) {
        super(firstName, lastName); // Вызываем конструктор родительского класса
        this.position = position; // Добавляем новое свойство
    }

    fullName() {
        return `${super.fullName()} (${this.position})`; // Используем метод родителя и дополняем его
    }
}

const employee = new Employee('Alex', 'Petrov', 'developer');
console.log(employee.fullName()); // 'Alex Petrov (developer)'
```

##### Перепишите метод employee.fullName так, чтобы он работал через геттер без вызова.

```JS
employee.fullName; // 'Alex Petrov (developer)'
```
решение
```JS
class Person {
    constructor(firstName, lastName) {
        this.firstName = firstName;
        this.lastName = lastName;
    }

    get fullName() {
        return `${this.firstName} ${this.lastName}`;
    }
}

class Employee extends Person {
    constructor(firstName, lastName, position) {
        super(firstName, lastName);
        this.position = position;
    }

    get fullName() {
        return `${super.fullName} (${this.position})`; // Используем геттер родителя
    }
}

const employee = new Employee('Alex', 'Petrov', 'developer');
console.log(employee.fullName); // 'Alex Petrov (developer)'
```

