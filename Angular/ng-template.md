**`ng-template`** в Angular — это директива, которая определяет фрагмент шаблона, который не отображается сразу. Вместо этого он может быть динамически загружен или использован по мере необходимости. Этот инструмент полезен для ленивой загрузки контента, кастомных отображений и структурных директив.


## **Основные особенности `ng-template`**

1. **Не отображается в DOM до активации**:
    - Контент внутри `ng-template` не добавляется в DOM, пока не будет явно отрисован.

1. **Используется для структурных директив**:
    - Такие директивы, как `*ngIf`, `*ngFor`, автоматически создают `ng-template`.

2. **Динамическое отображение шаблонов**:
    - Через `TemplateRef` и `ViewContainerRef` можно динамически управлять отображением шаблонов.

Синтаксис `ng-template`

```HTML
<ng-template #myTemplate>
  <p>Это содержимое внутри ng-template.</p>
</ng-template>
```

## Примеры использования `ng-template`
`ng-template` можно использовать для отображения контента по условию.

```HTML
<button (click)="show = !show">Переключить</button>

<ng-container *ngIf="show">
  <ng-template>
    <p>Контент отображен!</p>
  </ng-template>
</ng-container>
```


2. Динамическое использование через `ViewContainerRef`
``` HTML
<ng-template #template>
  <p>Контент добавлен динамически!</p>
</ng-template>

<button (click)="addTemplate()">Добавить контент</button>
```

Логика компонента:
```TS
import { Component, TemplateRef, ViewChild, ViewContainerRef } from '@angular/core';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
})
export class AppComponent {
  @ViewChild('template', { read: TemplateRef }) templateRef!: TemplateRef<any>;
  constructor(private viewContainerRef: ViewContainerRef) {}

  addTemplate() {
    this.viewContainerRef.createEmbeddedView(this.templateRef);
  }
}
```
