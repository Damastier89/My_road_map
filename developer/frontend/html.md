# HTML

- [HTML5](#html5)
- [Doctype](#doctype)
- [Tegs](#tegs)
- [Inline-elements](#inline-elements)
- [Таблицы](#table)
- [Checkbox and Radiobutton](#checkbox-and-radiobutton)
- [BEM](#bem)
- [Meta teg](#meta-teg)
- [Data attribute](#data-attribute)
- [SVG](#svg)
- [Special HTML](#special-html)


### **`HTML5`**
#### HTML5, как сделать верстку семантичной и зачем это нужно.
`Семантическая вёрстка` — подход к разметке, который опирается не на содержание сайта, а на смысловое предназначение каждого блока и логическую структуру документа.
 - Чтобы сделать сайт доступным. (Пример. скринридер, который читает текст со страницы вслух)
 - Чтобы сайт был выше в поисковиках.

[Вернуться к началу статьи](#html)

---

### **`Doctype`**
#### Что такое doctype и зачем он нужен.
`Doctype (Document Type Declaration или DTD)` — это часть html-кода страницы, “инструкция”, которая объявляет тип документа и объясняет браузеру, в какой версии языка разметки он сверстан. 
`Doctype` должен указываться в самом верху документа перед тегом `<html>` .

[Вернуться к началу статьи](#html)

---

### **`Tegs`**
#### Какие есть отличия у тегов div, p, span, a и т.д.
Два самых используемых элемента — `div` и `span` — не имеют семантического значения. 
Они нужны исключительно для структуры и стилей. 
- `<div>` — это блочный `(block-level)` элемент, у него свойство `display: block`. 
- `<span>` — это строчный `(inline-level)` элемент, у него свойство `display: inline`.
- `<p>` — это тег параграфа текста, то есть если нам нужен тег для текста, то мы будем использовать тег `p`.
- `<a>` — является одним из важных элементов HTML и предназначен для создания ссылок. В зависимости от присутствия атрибутов name или `href` тег `<a>` устанавливает ссылку или якорь. Якорем называется закладка внутри страницы, которую можно указать в качестве цели ссылки. При использовании ссылки, которая указывает на якорь, происходит переход к закладке внутри веб-страницы.
  
Синтаксис:
```HTML
    <a href="URL">...</a>
    <a name="идентификатор">...</a>
```
[Вернуться к началу статьи](#html)

---

### **`Inline-elements`**
#### Инлайновые элементы (например, b, i, strong, em).
`Строчные элементы` – это элементы, которые являются частью строки и занимают такое количество пространства, которое необходимо для отображения их содержимого. Строчным элементам нельзя установить размеры `(width и height)`, задать верхние и нижние margin отступы
- `<i>` — был просто курсивом, а сейчас обозначает дополнительное выделение.
- `<b>` — представляет собой фрагмент текста, который выделяется из окружающего его контекста, но не передает никакого особого значения.
- `<em>` — обозначает экспрессивно-эмоциональное выделение (т.е. нечто, произнесённое иначе). 
- `<strong>` — обозначает важность.

[Вернуться к началу статьи](#html)

---

### **`Table`**
#### Как создавать таблицу в html?
Таблица состоит из строк и столбцов ячеек, которые могут содержать текст и рисунки. 
Для добавления таблицы на веб-страницу используется тег `<table>`. 
Этот элемент служит контейнером для элементов, определяющих содержимое таблицы. 
Любая таблица состоит из строк и ячеек, которые задаются соответственно с помощью тегов `<tr>` и `<td>`. 
Таблица должна содержать хотя бы одну ячейку (пример 1). Допускается вместо тега `<td>` использовать тег `<th>`. 
Текст в ячейке, оформленной с помощью тега `<th>`, отображается браузером шрифтом жирного начертания и выравнивается по центру ячейки. 
В остальном разницы между ячейками, созданными через теги `<td>` и `<th>` нет.

```HTML
<!DOCTYPE html>
    <html>
     <head>
          <meta charset="utf-8">
          <title>Тег table</title>
     </head>
     <body>
          <table border="1">
           <tr> <!-- Первый столбец -->
                    <th>Ячейка 1</th> <!-- Заголовок первого столбца -->
                    <th>Ячейка 2</th>
               </tr>
               <tr>
                    <td>Ячейка 3</td> <!-- Ячейка первого столбца -->
                    <td>Ячейка 4</td>
              </tr>
         </table>
     </body>
    </html>
```

```HTML
<!DOCTYPE html>
    <html>
     <head>
      <meta charset="utf-8">
      <title>border-spacing</title>
      <style>
           table {
            border: 4px double #333; /* Рамка вокруг таблицы */ 
            border-collapse: separate; /* Способ отображения границы */ 
            width: 100%; /* Ширина таблицы */ 
            border-spacing: 7px 11px; /* Расстояние между ячейками */ 
           }
           td {
            padding: 5px; /* Поля вокруг текста */ 
            border: 1px solid #a52a2a; /* Граница вокруг ячеек */ 
           }
      </style>
     </head>
     <body>
          <table>
               <tr>
                    <td>1</td>
                    <td>2</td>
               </tr>
               <tr>
                    <td>3</td>
                    <td>4</td>
               </tr>
          </table>
     </body>
    </html>
```
- `rowspan` и `colspan` - Можно растягивать ячейку одновременно и по вертикали, и по горизонтали.
- `table-layout: auto | fixed | inherit` - Определяет, как браузер должен вычислять ширину ячеек таблицы, основываясь на ее содержимом.
- `<caption>` - предназначен для создания заголовка к таблице и может размещаться только внутри контейнера `<table>`, причем сразу после открывающего тега.
```HTML
    <table>
     <caption>Текст</caption>
         <tr>
             <td>...</td>
         </tr>
    </table>
```
Атрибут `scope` - связывает между собой ячейки с заголовком и обычные ячейки. 
По своему действию напоминает атрибут headers, но используется для простых таблиц. 
Атрибут предназначен для экранных ридеров вроде речевых браузеров, в обычных браузерах результат добавления scope никак не заметен.

- `display: table` - Означает: «веди себя как таблица». По умолчанию этим значением обладает html-элемент table, он же таблица.
- `display: inline-table` - Ровно то же самое, что и предыдущее значение, только наша псевдотаблица может располагаться на одной строке с другими строчными элементами. К строчной таблице применимо вертикальное выравнивание (свойство vertical-align).
- `display: table-row` - Означает: «Веди себя как табличная строка». По умолчанию таким элементом является tr. Свойства табличной строки:
  - имеет ширину по содержанию, но занимает целую строку;
  - задать строке таблицы ширину нельзя, зато можно задать высоту;
  - к табличной строке неприменимы поля, отступы, рамки и управление ими, а также вертикальное выравнивание;
  - зато по горизонтали (text-align) содержание табличных строк выравнивать можно.
- `display: table-cell` - На мой взгляд, самое интересное из табличных значений display. Означает: «Веди себя как ячейка таблицы». По умолчанию это значение имеют элементы td и th. Свойства табличных ячеек и элементов со значением display: table-cell:
  - идущие подряд ячейки находятся на одной строке с себе подобными, не переходя на следующую; если ячейкам на строке тесно, они сначала ужимаются по ширине, а затем начинают распяливать контейнер и/или окно браузера;
  - ширина ячеек по умолчанию распределяется пропорционально содержанию (с учётом всех ячеек в данной строке), однако может прямо задаваться через css;
  - все ячейки в строке имеют одинаковую высоту, которая определяется содержанием самой большой ячейки в данной строке;
  - ячейка может иметь внутренние отступы (padding), но не может иметь полей (margin);
    к табличным ячейкам применимо вертикальное выравнивание по табличному принципу: свойство vertical-align выравнивает содержание ячейки по высоте относительно самой ячейки, при этом ячейки в строке сохраняют одинаковую высоту, в отличие от строчных или строчно-блочных элементов. Значения vertical-align не бывают отрицательными;
  - содержание ячейки может выравниваться по горизонтали (text-align);
  - у ячейки может быть рамка, но чтобы повлиять на слияние/расклеивание рамок, надо соответствующие свойства назначать контейнеру, а не текущему элементу; кстати, в старых версиях Оперы у элементов со значением table-cell значение border-spacing почему-то было ненулевым и создавало лишние зазоры, в силу чего таким элементам требовалось правило border-collapse: collapse; сейчас этого, вроде бы, не наблюдается.
- `display: table-column` - «Веди себя как табличная графа (колонка, столбец)». Таким элементом в html является редко применяемый элемент col. Через css можно указать фон, рамку, ширина, видимость (visivility); в IE нет рамки и видимости.
- `display: table-column-group` - Соответствует группе граф colgroup. По поведению совпадает с предыдущим типом.
- `display: table-header-group, table-footer-group, table-row-group` - Это группы строк, которым соответствуют элементы thead, tfoot и tbody соответственно, то есть группа шапки, группа подвала и группа основной части таблицы

[Вернуться к началу статьи](#html)

---

### **`Checkbox and Radiobutton`**
#### В чем заключаются отличие чекбокса от радио кнопок?
RadioButton и CheckBox элементы управления имеют аналогичную функцию: они предлагают варианты выбора, 
которые пользователь может выбрать или очистить. 
Разница заключается в том, что одновременно можно выбрать несколько `CheckBox` элементов управления, но кнопки `RadioButton` являются взаимоисключающими.

Для создания радиокнопки, так же как и чекбокса, используются два тега:

- `<input>` с указанием `type="radio"`. Обязательным атрибутом является name, значением которого является имя. Данное имя должно быть одинаковым у всей группы радиокнопок. Без этого атрибута будет возможно выбрать все значения сразу, так как браузер не будет видеть связи между ними
- `<label>`, в котором будет текст, связанный с нужной нам радиокнопкой.
- Связь `<input>` с `<label>` происходит уже по одному из двух знакомых нам сценариев:
  - Связь по `id`. Для этого необходимо задать уникальный `id` для `<input>`, и связать `<label>` с радиокнопкой с помощью атрибута `for`
```HTML
  <form>
    <input id="yes" type="radio" name="question">
    <label for="yes">Да</label>

    <input id="no" type="radio" name="question">
    <label for="no">Нет</label>
  </form>
```

- Вложить `<input>` внутрь тега `<label>`. При этом указание уникального id не требуется.
```HTML
  <form>
    <label>
        <input type="radio" name="question">
        Да
    </label>
    <br>
    <label>
        <input type="radio" name="question">
        Нет
    </label>
</form>
```

[Вернуться к началу статьи](#html)

---

### **`BEM`**
`БЭМ (Блок, Элемент, Модификатор)` — компонентный подход к веб-разработке. 
В его основе лежит принцип разделения интерфейса на независимые блоки. 
Он позволяет легко и быстро разрабатывать интерфейсы любой сложности и повторно использовать существующий код, избегая «Copy-Paste».

#### **`Блок`**
Функционально независимый компонент страницы, который может быть повторно использован. 
В HTML блоки представлены атрибутом class.
 - Название блока характеризует смысл `(«что это?» — «меню»: menu, «кнопка»: button)`, а не состояние `(«какой, как выглядит?» — «красный»: red, «большой»: big)`.

```HTML
    <!-- Верно. Семантически осмысленный блок `error` -->
    <div class="error"></div>
    
    <!-- Неверно. Описывается внешний вид -->
    <div class="red-text"></div>
```

- Блок не должен влиять на свое окружение, т. е. блоку не следует задавать внешнюю геометрию (в виде отступов, границ, влияющих на размеры) и позиционирование.
- В CSS по БЭМ также не рекомендуется использовать селекторы по тегам или id.
- Блоки можно вкладывать друг в друга.
- Допустима любая вложенность блоков.

```HTML
    <!-- Блок `header` -->
    <header class="header">
        <!-- Вложенный блок `logo` -->
        <div class="logo"></div>
    
        <!-- Вложенный блок `search-form` -->
        <form class="search-form"></form>
    </header>
```

#### **`Элемент`**
Составная часть блока, которая не может использоваться в отрыве от него.
 - Название элемента характеризует смысл `(«что это?» — «пункт»: item, «текст»: text)`, а не состояние `(«какой, как выглядит?» — «красный»: red, «большой»: big)`.
 - Структура полного имени элемента соответствует схеме: `имя-блока__имя-элемента`. Имя элемента отделяется от имени блока двумя подчеркиваниями (__).

```HTML
    <!-- Блок search-form-->
    <form class="search-form">
    <!-- Элемент input блока search-form-->
    <input class="search-form__input">\

    <form class="search-form">
        <div class="search-form__content">
            <input class="search-form__input">
            <button class="search-form__button">Найти</button>
        </div>
    </form>
```

- Элемент — всегда часть блока и не должен использоваться отдельно от него.
- Элемент — необязательный компонент блока. Не у всех блоков должны быть элементы.
- Элементы можно вкладывать друг в друга.
- Допустима любая вложенность элементов
- Создавайте блок - если фрагмент кода может использоваться повторно и не зависит от реализации других компонентов страницы.
- Создавайте элемент - если фрагмент кода не может использоваться самостоятельно, без родительской сущности (блока).

```HTML
    <!-- Верно. Структура полного имени элементов соответствует схеме: `имя-блока__имя-элемента` -->
    <form class="search-form">
        <div class="search-form__content">
            <input class="search-form__input">
            <button class="search-form__button">Найти</button>
        </div>
    </form>
    
    <!-- Неверно. Структура полного имени элементов не соответствует схеме: `имя-блока__имя-элемента` -->
    <form class="search-form">
        <div class="search-form__content">
            
            <!-- Рекомендуется:`search-form__input` или `search-form__content-input` -->
            <input class="search-form__content__input">
            
            <!-- Рекомендуется: `search-form__button` или `search-form__content-button` -->
            <button class="search-form__content__button">Найти</button>
        </div>
    </form>
```
#### **`Модификатор`**
Cущность, определяющая внешний вид, состояние или поведение блока либо элемента.
 - Название модификатора характеризует внешний вид `(«какой размер?», «какая тема?» и т. п. — «размер»: size_s, «тема»: theme_islands)`, 
состояние `(«чем отличается от прочих?» — «отключен»: disabled, «фокусированный»: focused)` 
и поведение `(«как ведет себя?», «как взаимодействует с пользователем?» — «направление»: directions_left-top)`.

#### Типы модификаторов
#### Булевый
- Используют, когда важно только наличие или отсутствие модификатора, а его значение несущественно. 
Например, «отключен»: disabled. Считается, что при наличии булевого модификатора у сущности его значение равно true.
Имя модификатора отделяется от имени блока или элемента одним подчеркиванием (_).
- Структура полного имени модификатора соответствует схеме:
  - имя-блока_имя-модификатора;
  - имя-блока__имя-элемента_имя-модификатора;

```HTML
    <!-- Блок `search-form` имеет булевый модификатор `focused` -->
    <form class="search-form search-form_focused">
        <input class="search-form__input">
    
        <!-- Элемент `button` имеет булевый модификатор `disabled` -->
        <button class="search-form__button search-form__button_disabled">Найти</button>
    </form>
```

#### Ключ-значение
- Используют, когда важно значение модификатора. 
Например, «меню с темой оформления islands»: `menu_theme_islands`.
- Структура полного имени модификатора соответствует схеме:
  - имя-блока_имя-модификатора_значение-модификатора;
  - имя-блока__имя-элемента_имя-модификатора_значение-модификатора.

```HTML
    <!-- Блок `search-form` имеет модификатор `theme` со значением `islands` -->
    <form class="search-form search-form_theme_islands">
        <input class="search-form__input">
    
        <!-- Элемент `button` имеет модификатор `size` со значением `m` -->
        <button class="search-form__button search-form__button_size_m">Найти</button>
    </form>
    
    <!-- Невозможно одновременно использовать два одинаковых модификатора с разными значениями -->
    <form class="search-form
                 search-form_theme_islands
                 search-form_theme_lite">
    
        <input class="search-form__input">
    
        <button class="search-form__button
                       search-form__button_size_s
                       search-form__button_size_m">
            Найти
        </button>
    </form>
```
- Модификатор нельзя использовать самостоятельно. 
- С точки зрения БЭМ-методологии модификатор не может использоваться в отрыве от модифицируемого блока или элемента. 
- Модификатор должен изменять вид, поведение или состояние сущности, а не заменять ее.

[Вернуться к началу статьи](#html)

---

### **`Meta teg`**
#### Зачем нужны метатеги?
Чтобы SEO-продвижение было максимально эффективным и экономичным, рекомендуется использовать основные и дополнительные метатеги.
Метатеги (от англ. meta tags) - это элементы (html-теги) веб страницы, используемые для передачи структурированных метаданных, как правило, размещаются в разделе <head> веб-документа.

- Title - является базовым элементом HTML разметки, по которой поисковые системы и пользователи могут определить тематику и содержание контента страницы онлайн ресурса.;
- Description - (мета-описание) предназначен для быстрого ознакомления пользователей с содержанием страницы в поисковой выдаче;
- Keywords - метатег, который, согласно официальным заявлениям представителей поисковых систем, более не учитывается алгоритмами Яндекс и Google при ранжировании.;
- Content-type -  это заголовок-сущность, предназначенный для определения media type онлайн ресурса. Этот заголовок показывает тип файла (аудиофайл - audio/ogg, изображение - image/png). Данные необходимы для интернет сервисов, обрабатывающих разные форматы файлов (графические, аудио или видео)


[Вернуться к началу статьи](#html)

---

### **`Data attribute`**
#### Что такое data-атрибуты?
Дата-атрибут — это пользовательский атрибут на элементе, название которого начинается с data-, например data-testid. 
Дата атрибуты используются, чтобы хранить значения на элементах в HTML.

```HTML
<h1>Известные ситхи</h1>
<ul>
    <li data-id="1541" data-episode="1">Дарт Мол</li>
    <li data-id="9434" data-episode="4">Дарт Вейдер</li>
    <li data-id="5549" data-episode="4">Дарт Сидиус</li>
</ul>
```
```JS
    console.log(document.querySelector('[data-episode="1"]').nextSibling); // получить node
    console.log(document.querySelector('[data-episode="4"]').nextElementSibling); // получить элемент
```

[Вернуться к началу статьи](#html)

---

### **`SVG`**
#### Как стилизовать svg?
#### Основные атрибуты

- `xmlns="http://www.w3.org/2000/svg"` — данный атрибут прописывает путь к стандарту svg, в котором описана эта иконка
- `viewBox="0 0 512 512"` — указывает на ту область иконки, которую мы видим в браузере
- `class="twitter-icon"` — как и другим элементам, можно задать класс и стилизовать по нему в CSS файле
- `width="256" height="256"` — при помощи этих атрибутов можно настраивать размер иконки

#### Атрибуты fill, stroke, stroke-width в SVG
Эти атрибуты можно применить к тегу <svg> и тогда они распространятся на всю иконку. 
А можно применить к отдельному <path> — тогда они будут работать только в области, описанной в конкретном <path>.

- `fill="red"` — заливка цветом
- `stroke="green"` — цвет обводки
- `stroke-width="10"` — толщина обводки

[Вернуться к началу статьи](#html)

---

### **`Special HTML`**
#### Что такое специальные html-сущности (неразрывный пробел, длинное тире) и как с ними работать?

Основное назначение неразрывного пробела `(&nbsp ;)` `(от non-breaking space)` — разделять слова, но запрещать в этом месте переход на новую строку.

Неразрывной пробел нужен когда:
- фамилии с инициалами;
- длинные тире с предшествующим им словом;
- односложные слова с последующим словом;
- цифры с последующими единицами измерения

[Вернуться к началу статьи](#html)

---