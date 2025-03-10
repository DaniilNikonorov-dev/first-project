Необходимо написать свою функцию promiseAny, которая является аналогом Promise.any.

- на вход поступает массив промисов
- резолв с первым зарезолвленным промисом
- реджект, если упали все промисы
- в случае реджекта порядок ошибок должен сохраняться
- в случае резолва не должен дожидаться выполнения остальных промисов


```JS
const promiseAny = (promises) => {
   
}  
 
 
const resolve = (value, timeout) =>
  new Promise((res) => setTimeout(res, timeout, value))
const reject = (value, timeout) =>
  new Promise((_, rej) => setTimeout(rej, timeout, value))
 
promiseAny([resolve(1, 200), resolve(2, 100), resolve(3, 300)]).then(
  console.log
) // 2
 
promiseAny([reject(1, 500), reject(2, 100), resolve(3, 200)]).then(
  console.log
) // 3
 
promiseAny([reject(1, 300), reject(2, 100), reject(3, 200)]).catch(
  console.error
) // [1, 2, 3]
```

Решение

```JS
const promiseAny = (promises) =>
  new Promise((resolve, reject) => {
    const errors = []
    let rejected = 0
 
    for (let i = 0; i < promises.length; i++) {
      promises[i]
        .then((result) => resolve(result))
        .catch((err) => {
          errors[i] = err
          rejected++
 
          if (rejected === promises.length) {
            reject(errors)
          }
        })
    }
  })
```

Еще одно решение
```JS
const promiseAny = (promises) => {
  return new Promise((resolve, reject) => {
    if (promises.length === 0) {
      return reject([]); // Если входной массив пуст, сразу реджектим пустым массивом ошибок
    }
    
    let errors = new Array(promises.length);
    let rejectedCount = 0;
    
    promises.forEach((p, index) => {
      // Оборачиваем значение, чтобы корректно работать даже с не-промисами
      Promise.resolve(p)
        .then(resolve) // Если хотя бы один промис успешно выполнится, сразу резолвим итоговый промис
        .catch(err => {
          errors[index] = err; // Сохраняем ошибку по индексу для сохранения порядка
          rejectedCount++;
          // Если все промисы завершились реджектом, реджектим итоговый промис с массивом ошибок
          if (rejectedCount === promises.length) {
            reject(errors);
          }
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

promiseAny([resolve(1, 200), resolve(2, 100), resolve(3, 300)])
  .then(console.log) // выведет: 2 (так как второй промис зарезолвится первым)
  .catch(console.error);

promiseAny([reject(1, 500), reject(2, 100), resolve(3, 200)])
  .then(console.log) // выведет: 3
  .catch(console.error);

promiseAny([reject(1, 300), reject(2, 100), reject(3, 200)])
  .then(console.log)
  .catch(console.error); // выведет: [1, 2, 3]
