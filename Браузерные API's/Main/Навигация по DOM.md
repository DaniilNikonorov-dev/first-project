### 1. **`document.documentElement`**

- Это свойство возвращает корневой элемент документа (обычно `<html>`), что позволяет работать с ним напрямую.
- Пример:

    `let htmlElement = document.documentElement;`
    

### 2. **`document.body`**

- Это свойство возвращает элемент `<body>`, который содержит основной контент страницы.
- Пример:
    
    javascript
    
    КопироватьРедактировать
    
    `let bodyElement = document.body;`
    

### 3. **`document.head`**

- Это свойство возвращает элемент `<head>`, который содержит метаинформацию страницы (например, ссылки на стили и скрипты).
- Пример:
    
    `let headElement = document.head;`
    

### 4. **Работа с дочерними узлами**

Для того чтобы получить доступ к дочерним элементам родительского узла, используются следующие методы:

- **`parentNode`**: Возвращает родительский элемент текущего узла.
    
    javascript
    
    КопироватьРедактировать
    
    `let parent = childNode.parentNode;`
    
- **`childNodes`**: Возвращает коллекцию всех дочерних узлов, включая текстовые узлы и комментарии.
    
    javascript
    
    КопироватьРедактировать
    
    `let children = parentNode.childNodes;`
    
- **`firstChild`**: Возвращает первый дочерний узел, включая текстовые узлы и комментарии.
    
    javascript
    
    КопироватьРедактировать
    
    `let firstChild = parentNode.firstChild;`
    
- **`lastChild`**: Возвращает последний дочерний узел.
    
    javascript
    
    КопироватьРедактировать
    
    `let lastChild = parentNode.lastChild;`
    

### 5. **Методы для работы с элементами**

В статье также обсуждаются методы, которые позволяют получить элементы и манипулировать ими:

- **`getElementById(id)`**: Возвращает элемент по его `id`.
    
    javascript
    
    КопироватьРедактировать
    
    `let element = document.getElementById('myId');`
    
- **`getElementsByTagName(tagName)`**: Возвращает коллекцию всех элементов с указанным тегом.
    
    javascript
    
    КопироватьРедактировать
    
    `let divs = document.getElementsByTagName('div');`
    
- **`getElementsByClassName(className)`**: Возвращает коллекцию всех элементов с указанным классом.
    
    javascript
    
    КопироватьРедактировать
    
    `let elements = document.getElementsByClassName('myClass');`
    
- **`querySelector(selector)`**: Возвращает первый элемент, соответствующий CSS-селектору.
    
    javascript
    
    КопироватьРедактировать
    
    `let element = document.querySelector('.myClass');`
    
- **`querySelectorAll(selector)`**: Возвращает коллекцию всех элементов, соответствующих CSS-селектору.
    
    javascript
    
    КопироватьРедактировать
    
    `let elements = document.querySelectorAll('div.myClass');`
    

### 6. **Методы для изменения структуры DOM**

- **`appendChild(child)`**: Добавляет дочерний элемент в конец родительского элемента.
    
    javascript
    
    КопироватьРедактировать
    
    `parentNode.appendChild(childElement);`
    
- **`removeChild(child)`**: Удаляет дочерний элемент из родительского элемента.
    
    javascript
    
    КопироватьРедактировать
    
    `parentNode.removeChild(childElement);`
    
- **`replaceChild(newChild, oldChild)`**: Заменяет один дочерний элемент другим.
    
    javascript
    
    КопироватьРедактировать
    
    `parentNode.replaceChild(newElement, oldElement);`
    

### 7. **Свойства `children` и `childNodes`**

- **`children`**: Возвращает коллекцию только **элементов**-дочерних узлов (без текстовых узлов и комментариев).
    
    javascript
    
    КопироватьРедактировать
    
    `let children = parentNode.children;`
    
- **`childNodes`**: Возвращает коллекцию всех дочерних узлов, включая текстовые узлы и комментарии.
    
    javascript
    
    КопироватьРедактировать
    
    `let childNodes = parentNode.childNodes;`
    

### 8. **Упрощение работы с узлами**

- Использование свойств и методов, таких как `firstElementChild` и `lastElementChild`, позволяет обрабатывать только элементы (без текстовых узлов).
    
    javascript
    
    КопироватьРедактировать
    
    `let firstElement = parentNode.firstElementChild; let lastElement = parentNode.lastElementChild;`