# Паттерны и флаги

Регулярные выражения –- мощное средство поиска и замены в строке. 

В JavaScript регулярные выражения реализованы отдельным объектом `RegExp` и интегрированы в методы строк.
[cut]

## Регэкспы

Регулярное выражение (оно же "регэксп", "регулярка" или просто "рег"), состоит из *паттерна* (он же "шаблон") и необязательных *флагов*.

Синтаксис создания регулярного выражения:

```js
var regexp = new RegExp("шаблон", "флаги");
```

Как правило, используют более короткую запись: шаблон внутри слешей `"/"`:

```js
var regexp = /шаблон/; // без флагов
var regexp = /шаблон/gmi; // с флагами gmi (изучим их дальше)
```

Слэши `"/"` говорят JavaScript о том, что это регулярное выражение. Они играют здесь ту же роль, что и кавычки для обозначения строк.

## Использование

Основа регулярного выражения -- паттерн. Это строка, которую можно расширить специальными символами, которые делают поиск намного мощнее.

В простейшем случае, если флагов и специальных символов нет, поиск по паттерну -- то же самое, что и обычный поиск подстроки:

```js
//+ run
var str = "Я люблю JavaScript!"; // будем искать в этой строке

var regexp = /лю/;
alert( str.search(regexp) ); // 2
```

Сравните с обычным поиском:

```js
//+ run
var str = "Я люблю JavaScript!";

var substr = "лю";
alert( str.indexOf(substr) ); // 2
```

Как видим, то же самое, разве что для регэкспа использован метод [search](https://developer.mozilla.org/ru/docs/Web/JavaScript/Reference/Global_Objects/String/search) -- он как раз работает с регулярными выражениями, а для подстроки -- [indexOf](https://developer.mozilla.org/ru/docs/Web/JavaScript/Reference/Global_Objects/String/indexOf). 

Но это соответствие лишь кажущееся. Очень скоро мы усложним регулярные выражения, и тогда увидим, что они гораздо мощнее.

[smart header="Цветовые обозначения"]
Здесь и далее в тексте используется следующая цветовая схема:
<ul>
<li>регэксп (регулярное выражение) - <code class="pattern">красный</code></li>
<li>строка - <code class="subject">синий</code></li>
<li>результат - <code class="match">зеленый</code></li>
</ul>
[/smart]

## Флаги

Регулярные выражения могут иметь флаги, которые влияют на поиск. 

В JavaScript их всего три:

<dl>
<dt>`i`</dt>
<dd>Если этот флаг есть, то регэксп ищет независимо от регистра, то есть не различает между `А` и `а`.</dd>
<dt>`g`</dt>
<dd>Если этот флаг есть, то регэксп ищет все совпадения, иначе -- только первое.</dd>
<dt>`m`</dt>
<dd>Многострочный режим.</dd>
</dl>

Самый простой для понимания из этих флагов -- безусловно, `i`. 

Пример его использования:

```js
//+ run
var str = "Я люблю JavaScript!"; // будем искать в этой строке
 
alert( str.search( *!*/ЛЮ/*/!* ) ); // -1
alert( str.search( *!*/ЛЮ/i*/!* ) ); // 2
```

<ol>
<li>С регом <code class="pattern">/ЛЮ/</code> вызов вернул `-1`, что означает "не найдено" (как и в `indexOf`),</li>
<li>С регом <code class="pattern">/ЛЮ/i</code> вызов нашёл совпадение на позиции 2, так как стоит флаг `i`, а значит "лю" тоже подходит.</li>
</ol>

Другие флаги мы рассмотрим в последующих главах.

## Итого

<ul>
<li>Регулярное выражение состоит из шаблона и необязательных флагов `g`, `i` и `m`.</li>
<li>Поиск по регулярному выражению без флагов и спец. символов, которые мы изучим далее -- это то же самое, что и обычный поиск подстроки в строке. Но флаги и спец. символы, как мы увидим далее, могут сделать его гораздо мощнее.</li>
<li>Метод строки `str.search(regexp)` возвращает индекс, на котором найдено совпадение.</li>
</ul>