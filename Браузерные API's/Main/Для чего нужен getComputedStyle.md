`getComputedStyle` – это метод, который возвращает объект типа `CSSStyleDeclaration`, содержащий **вычисленные** стили элемента. Он показывает итоговые значения стилей после применения всех CSS-правил (включая внешние таблицы стилей, inline-стили, унаследованные свойства и т.д.). Это особенно полезно, если вам нужно узнать, как браузер отобразил элемент в итоговом варианте.

**Примеры использования:**
- Получить итоговый цвет текста
```JS
const element = document.querySelector('.my-element');
const styles = window.getComputedStyle(element);
console.log(styles.color); // например, "rgb(255, 0, 0)"
```

