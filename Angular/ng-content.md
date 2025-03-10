**`ng-content`** в Angular — это специальный инструмент, который позволяет реализовать **[[контентную проекцию]]**. Он используется для вставки пользовательского содержимого в шаблон компонента. Это особенно полезно при создании переиспользуемых компонентов.

`ng-content` acts as a placeholder для контента, передаваемого между тегами компонента. Контент, переданный в тег компонента, автоматически вставляется в место, где находится `<ng-content>`.

### Пример:

#### Шаблон родительского компонента:

```HTML
<app-card>
  <h2>Заголовок</h2>
  <p>Это содержимое будет передано в app-card.</p>
</app-card>
```

Шаблон дочернего компонента (`app-card`):
```HTML
<div class="card">
  <ng-content></ng-content>
</div>
```




**`Селективная проекция`**

Вы можете управлять тем, какой контент куда вставлять, используя **CSS-селекторы** внутри `ng-content`.

#### Пример:

##### Шаблон родителя:
```HTML
<app-card>
  <h2 title>Заголовок</h2>
  <p>Основной текст</p>
</app-card>
```

Шаблон дочернего компонента:

```HTML
<div class="card">
  <header>
    <ng-content select="[title]"></ng-content>
  </header>
  <section>
    <ng-content></ng-content>
  </section>
</div>
```


**`Множественная проекция`**

Вы можете использовать несколько `<ng-content>` с разными селекторами, чтобы распределить контент по различным частям шаблона.

#### Пример:

##### Шаблон родителя:
```HTML
<app-layout>
  <h1 header>Заголовок страницы</h1>
  <p>Основной контент</p>
  <footer>Футер</footer>
</app-layout>
```

##### Шаблон дочернего компонента:
<div class="layout">
  <header>
    <ng-content select="[header]"></ng-content>
  </header>
  <main>
    <ng-content></ng-content>
  </main>
  <footer>
    <ng-content select="footer"></ng-content>
  </footer>
</div>
<div class="layout">
  <header>
    <ng-content select="[header]"></ng-content>
  </header>
  <main>
    <ng-content></ng-content>
  </main>
  <footer>
    <ng-content select="footer"></ng-content>
  </footer>
</div>
<div class="layout">
  <header>
    <ng-content select="[header]"></ng-content>
  </header>
  <main>
    <ng-content></ng-content>
  </main>
  <footer>
    <ng-content select="footer"></ng-content>
  </footer>
</div>
<div class="layout">
  <header>
    <ng-content select="[header]"></ng-content>
  </header>
  <main>
    <ng-content></ng-content>
  </main>
  <footer>
    <ng-content select="footer"></ng-content>
  </footer>
</div>
<div class="layout">
  <header>
    <ng-content select="[header]"></ng-content>
  </header>
  <main>
    <ng-content></ng-content>
  </main>
  <footer>
    <ng-content select="footer"></ng-content>
  </footer>
</div>

<div class="layout">
  <header>
    <ng-content select="[header]"></ng-content>
  </header>
  <main>
    <ng-content></ng-content>
  </main>
  <footer>
    <ng-content select="footer"></ng-content>
  </footer>
</div>
<div class="layout">
  <header>
    <ng-content select="[header]"></ng-content>
  </header>
  <main>
    <ng-content></ng-content>
  </main>
  <footer>
    <ng-content select="footer"></ng-content>
  </footer>
</div>
```HTML
<div class="layout">
  <header>
    <ng-content select="[header]"></ng-content>
  </header>
  <main>
    <ng-content></ng-content>
  </main>
  <footer>
    <ng-content select="footer"></ng-content>
  </footer>
</div>
```



