## Решение

```typescript
function merge(intervals: number[][]): number[][] {
  intervals.sort((a, b) => a[0] - b[0]);
  const result: number[][] = [intervals[0]];

  for (const current of intervals) {
    const prev = result.at(-1);

    if (Math.max(prev[0], current[0]) <= Math.min(prev[1], current[1])) {
      result.pop();
      result.push([Math.min(prev[0], current[0]), Math.max(prev[1], current[1])]);
    } else {
      result.push(current);
    }
  }

  return result;
}
```

## Эталонное решение

```javascript
/**
 * @param {number[][]} intervals
 * @return {number[][]}
 */
var merge = function (intervals) {
  // O(NlogN)
  intervals.sort((a, b) => a[0] - b[0]); // start <= end по условию (это важно)

  let result = [];
  result.push(intervals[0]);

  // O(n)
  for (let i = 1; i < intervals.length; i++) {
    let interval = intervals[i];
    // если текущий интервал и последний в ответе пересекаются,
    // значит объединяем их, иначе добавляем интервал к ответу и это значит,
    // что ни один интервал, который имеет точку начала меньше текущего интервала
    // не будет пересечен ни с одним лежащим правее и не с текущим
    if (isOverlapping(result[result.length - 1], interval)) {
      result[result.length - 1] = mergeTwoIntervals(result[result.length - 1], interval);
    } else {
      result.push(interval);
    }
  }
  return result;
};

/**
 * @param {number[]} a
 * @param {number[]} b
 * @return {boolean}
 */
var isOverlapping = function (a, b) {
  return Math.max(a[0], b[0]) <= Math.min(a[1], b[1]);
};

/**
 * @param {number[]} a
 * @param {number[]} b
 * @return {number[]}
 */
var mergeTwoIntervals = function (a, b) {
  return [a[0], Math.max(a[1], b[1])];
};
```

**Оценка по времени:** O(n \* logn)

**Оценка по памяти:** O(n)

**Описание решения:**

https://kinescope.io/m9iYTLT66EnFn7L8rt1PvP

1. Сортируем исходный массив по первым точкам отрезков.

2. Создаем результирующий массив. Изначально он содержит самый первый отрезок.

3. Перебираем отрезки. Если текущий интервал пересекается с последним в результирующем массиве (`Math.max(prev[0], current[0]) <= Math.min(prev[1], current[1])`), то обновляем последний отрезок в результирующем массиве (`[Math.min(prev[0], current[0]), Math.max(prev[1], current[1])]`). Иначе просто добавляем текущий отрезок в `result`
