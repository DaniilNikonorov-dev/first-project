Задача в несколько шагов.

Даны HTTP-запросы, обёрнутые в Observable и Promise.

Сколько уйдёт запросов?

```TS
const obs$ = httpClient.get('tinkoff.ru'); // Стандартный HttpClient из Angular
const promise = fetch('tinkoff.ru');
```

1. **0** (у Observable) и **1** (у fetch) — **всего 0 + 1 = 1 запрос** (возвращает Promise, в названии переменной уже есть подсказка)


Сколько запросов уйдёт в таком случае?


``` TS
const obs$ = httpClient.get('tinkoff.ru'); // Стандартный HttpClient из Angular
const promise = fetch('tinkoff.ru');
 
obs$.subscribe(console.log);
obs$.subscribe(console.log);
obs$.subscribe(console.log);
 
promise.then(console.log);
promise.then(console.log);
promise.then(console.log);
```

1. **3** (у Observable) и **1** (у fetch) — **всего 3 + 1 = 4 запроса** (просто вызовется коллбэк у зарезолвленного промиса, запрос улетит единожды)

1. Сколько раз выведется сообщение в консоль в каждом из случаев?

1. **3** (у Observable) и **3** (у Promise.then) — **всего 3 + 3 = 6 логов в консоль**
2. Самое простое решение — shareReplay(1). Можно спросить про более расширенную версию конфигурации оператора


