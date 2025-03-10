
Задача на работу с ng-content. Есть компонент и хотим прокинуть внутри него кнопки:

Прокинуть кнопки (easy)
Из компонента получить кнопки и как-нибудь отразить (например, в шаблоне показать, сколько действий доступно) (easy-medium)
Кроме кнопок прокинуть еще и лейбл с названием, который располагается в другом месте (medium)

```HTML
<!-- код дочернего компонента user-data-form -->
<form>
    <input name="phone" [ngModel]="phone"/>
    <input name="address" [ngModel]="address"/>
</form>
 
<!-- код родительского компонента -->
<user-data-form></user-data-form>
```



Решение

```HTML
<!-- код дочернего компонента user-data-form -->
<ng-content select="title"></ng-content>
<form>
    <input name="phone" [ngModel]="phone"/>
    <input name="address" [ngModel]="address"/>
    <div class="buttons">
        <ng-content select="button"></ng-content>
    </div>
</form>
 
<!-- код родительского компонента -->
<user-data-form>
    <h1 ngProjectAs="title">Заголовок</h1>
    <button>Отмена</button>
    <button>Сохранить</button>
</user-data-form>
```


Решение 2
Родительский
```HTML 
<user-data-form>
  <!-- Кнопки -->
  
<p>
  Всего доступно {{buttons.length}} действий:
</p>

  <button>Save</button>
  <button>Cancel</button>
</user-data-form>
```

Дочерний
```TS
<form> <input name="phone" [ngModel]="phone" /> <input name="address" [ngModel]="address" />

<div class="buttons"> 
		<ng-content></ng-content> 
	</div> 
</form>
```
