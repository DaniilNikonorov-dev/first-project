Необходимо реализовать класс EventEmitter, с возможностью подписки на разные события, отписки, и оповещения о событии для всех подписчиков.

Базовый пример для проверки:

```JS
class EventEmitter {
    // Реализуйте класс, чтобы заработал код ниже
}
 
const emitter = new EventEmitter()
 
const cb1 = () => console.log('cb1')
const cb2 = () => console.log('cb2')
 
emitter
    .on('event', cb1) // подписка коллбэка cb1 на событие 'event'
    .on('event', cb2)
    .emit('event') // срабатывание события 'event'
    // 'cb1'
    // 'cb2'
    .off('event', cb2) // отписка коллбэка cb2 от события 'event'
    .emit('event')
    // 'cb1'
```

##### Вопросы:
###### Какое должно быть поведение, если в коллбэке будет выброшено исключение?

- **Основной момент:** Если в одном из коллбэков выбрасывается исключение, оно не должно прерывать вызов остальных подписчиков.
- **Рекомендуемое решение:** В методе `emit` обернуть каждый вызов коллбэка в `try/catch`. Это позволит:
    - Локально обработать ошибку (например, залогировать её).
    - Продолжить вызов оставшихся коллбэков.

###### Как передавать данные при вызове события?
**Решение:** Метод `emit` принимает произвольное количество дополнительных аргументов (через rest-оператор `...args`).

##### Решение

###### Эталонное:
``` JS
class EventEmitter {
    constructor() {
        this.events = new Map()
    }
 
    on(event, callback) {
        if (!this.events.has(event)) {
            this.events.set(event, new Set())
        }
        this.events.get(event).add(callback)
 
        return this
    }
 
    off(event, callback) {
        if (this.events.has(event)) {
            this.events.get(event).delete(callback)
        }
 
        return this
    }
 
    emit(event, payload) {
        if (this.events.has(event)) {
            this.events.get(event).forEach((callback) => {
                try {
                    callback(payload)
                } catch (e) {
                    console.error(e)
                }
            })
        }
 
        return this
    }
}
```

###### Возможное:
```JS
class EventEmitter {
  constructor() {
    this.events = {}; // Объект, где ключ — название события, а значение — массив коллбэков
  }

  // Подписка: добавляем коллбэк для конкретного события
  on(event, cb) {
    if (!this.events[event]) {
      this.events[event] = [];
    }
    this.events[event].push(cb);
    return this; // Для возможности цепочки вызовов
  }

  // Отписка: удаляем конкретный коллбэк для события
  off(event, cb) {
    if (!this.events[event]) return this;
    this.events[event] = this.events[event].filter(listener => listener !== cb);
    return this;
  }

  // Оповещение: вызываем все коллбэки, подписанные на событие
  // ...args — данные, которые будут переданы подписчикам
  emit(event, ...args) {
    if (!this.events[event]) return this;

    // Если в одном из коллбэков возникает исключение, оно не должно мешать вызову остальных
    // Поэтому оборачиваем вызов каждого коллбэка в try/catch
    const listeners = this.events[event].slice(); // Клонируем массив, чтобы избежать проблем,
                                                    // если подписчики изменят его во время итерации
    listeners.forEach(listener => {
      try {
        listener(...args);
      } catch (error) {
        console.error(`Ошибка в обработчике события "${event}":`, error);
        // Можно также решить: throw error; если нужно прервать цепочку,
        // но обычно лучше обрабатывать ошибку локально и продолжать
      }
    });
    return this;
  }
}
```
