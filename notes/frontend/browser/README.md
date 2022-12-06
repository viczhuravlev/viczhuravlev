# JavaScript

## API

### IntersectionObserver
Используется для скролл анимаций, инфинити скролла или слежением за какими то объектом во время скролла.

```js
const elements = document.querySelectorAll(".observable");
const observer = new IntersectionObserver((entries, observer) => {
    /**
     * your magic
     */
}, {
    root: document.body,
    threshold: 1,
    rootMargin: 1,
})

elements.forEach((el) => observer.observe(el));;
```

#### Config

> `threshold` - свойство, которое используется для определения того, какая часть элемента уже видна и позволяет вызвать действие наблюдателя.
> Значение между 0 и 1 и это эквивалентно 0%-100%. По умолчанию 0.

> `rootMargin` - тоже самое, что и css margin.

> `root` - используется для установки границы точки обзора в виде размера элемента. Это должен быть один из наблюдаемых элементов и может быть полезно для контейнеров с прокруткой.

#### Methods

`unobserve()` - Метод  используется, чтобы остановить IntersectionObserver от наблюдения за элементом, когда он уже наблюдался. Для ленивой загрузки изображений это может решить многие проблемы и ошибки.

`disconnect()` - похож на метод unobserve, но он полностью отключает все.
