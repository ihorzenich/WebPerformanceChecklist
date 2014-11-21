Чек-лист оптимизации скорости загрузки сайта
====================
Инструменты анализа скорости загрузки сайта с выдачей рекомендаций:
* [GTmetrix](http://gtmetrix.com/)
* [Google PageSpeed Insights](https://developers.google.com/speed/pagespeed/insights/)

GTmetrix использует Google Page Speed + Yahoo! YSlow и выдает подробные рекомендации, зато Google PageSpeed Insights проверяет также загрузку на мобильных устройствах.

## Серверное
1. [Включение gzip](http://gtmetrix.com/enable-gzip-compression.html).
2. Включение кеширования генерации страниц движком сайта.
3. Включение кеширования для файлов, отдаваемых сервером:
  1. [Last-Modifed](http://last-modified.com/ru/)
  2. [Expires headers](http://gtmetrix.com/add-expires-headers.html)
  2. [E-tag](https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/http-caching#validating-cached-responses-with-etags)
  3. [Cache-Control](https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/http-caching#cache-control)
  4. [Vary: Accept-Encoding header](https://www.maxcdn.com/blog/accept-encoding-its-vary-important/)
4. Проверка чтоб не было 404-тых откликов на загрузку ресурсов - они замедляют загрузку.

##Верстка
5. Подключение CSS должно быть в HEAD, а JS - в конце HTML, перед </body>
6. Минимизировать кол-во загружаемых файлов:
  1. Использовать CSS-спрайты.
  2. Использовать base64-encode.
  3. Объединять все css в один файл.
  4. Объединять все js в один файл.
  5. Использовать только [WOFF](http://caniuse.com/#search=woff) при подключении web fonts.
7. Отложить загрузку файлов необязательных для первого отображения страницы:
  1. Использовать defer для стороннего js.
  2. [Вынести кнопки соц. шаринга в пост-загрузку](https://github.com/ideus-team/bem-snippets/blob/master/js-socialSharePreload/README.md).
  3. Использовать LazyLoad для картинок.
8. Подгружать js-библиотеки и шрифты с CDN - для использования их версий закешированных с других сайтов и быстрой загрузки с CDN если кеша нет.
9. Перенести внешние баннеры и другие ресурсы подгружаемые со сторонних медленных серверов - на сервер клиента.
10. Минимизировать редиректы для внешних ресурсов (например внешний js отдается не по тому URL, по которому запрашивается, а по редиректу стого URL)
11. Прописать размеры img в html
12. Минимизировать CSS, JS и HTML
13. Оптимизировать графику:
  1. Конвертация типа картинок: 
    - png - для строгих цветов,
    - jpg - для полноцвета и градиентов
    - png24 для прозрачностей. 
    Возможно где-то можно заменить png24 на png8+matte, а где-то на png24 jpg.
  2. Использовать технику [30% quality Retina JPG](http://www.netvlies.nl/blog/design-interactie/retina-revolution). 
  2. Сохранять JPG как progressive
  3. Оптимизировать jpg и png-файлы:
    - с помощью http://compresspng.com/ и http://compressjpeg.com/ (сжимают лучше и быстрей чем консольные утилиты)
    - или с помощь консольных утилит pngout, jpegtrank (в том числе плагинами к Grunt/Gulp)
  4. Перенос визуальных украшений в CSS3 вместо картинок
14. Внести правки в дизайн, удалив тяжеловесные элементы.
15. Желательно удалить query string ("?") в URL отдаваемых ресурсов (некоторые прокси не кешируют их)
