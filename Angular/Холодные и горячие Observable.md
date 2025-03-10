Холодные observable - uniq casting - передает данные кому то одному, если к нему подпишется кто - то другой, данные могут различаться

```
function random () {
  return new Observable( subs => {
  const random = Math.random(); - находится вне Observable - находится внутри Observable
    subs.next(random)
  })
}
```

Горячие Observable - multi casting - передает данные многим и они не будут отличаться. 

```
function random () {
  const random = Math.random(); - находится вне Observable
  return new Observable( subs => {
    subs.next(random)
  })
}
```
Различия в создании замыкания в функции подписки Observable, где происходит создание данных

Сделать из холодного - горячий можно при помощи shareReplay и пайпа
```
const obs = random().pipe(shareReplay())`
```


# Порождающие операторы

## of 
```
const observable$ = of(1,2,3,4,5)

console: 
next 1
app.component.ts:152 next 2
app.component.ts:152 next 3
app.component.ts:152 next 4
app.component.ts:152 next 5
app.component.ts:154 compete
```

## from 
```
const observable$ = from([1,2,3,4,5])
console: 
next 1
app.component.ts:152 next 2
app.component.ts:152 next 3
app.component.ts:152 next 4
app.component.ts:152 next 5
app.component.ts:154 compete
```
Пытается из всего сделать поток, можно передать Promise с помощью fetch.
Делает из Promise Observable. 


## interval 
```
const observable$ = interval(1000)
next 0
app.component.ts:152 next 1
app.component.ts:152 next 2
app.component.ts:152 next 3
app.component.ts:152 next 4
app.component.ts:152 next 5
app.component.ts:152 next 6
app.component.ts:152 next 7
app.component.ts:152 next 8
app.component.ts:152 next 9
app.component.ts:152 next 10
app.component.ts:152 next 11
app.component.ts:152 next 12
app.component.ts:152 next 13
app.component.ts:152 next 14
app.component.ts:152 next 15
app.component.ts:152 next 16
app.component.ts:152 next 17
app.component.ts:152 next 18
app.component.ts:152 next 19
app.component.ts:152 next 20
app.component.ts:152 next 21
```
Выполняет запрос с определенным интервалом


## timer
```
const observable$ = timer(1000)
next 0
app.component.ts:154 compete
```
Выполняет запрос  1 раз через определенный интервал 
Но, можно дописать конструкцию в вид
```
const observable$ = timer(3000, 1000)`
```
чтобы началось выполнение через 3 секунду, с ==интервалом== в секунду


<h2> fromEvent</h2>
```
const observable$ = fromEvent( document.body, 'click')`
```


<h2>throwError</h2>
```
const observable$ = throwError(() => 123)
```


# Фильтрующие операторы
<h2>Filter</h2>
``` 
      .pipe(
        filter(val => val<5)
      )
```
Значение должно вернуть true, чтобы мы его пустили

## take

```
      .pipe(
        take(3)
      )
```
Берет первые значения , чтобы взять первое значения - использовать оператор first()

## skip

```
      .pipe(
        skip(10)
      )
```
Пропустит первые 10 значений


  
## pipe
 ```
      .pipe(
        find(val => val===3)
      )
``` 
Ищет в потоке инфу по условию



## distinctUntilChanged
```
      .pipe(

        // filter(val => val <5)

        // take(19)

        // skip(3)

        // find(val => val===123)

        distinctUntilChanged()

      )
```
Отсеивает все одинаковые элементы, ЕСЛИ они идут подряд


## tap
Используется для дебагга, идет по шагам

## debounceTime
Делает перерыв перед последним нажатием, как отправить данные 



## throttleTime
не дает спамить