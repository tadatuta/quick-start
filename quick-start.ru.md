# Введение

БЭМ (Блок, Элемент, Модификатор) — методология web—разработки, основанная на представлении страницы в виде совокупности независимых блоков, каждый из которых выражается определенным классом. В основу БЭМ положен принцип компонентного подхода — разделения интерфейса на мелкие части, которые легко разрабатывать, тестировать и поддерживать.

Документ содержит информацию:
* об основных понятиях, их особенностях и принципах;
* об организации файловой структуры БЭМ—проекта.

#  Содержание

* [Блок](#Блок)
 * [Особенности](#Особенности)
 * [Принципы](#Принципы)
* [Элемент](#Элемент)
 * [Особенности](#Особенности)
 * [Принципы](#Принципы)
* [Модификатор](#Модификатор)
 * [Особенности](#Особенности)
 * [Принципы](#Принципы)
* [Микс](#Микс)
* [Файловая система](#Файловая система)


# Блок

Функционально независимый компонент страницы, который может быть повторно использован.

### Особенности

* [Название блока](../naming-convention/naming-convention.ru.md/#Имя-блока) характеризует смысл («что это?» — меню, кнопка…), а не состояние («какой, как выглядит?» — маленький, большой…). Например, `header`, `menu`, `checkbox` и т. п.
* Блок не должен влиять на свое окружение, т. е. блоку не следует задавать внешнюю геометрию (в виде отступов, границ, влияющих на размеры) и position. Таким образом, обеспечивается независимость, при которой удаление логических блоков не нарушает верстку.

**Пример**

```html

    <!-- Пример удачного именования блока. Блок `error` -->
    <div class="error"></div>

    <!-- Пример неудачного именования блока. Блок `red—text` -->  
    <div class="red—text"></div>

```
### Принципы

##### Вложенность

 * Не существует ограничений на вложенность блоков, кроме здравого смысла.
 * Никакой дополнительной специфики вложенные блоки не имеют.

**Пример**

```html

    <div class="header">  <!-- Блок `header`  -->
        <div class="logo"></div>  <!-- Вложенный блок `logo` -->
        <div class="search—form"></div>  <!-- Вложенный блок `search-form` -->
    </div>

```

# Элемент

Составная часть блока, которая не может использоваться в отрыве от него.

 ### Особенности

* [Название элемента](../naming-convention/naming-convention.ru.md/#Имя-элемента) описывает смысл («что это?» — item, text…), а не состояние («какой, как выглядит?» — first, bold…). Например,  `header__title`, `menu__item`, `checkbox__caption`.
* Полное имя элемента создается по схеме: `block—name__elem—name`.

**Пример**

```html

    <div class="search-form">  <!-- Блок `search-form` -->  
        <input class="search-form__input"/>  <!-- Элемент `search-form__input` блока `search-form` -->
        <span class="search-form__button">Найти</span>  <!-- Элемент `search-form__button` блока `search-form` -->
    </div>

```
### Принципы

####  Вложенность

* Элементы как и блоки можно вкладывать друг в друга.
* При любой вложенности элемент — всегда часть блока, а не другого элемента. Это означает, что в названии элементов [нельзя прописывать иерархию вида `block__elem1__elem2`](https://ru.bem.info/methodology/faq/#Почему-в-БЭМ-не-рекомендуется-создавать-элементы-элементов-block__elem1__elem2).

```html

<!-- Верно. Элементы лежат внутри блока `search-form` -->
<div class="search-form">  <!-- Блок `search-form` -->  
    <div class="search-form__content">  <!-- Элемент `search-form__content` блока `search-form` -->
        <input class="search-form__input"/>  <!-- Элемент `search-form__input` блока `search-form` -->
        <span class="search-form__button">Найти</span>  <!-- Элемент `search-form__button` блока `search-form` -->
    </div>
</div>

<!-- Неверно. В БЭМ-методологии не рекомендуется создавать элементы элементов (block__elem1__elem2) -->
<div class="search-form">  <!-- Блок `search-form` -->  
    <div class="search-form__content">  <!-- Элемент `search-form__content` блока `search` -->
        <input class="search-form__content__input"/>  <!-- Элемент `search-form__content__input` элемента `search-form__content` -->
        <span class="search-form__content__button">Найти</span>  <!-- Элемент `search-form__content__button` элемента `search-form__content` -->
    </div>
</div>

```

#### Элемент нельзя использовать вне блока

Элемент — **всегда часть блока** и не должен использоваться вне своего блока.

**Пример**

```html

    <!-- Верно. Элементы лежат внутри блока `search-form` -->
    <div class="search—form">  <!-- Блок `search-form` -->  
        <input class="search-form__input"/>  <!-- Элемент `search-form__input` блока `search-form` -->
        <span class="search-form__button">Найти</span>  <!-- Элемент `search-from__button` блока `search-form` -->
    </div>

    <!-- Неверно. Элементы лежат вне контекста блока `search-form` -->
    <input class="search-form__input"/>  <!-- Элемент `search-form__input` -->
    <span class="search-form__button">Найти</span>  <!-- Элемент `search-form__button` -->  

```

#### Элемент — необязательный компонент блока

Не у всех блоков должны быть элементы. Для наглядности, давайте изменим предыдущий пример с блоком `search-form`.

**Пример**

```html

<!-- Пример с элементами -->
<div class="search—form">  <!-- Блок `search-form` -->  
    <input class="search-form__input"/>  <!-- Элемент `search-form__input` блока `search-form` -->
    <span class="search-form__button">Найти</span>  <!-- Элемент `search-from__button` блока `search-form` -->
</div>

<!-- Пример без элементов -->
<div class="search-form">  <!-- Блок `search-form` -->  
    <input class="input"/>  <!-- Блок `input` -->
    <span class="button">Найти</span>  <!-- Блок `button` -->
</div>

```

>[Когда создавать блок, когда элемент?](https://ru.bem.info/methodology/faq/#В-каком-случае-создавать-блок-в-каком--элемент)


# Модификатор

В некоторых случаях бывает необходимо изменить стиль или поведение конкретного блока либо элемента, т. е. модифицировать его.
Модификатор - это сущность, определяющая внешний вид, состояние или поведение.

### Особенности

* [Название модификатора](../naming-convention/naming-convention.ru.md/#Имя-модификатора) описывает внешний вид («что это?» – «размер»:`size`, «тема»:`theme`, …), состояние («чем отличается от прочих?» – «отключен»:`disabled`, «фокусированный»:`focused`, …) и поведение («что меняется?» – «автоматическое скрытие»:`autoclosable`,         ). Например, `header_fixed`, `menu_disabled`, `checkbox_checked`.

* Полное имя модификатора создается по схеме, для модификаторов:

 * булевого вида — `block(element)-name_mod-name`;
 * вида «ключ-значение» — `block(element)-name_mod-name_mod-val`.


**Пример**

```html

    <div class="search-form search-form_theme_islands">  <!-- Блок `search-form` имеет модификатор `theme` со значением  `islands`-->  
        <input class="search-form__input search-form__input_size_m"/>  <!-- Элемент `search-form__input` имеет модификатор `size` со значением  `m` -->
        <span class="search-form__button search-form__button_disabled">Найти</span>  <!-- Элемент `search-form__button` имеет булевый модификатор `disabled` со значением `true` -->
    </div>

```
### Принципы

#### Модификатор нельзя использовать самостоятельно

С точки зрения БЭМ—методологии модификатор не может использоваться в отрыве от модифицируемого блока или элемента. Модификатор должен изменять вид, поведение сущности, а не заменять ее.

**Пример**

```html

    <!-- Верно! Блок `search-form` имеет модификатр `theme` со значением `islands`-->
    <div class="search-form search-form_theme_islands">
        <input class="search-form__input"/>  
        <span class="search-form__button">Найти</span>  
    </div>
    <!-- Не верно! Отсутствует модифицируемый класс `search-form` -->
    <div class="search-form_theme_islands">  
        <input class="search-form__input"/>  
        <span class="search-form__button">Найти</span>  
    </div>

```

# Микс

Микс - это способ использования разных сущностей на одном DOM-узле.

**Пример**

```html

    <div class="search-form header">  <!-- К блоку `search-form` примиксован блок `header`-->  
        <input class="search-form__input"/>  
        <span class="search-form__button">Найти</span>  
    </div>

```

В данном примере мы совместили поведение и стили блоков `search-form` и `header`. Это очень удобно, так как позволяет применить базовую функциональность блока `search-form` и дополнительные CSS-правила из блока `header` без копирования кода.


# Файловая система

Принятый в методологии БЭМ компонентный подход применяется и к [организации БЭМ—проектов в файловой системе](../filesystem/filesystem.ru.md#Организация-файловой-системы). В БЭМ не только интерфейс делится на независимые компоненты — блоки, но и реализация блоков делится на независимые части — файлы.

### Особенности

* Один блок — одна папка. Для каждого блока создается отдельная директория. Имена блока и его директории совпадают. Например, `header/`, `container/`, `menu/`, `checkbox/`, `input/`.
* Реализация блока разделяется на отдельные одноименные файлы — файлы технологий. Например, `header.css`, `header.js`.
* Директория блока является корневой для поддиректорий соответствующих ему элементов и модификаторов. Например, `header/__logo/`, `container/__content/`, `menu/__item/`, `checkbox/_checked/`, `input/_focused/`.
* Реализации элементов и модификаторов также разделяются на отдельные файлы технологий. Например, `header__input.js`, `header_theme_islands.css`.

**Пример**

```files

search-form/  # Директория блока `search-form`
        __input/  # Поддиректория элемента `search-form__input`
            search-form__input.css  # Реализация элемента `search-form__input` в технологии CSS
            search-form__input.js  # Реализация элемента `search-form__input` в технологии JavaScript
        __button/  # Поддиректория элемента `search-form__button`
            search-form__button.css
            search-form__button.js
        _theme/ # Поддиректория модификатора `search-form_theme`
            search-form_theme_islands.css # Реализация блока `search-form`, имеющего модификатор `theme` со значением `islands` в технологии CSS

search-form.css # Реализация блока `search-form` в технологии CSS
search-form.js # Реализация блока `search-form` в технологии JavaScript

```
