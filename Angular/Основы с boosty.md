Пример реализации создания потока

```
  constructor(){

    this.formControl.valueChanges

      .pipe( - подкапотный метод

        filter(val => val.lenght >3),

        debounceTime(500)

      )

      .subscribe(val => console.log(val)) - подписка и вывод в консоль 

  }
  ```````

Observable - наблюдаемый объект на который мы можем подписаться 


```
  constructor(){
    fromEvent(document.body, 'click') - создаем отслеживаемый ивент
    .pipe( - в пайпе какие либо манипуляции
      map (() => 123) 
    )
    .subscribe(val => { - происходит подписка на поток
      console.log(val)
    }
    )
    const obs = new Observable((subscriber) => { - подписка на поток
      subscriber.next(1)
      subscriber.next(2)
      subscriber.next(3)
      subscriber.next(4)
      // subscriber.error() - вызов ошибки
      subscriber.next(4)
      return () => {
        console.log('Destr') - возврат при отписке \ ошибке
      }
    })
    const sub = obs.subscribe(val => console.log(val))
    setTimeout(()=> {
      sub.unsubscribe() - отписываемся от потока
    },3000)
  }
```



Обработчик событий
```
function customFromEvent(el: HTMLElement, eventName: string) { - получает HTML эелмент и событие

  return new Observable( subscriber => { - будет возвращать подписку на этот обс

    const handleEvent = (e: Event) => subscriber.next(e) - что будет происходит при каждом ивенте ( мы передаем собсрайберу ивент)

    el.addEventListener(eventName, handleEvent)

  })

}
````

что такое addEventListener ?


