Манипуляция DOM (Document Object Model) — это динамическое изменение структуры, содержимого и стилей веб-страницы с помощью JavaScript. Ниже приведён обзор основных методов и подходов, которые используются для работы с DOM, а также примеры их применения.

## 1. Получение элементов

**Методы поиска элементов позволяют выбрать нужные узлы для дальнейшей работы:**

- **`document.getElementById(id)`**  
    Возвращает элемент с указанным значением атрибута `id`.
    ```JS
	    const header = document.getElementById('header');
	```

**`document.getElementsByClassName(className)`**  
Возвращает коллекцию элементов, имеющих указанный класс.  
**Важно:** Возвращает "живую" HTMLCollection.
```JS
const items = document.getElementsByClassName('item');
```

**`document.getElementsByTagName(tagName)`**  
Возвращает коллекцию элементов с указанным тегом.
```JS
const divs = document.getElementsByTagName('div');
```

**`document.querySelector(selector)`**  
Возвращает **первый** элемент, удовлетворяющий CSS-селектору.
```JS
const firstButton = document.querySelector('button.primary');
```

**`document.querySelectorAll(selector)`**  
Возвращает **статическую** (не изменяемую в реальном времени) коллекцию элементов, соответствующих селектору.
```JS
const listItems = document.querySelectorAll('ul li');
```

## 2. Изменение содержимого элементов

- **`innerHTML`**  
    Позволяет получить или задать HTML-содержимое элемента.
	```JS
	const container = document.getElementById('container');
	container.innerHTML = '<p>Новый HTML-контент</p>';
```

**`textContent`**  
Позволяет получить или задать только текстовое содержимое (без HTML-разметки).
```JS
container.textContent = 'Простой текст';
```

## 3. Работа с атрибутами

- **`getAttribute(attributeName)`**  
    Возвращает значение указанного атрибута.
    ```JS
    const link = document.querySelector('a');
	console.log(link.getAttribute('href'));
```

**`setAttribute(attributeName, value)`**  
Устанавливает или обновляет значение атрибута.
```JS
link.setAttribute('target', '_blank');
```

**`removeAttribute(attributeName)`**  
Удаляет указанный атрибут.
```JS
link.removeAttribute('title');
```

**`hasAttribute(attributeName)`**  
Проверяет наличие атрибута.
```JS
if (link.hasAttribute('href')) {
  console.log('Атрибут href присутствует');
}
```

## 4. Управление стилями

- **Inline-стили через свойство `style`:**
```JS
const box = document.getElementById('box');
box.style.width = '200px';
box.style.height = '200px';
box.style.backgroundColor = 'blue';
```

**Работа с классами через `classList`:**  
Методы `add`, `remove`, `toggle`, `contains` позволяют удобно управлять CSS-классами.
```JS
box.classList.add('active');
box.classList.remove('inactive');
box.classList.toggle('highlight');
if (box.classList.contains('active')) {
  console.log('Элемент активен');
}
```

## 5. Создание и изменение структуры DOM

**Основные методы для создания, вставки, удаления и замены узлов:**

- **`document.createElement(tagName)`**  
    Создает новый элемент с указанным тегом.
    ```JS
    const newDiv = document.createElement('div');
	newDiv.textContent = 'Новый элемент';
```

**`document.createTextNode(text)`**  
Создает новый текстовый узел.
```JS
const textNode = document.createTextNode('Пример текста');
```

**`appendChild(newChild)`**  
Добавляет узел в конец списка дочерних элементов.
```JS
const parent = document.getElementById('parent');
parent.appendChild(newDiv);
```

**`insertBefore(newNode, referenceNode)`**  
Вставляет новый узел перед указанным дочерним узлом.
```JS
parent.insertBefore(newDiv, parent.firstChild);
```

**`removeChild(child)`**  
Удаляет указанный дочерний узел из родительского.
```JS
parent.removeChild(newDiv);
```

**`replaceChild(newChild, oldChild)`**  
Заменяет один дочерний узел другим.
```JS
const replacement = document.createElement('span');
replacement.textContent = 'Заменённый элемент';
parent.replaceChild(replacement, newDiv);
```

**`cloneNode(deep)`**  
Создает копию узла. Параметр `true` делает глубокое клонирование (копирует все вложенные узлы).
```JS
const clone = replacement.cloneNode(true);
parent.appendChild(clone);
```

**Современные методы вставки:**  
Помимо классических методов, появились методы `append()`, `prepend()`, `before()`, `after()`, и `replaceWith()`.
```JS
const paragraph = document.createElement('p');
paragraph.textContent = 'Новый параграф';

// Добавление в конец
parent.append(paragraph);

// Добавление в начало
parent.prepend('Начало контейнера ');

// Вставка перед элементом
paragraph.before('Перед параграфом ');

// Вставка после элемента
paragraph.after('После параграфа ');

// Замена элемента на новый
paragraph.replaceWith('Новый контент вместо параграфа');
```

## 6. Навигация по DOM-дереву

- **`parentNode` / `parentElement`**  
    Возвращает родительский узел/элемент.
    ```JS
    const parent = paragraph.parentNode;
```

**`childNodes`**  
Возвращает коллекцию всех дочерних узлов (включая текстовые узлы).
```JS
const children = parent.childNodes;
```

**`children`**  
Возвращает коллекцию только дочерних элементов (без текстовых узлов).
```JS
const elementChildren = parent.children;
```

**`firstChild` / `firstElementChild`**  
Первый дочерний узел или элемент.
```JS
const first = parent.firstElementChild;
```

**`lastChild` / `lastElementChild`**  
Последний дочерний узел или элемент.
```JS
const last = parent.lastElementChild;
```

**`nextSibling` / `nextElementSibling`**  
Следующий соседний узел или элемент.
```JS
const next = paragraph.nextElementSibling;
```

**`previousSibling` / `previousElementSibling`**  
Предыдущий соседний узел или элемент.
```JS
const prev = paragraph.previousElementSibling;
```



## Итог

Манипуляция DOM включает:

- **Получение элементов:** выбор узлов с помощью методов поиска. getElementById, getElementsByClassName, querySelector
- **Изменение содержимого:** работа с `innerHTML`, `textContent`.
- **Изменение атрибутов и стилей:** использование методов `getAttribute`, `setAttribute`, свойства `style`, `classList`.
- **Изменение структуры:** создание, вставка, удаление, замена и клонирование узлов. createElement, newChild
- **Навигация по дереву:** работа с родительскими, дочерними и соседними элементами. parentNode
- **Обработка событий:** добавление и удаление обработчиков событий.