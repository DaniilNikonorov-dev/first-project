function createCounter() {
````
    let count = 0;  // Локальная переменная для хранения значения счётчика

    return {
        // Геттер для получения текущего значения счётчика
        get count() {
            return count;
        },
        // Сеттер для предотвращения изменения значения счётчика
        set count(value) {
            // Сеттер ничего не делает, если пытаемся изменить значение
            // Таким образом, значение нельзя изменять извне
        },
        // Метод для инкрементации счётчика
        increment() {
            count++;
        }
    };
}

const counter = createCounter();
console.log(counter.count);  // 0
counter.increment();
console.log(counter.count);  // 1
counter.increment();
console.log(counter.count);  // 2
counter.count = 100;  // Попытка изменить значение не повлияет на счётчик
console.log(counter.count);  // 3 (значение не изменилось)


````
