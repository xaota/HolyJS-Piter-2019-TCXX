# pragma syntax
## motivation
добавляет подсказки для среды исполнения, что код может быть распараллелен или векторизован.

в первом случае ускоряет выполнение за счет использования мультипоточеости без явного создания воркеров, а во втором снижает количесво обращений к памяти.

> В будущем могут быть добавлены другие инструкции pragma.

## high-level api
### cycles
```javascript
% pragma parallel
for (const i = 0; i < array.length; ++i) {
  array[i] = i ** 2;
}

% pragma parallel
array.map(e => e ** 2);
```

### short syntax

```javascript
for%parallel (const i = 0; i < array.length; ++i) {
  array[i] = i ** 2;
}

array.map%parallel(e => e ** 2);
```

## FAQ
### Что, если вычисление зависит не только от i-го элемента массива, но и от предыдущих (вычисленных значений)?
в таком случае исполнение "векторизуется": из памяти в кеш всегда читается не один элемент массива, а некая последовательность элементов, обычно, минимум "страница" (зависит от процессора и его кеша).

Обычно, в начале каждой итерации цикла происходит выгрузка из кеша предыдущих значений, загрузка новых и работа идет уже с ними. ппи этом, если код обращается к предыдушим значениям, илет новое обращение к памяти.

Векторизация же  "говорит" процессору "выгружай предыдущие значения как можно реже"
