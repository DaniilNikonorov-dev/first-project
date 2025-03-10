```TS
// Создаём экземпляр наблюдателя с указанной функцией колбэка
const observer = new MutationObserver(callback);
 
// Начинаем наблюдение за настроенными изменениями целевого элемента
observer.observe(target, config);
 
// Позже можно остановить наблюдение
observer.disconnect();
```
По аналогии с функцией fromEvent, надо создать функцию fromMutationObserver(target, config), которая возвращает Observable, который на каждое событие из  MutationObserver эмитит это событие

Обязательно предусмотреть остановку MutationObserver, когд он уже не нужен

```TS

function fromMutationObserver(target: Node, options?: MutationObserverInit): Observable<[MutationRecord[], MutationObserver]> {
    return new Observable((subscriber: Subscriber<[MutationRecord[], MutationObserver]>) => {
        const observer = new MutationObserver((mutations: MutationRecord[], mutationObserver: MutationObserver) =>
            subscriber.next([mutations, mutationObserver]),
        );
 
        observer.observe(target, options);
 
        return () => observer.disconnect();
    });
}
```

