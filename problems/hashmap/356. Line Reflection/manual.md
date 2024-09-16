## Решение

```javascript
function isReflected(points) {
  const hashmap = {};
  let minX = Infinity;
  let maxX = -Infinity;

  for (let [x, y] of points) {
    minX = Math.min(minX, x);
    maxX = Math.max(maxX, x);

    const key = pointToString(x, y);
    hashmap[key] = (hashmap[key] ?? 0) + 1;
  }

  for (let [x, y] of points) {
    const symX = maxX + minX - x;
    const curPoint = pointToString(x, y);
    const symPoint = pointToString(symX, y);

    if (hashmap[curPoint] !== hashmap[symPoint]) {
      return false;
    }
  }

  return true;
}

function pointToString(x, y) {
  return `[${x}, ${y}]`;
}
```

Оценка по времени: O(n), где n - размер списка points. Несмотря на то, что проходим массив дважды O(2n), в Big O-notation константы опускаются.

Оценка по памяти: O(n), где n - размер списка points

Описание решения:

Решение учитывает дубликаты

1 - Обходим все точки, находим maxX и minX и наполняем хешмапу. Ключом будет текущая точка (x и y приводятся к строке - недостаточно учитывать только координату x или только y), а значением кол-во ее повторений.

2 - Обходим все точки и ищем симметричную по формуле: symX = maxX + minX - currentX. Формируем ключ для хешмапы на основании symX и текущего y. Если значение для текущей точки отличается от значения симметричной - возвращаем false
