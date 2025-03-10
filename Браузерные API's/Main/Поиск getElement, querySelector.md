https://learn.javascript.ru/searching-elements-dom

## [document.getElementById или просто id](https://learn.javascript.ru/searching-elements-dom#document-getelementbyid-ili-prosto-id)

Если у элемента есть атрибут `id`, то мы можем получить его вызовом `document.getElementById(id)`, где бы он ни находился.
## [querySelectorAll](https://learn.javascript.ru/searching-elements-dom#querySelectorAll)

Самый универсальный метод поиска – это `elem.querySelectorAll(css)`, он возвращает все элементы внутри `elem`, удовлетворяющие данному CSS-селектору.
Следующий запрос получает все элементы `<li>`, которые являются последними потомками в `<ul>`:
```JS
let elements = document.querySelectorAll('ul > li:last-child');
```

## [querySelector](https://learn.javascript.ru/searching-elements-dom#querySelector)

Метод `elem.querySelector(css)` возвращает первый элемент, соответствующий данному CSS-селектору.
Иначе говоря, результат такой же, как при вызове `elem.querySelectorAll(css)[0]`, но он сначала найдёт _все_ элементы, а потом возьмёт первый, в то время как `elem.querySelector` найдёт только первый и остановится. Это быстрее, кроме того, его короче писать.

## [matches](https://learn.javascript.ru/searching-elements-dom#matches)

Предыдущие методы искали по DOM.
Метод [elem.matches(css)](https://dom.spec.whatwg.org/#dom-element-matches) ничего не ищет, а проверяет, удовлетворяет ли `elem` CSS-селектору, и возвращает `true` или `false`. Этот метод удобен, когда мы перебираем элементы (например, в массиве или в чём-то подобном) и пытаемся выбрать те из них, которые нас интересуют.

## [closest](https://learn.javascript.ru/searching-elements-dom#closest)

_Предки_ элемента – родитель, родитель родителя, его родитель и так далее. Вместе они образуют цепочку иерархии от элемента до вершины.

Метод `elem.closest(css)` ищет ближайшего предка, который соответствует CSS-селектору. Сам элемент также включается в поиск.

Другими словами, метод `closest` поднимается вверх от элемента и проверяет каждого из родителей. Если он соответствует селектору, поиск прекращается. Метод возвращает либо предка, либо `null`, если такой элемент не найден.