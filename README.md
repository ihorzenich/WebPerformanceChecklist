Чек-лист оптимизации скорости загрузки сайта
====================
Инструменты анализа скорости загрузки сайта с выдачей рекомендаций:
* [GTmetrix](http://gtmetrix.com/)
* [Google PageSpeed Insights](https://developers.google.com/speed/pagespeed/insights/)

GTmetrix использует Google Page Speed + Yahoo! YSlow и выдает подробные рекомендации, зато Google PageSpeed Insights проверяет также загрузку на мобильных устройствах.


## Серверное

1. Включение HTTP2
2. [Включение gzip](http://gtmetrix.com/enable-gzip-compression.html)
3. Включение кеширования генерации страниц движком сайта
4. Включение кеширования для файлов, отдаваемых сервером:
    1. [Last-Modifed](http://last-modified.com/ru/)
    2. [Expires headers](http://gtmetrix.com/add-expires-headers.html)
    2. [E-tag](https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/http-caching#validating-cached-responses-with-etags)
    3. [Cache-Control](https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/http-caching#cache-control)
    4. [Vary: Accept-Encoding header](https://www.maxcdn.com/blog/accept-encoding-its-vary-important/)
5. Проверка чтоб не было 404-тых откликов на загрузку ресурсов - они замедляют загрузку


## Верстка

1. Подключение CSS и JS - в конце HTML, перед `</body>`
6. Автоматически генерировать [критический CSS](https://github.com/addyosmani/critical) и вставлять его через `<style>` в `<head>`
6. Минимизировать кол-во загружаемых файлов (не очень актуально, если есть HTTP2):
    1. Использовать CSS-спрайты
    2. Использовать base64 или [инлайнить svg](https://css-tricks.com/probably-dont-base64-svg/) для небольших изображений
    3. Объединять все css в один файл
    4. Объединять все js в один файл
    5. Использовать только [WOFF2](http://caniuse.com/#search=woff2) и [WOFF](http://caniuse.com/#search=woff) при подключении web fonts. [Подробнее](http://bdadam.com/blog/better-webfont-loading-with-localstorage-and-woff2.html) про подключение.
7. Отложить загрузку данных необязательных для первого отображения страницы:
    1. Использовать defer и async для стороннего js
    2. [Вынести кнопки соц. шаринга в пост-загрузку](https://github.com/ideus-team/bem-snippets/blob/master/js-socialSharePreload/README.md) или загружать их при прокрутке содержимого к ним
    3. Использовать LazyLoad для картинок, но не в ущерб SEO (scr ведет на основную картинку).
    4. Подгружать невидимые при первой загрузке части страницы через AJAX (например содержимое табов) или через `prerender`, [подробнее](https://ymatuhin.ru/front-end/html5-link-prefetch/)
    5. Подгружать через `prerender` блоки неиспользуемые на текущей странице, но будут нужны для следующих
8. Подгружать js-библиотеки и шрифты с CDN - для использования их версий закешированных с других сайтов и быстрой загрузки с CDN если кеша нет
9. Перенести внешние баннеры и другие ресурсы подгружаемые со сторонних медленных серверов - на сервер клиента
10. Минимизировать редиректы для внешних ресурсов (например внешний js отдается не по тому URL, по которому запрашивается, а по редиректу стого URL)
11. Прописать размеры img в html
12. Минимизировать CSS, JS и HTML
13. Оптимизировать графику:
    1. Не грузить на обычный дисплей ретина изображения. Использовать [retinajs](https://github.com/imulus/retinajs) и миксины.
    2. Либо использовать технику [30% quality Retina JPG](http://www.netvlies.nl/blog/design-interactie/retina-revolution)
    3. Конвертация типа картинок:
        - svg (предпочтительней) или png - для векторных изображений, диаграмм, строгих переходов цветов
        - jpg - для полноцвета и градиентов
        - png24 для прозрачностей
        - png8 с альфа-каналом для прозрачностей (через оптимизатор графики http://compresspng.com/)
        Возможно где-то можно заменить png24 на png8+matte, а где-то на jpg
    4. Сохранять JPG как progressive
    5. Оптимизировать jpg и png-файлы:
        - с помощью http://compresspng.com/ и http://compressjpeg.com/ (сжимают лучше и быстрей чем консольные утилиты)
        - или с помощь консольных утилит pngout, jpegtrank (в том числе плагинами к Grunt/Gulp)
    6. Перенос визуальных украшений в CSS3 вместо картинок:
        - например тень у картинки можно сделать через box-shadow, а саму картинку сохранить без тени
    7. Объединять несколько рядом стоящих картинок-ссылок в одну картинку, на которую накладываются позиционированные ссылки
14. Внести правки в дизайн, удалив тяжеловесные элементы
15. Желательно удалить query string ("?") в URL отдаваемых ресурсов (некоторые прокси не кешируют их)
