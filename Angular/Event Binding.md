**Event Binding** позволяет отслеживать события DOM (например, `click`, `input`, `change` и т. д.) и выполнять определённые действия в ответ на них. Для этого используется синтаксис `(событие)="выражение"`.

```html
<button (click)="onClick()">Click Me</button>
```

```TS
export class AppComponent {
  onClick() {
    console.log('Button was clicked!');
  }
}
```


2. Передача данных из шаблона
События могут передавать данные, такие как объект `Event`, или настраиваться для передачи пользовательских данных.


Пример с передачей события:
```html
<input (input)="onInput($event)" placeholder="Введите текст">
```

```TS
onInput(event: Event) {
  const inputValue = (event.target as HTMLInputElement).value;
  console.log(inputValue);
}
```


 Пример с передачей пользовательских данных:

``` html
<button (click)="onClick('Hello!')">Click Me</button>
```

``` TS
onClick(message: string) {
  console.log(message);
}
```

