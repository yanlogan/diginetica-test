1. Каким будет результат следующей операции на языке JavaScript:

```js
[1, 2, 3] + [4, 5, 6];
```

Почему был получен такой результат?

### Ответ:

Результатом операции будет строка '1,2,34,5,6'.

Такой результат получается из-за того, что оператор + перегружен (т.е. ведет себя по разному в зависимости от типов операндов). В случае, когда он используется с массивами, он является оператором конкатенации. Поэтому сначала оба массива приводятся к строчному типу ('1,2,3' и '4,5,6' соответственно), а затем конкатенируются в одну. Конкатенация строк просто приписывает одну в конец другой, поэтому между 3 и 4 нет разделителя.

2. Дано выражение:

```js
var a = { b: 1 };
var b = a;
b.b = 2;
console.log(a);
```

Что будет выведено в консоли? Почему был получен такой результат?

### Ответ:

В консоли выведется объект {b: 2}.

Такой результат получается потому, что объекты имеют ссылочный тип. Поэтому, когда мы создаем переменную b и присваиваем ей объект a, мы не создаем новый объект с такими же свойствами, а записываем туда ссылку на присваеваемый объект. И переменная a и переменная b будут указывать на один и тот же объект. В результате операция b.b = 2; перезаписывает свойство b у этого исходного объекта.

3. Написать регулярное выражение, совпадающее с числом с плавающей точкой с точностью до 3 знака после запятой.

### Ответ:

```js
const regex = /^\d+\.\d{3}$/;
console.log(regex.test("1.234"));

// ^ начало строки
// \d+ любое количество цифр перед плавающей точкой
// \. точка
// \d{3} ровно три цифры после точки
// $ конец строки
```

4. Написать регулярное выражение, по которому определяется является ли строка ссылкой. Объяснить, как оно работает.

Пример:

```js
const isURL = (str) => true;
isURL("https://example.com");
isURL("http://www.example.com");
```

### Ответ:

```js
const isURL = (str) => {
  const regex = /^https?:\/\/\S+\.\S+$/;
  return regex.test(str);
};
console.log(isURL("https://example.com"));
console.log(isURL("http://www.example.com"));

// ^ начало строки
// https? совпадет с http и с https, т.к ? после символа делает его необязательным
// :\/\/ это экранированные ://
// \S+ один или больше непробельный символ
// \. точка
// $ конец строки
```

Это самая базовая реализация, не учитывающая все возможные аспекты (порты, запросы итд)

5. Каким будет значение переменной text после выполнения данного JavaScript кода?

```js
function setText(message) {
  text = message;
}
var text = "Текст";
setText("Сообщение");
```

Опишите, почему получился такой результат.

### Ответ:

Переменная text будет иметь значение "Сообщение".

Такой результат получится потому, что переменные, объявленные с помощью var имеют глобальную область видимости, поэтому доступны отовсюду внутри модуля, где они определены. Поэтому функция setText переписывает значение этой переменной на новое.

6. Написать функцию для получения список всех артикулов товаров в консоли браузера на странице [https://groupprice.ru/categories/jenskaya-odejda?referer_from=main_catalog](https://groupprice.ru/categories/jenskaya-odejda?referer_from=main_catalog)

### Ответ:

```js
const getProductIds = () => {
  const products = document.querySelectorAll("._product");

  products.forEach((product) => {
    console.log("0" + product.dataset["id"]);
  });
};

getProductIds();
```

7. Написать функцию для получения всех характеристики товара в консоли браузера в виде объекта в формате attributeName: value на странице [https://nir-vanna.ru/product/smesitel-bravat-art-f175109c-dlya-rakoviny/](https://nir-vanna.ru/product/smesitel-bravat-art-f175109c-dlya-rakoviny/)

### Ответ:

```js
const getProductParameters = () => {
  const parameters = document.querySelectorAll(
    ".tab-pane-product-parameter-item"
  );

  const parameterObj = {};

  parameters.forEach((parameter) => {
    const name = parameter.querySelector(".parameter-name");
    const value = parameter.querySelector(".parameter-value");

    const tooltip = name.querySelector(".t-w");
    if (tooltip) name.removeChild(tooltip);

    const attributeName = name.textContent.trim();
    const attributeValue = value.textContent.trim();

    parameterObj[attributeName] = attributeValue;
  });

  console.log(parameterObj);
};

getProductParameters();
```
