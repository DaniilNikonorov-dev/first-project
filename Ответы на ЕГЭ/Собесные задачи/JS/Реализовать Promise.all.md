Необходимо написать свою функцию promiseAll, которая является аналогом Promise.all.

- на вход поступает массив промисов
- реджект, если хотя бы один промис упал
- резолв, если все промисы успешно выполнены
- в случае резолва порядок результатов должен сохраняться
- в случае реджекта сразу реджект не дожидаясь остальных промис

```JS
const promiseAll = (promises) => {
  return new Promise((resolve, reject) => {
    // your code
  })
}
 
const resolve = (value, timeout) =>
  new Promise((res) => setTimeout(res, timeout, value))
const reject = (value, timeout) =>
  new Promise((_, rej) => setTimeout(rej, timeout, value))
 
promiseAll([resolve(1, 200), resolve(2, 300), resolve(3, 100)])
  .then(console.log) // [1, 2, 3]
 
promiseAll([reject(1, 100), reject(2, 500), resolve(3, 1000)])
  .catch(console.error) // 1
```

Решение

```JS
const promiseAll = (promises) => {
  return new Promise((resolve, reject) => {
    const promisesResult = [];
    let promisesResolved = 0;
 
    for (let i = 0; i < promises.length; i++) {
      promises[i]
        .then((response) => {
          promisesResult[i] = response;
          promisesResolved++;
 
          if (promisesResolved === promises.length) {
            resolve(promisesResult);
          }
        })
        .catch((error) => reject(error));
    }
  });
};
```

Возможное решение
```JS
const promiseAll = (promises) => {
  return new Promise((resolve, reject) => {
    // Если массив пустой, сразу резолвим пустым массивом
    if (promises.length === 0) {
      return resolve([]);
    }

    const results = [];
    let completed = 0;

    promises.forEach((promise, index) => {
      // Оборачиваем promise, чтобы корректно обработать не-промис значения
      Promise.resolve(promise)
        .then(value => {
          results[index] = value; // Сохраняем результат по индексу
          completed++;
          // Если все промисы завершены успешно, резолвим итоговый массив
          if (completed === promises.length) {
            resolve(results);
          }
        })
        .catch(err => {
          // При первом реджекте сразу реджектим основной промис
          reject(err);
        });
    });
  });
};
```

// Примеры использования:
const resolve = (value, timeout) =>
  new Promise((res) => setTimeout(res, timeout, value));
const reject = (value, timeout) =>
  new Promise((_, rej) => setTimeout(rej, timeout, value));

promiseAll([resolve(1, 200), resolve(2, 300), resolve(3, 100)])
  .then(console.log) // [1, 2, 3]
  .catch(console.error);

promiseAll([reject(1, 100), reject(2, 500), resolve(3, 1000)])
  .then(console.log)
  .catch(console.error); // 1
