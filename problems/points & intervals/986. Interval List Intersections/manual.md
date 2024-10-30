## Решение

```typescript
function intervalIntersection(firstList: number[][], secondList: number[][]): number[][] {
  const result: number[][] = [];

  let p1 = 0;
  let p2 = 0;

  while (p1 < firstList.length && p2 < secondList.length) {
    const [a1, b1] = firstList[p1];
    const [a2, b2] = secondList[p2];

    if (isIntersection(firstList[p1], secondList[p2])) {
      result.push([Math.max(a1, a2), Math.min(b1, b2)]);
    }

    if (b1 < b2) {
      p1++;
    } else {
      p2++;
    }
  }

  return result;
}

function isIntersection(interval1: number[], interval2: number[]): boolean {
  const [a1, b1] = interval1;
  const [a2, b2] = interval2;

  return Math.max(a1, a2) <= Math.min(b1, b2);
}
```

## Эталонное решение

```javascript
/**
 * @param {number[][]} firstList
 * @param {number[][]} secondList
 * @return {number[][]}
 */
var intervalIntersection = function (firstList, secondList) {
  let result = [];
  let p1 = 0;
  let p2 = 0;
  while (p1 < firstList.length && p2 < secondList.length) {
    // если пересекаются - добавляем в ответ
    if (isOverlapping(firstList[p1], secondList[p2])) {
      result.push(overlapTwoIntervals(firstList[p1], secondList[p2]));
    }

    // важно сравнивать именно концы интервалов, а не начало
    if (firstList[p1][1] < secondList[p2][1]) {
      p1 += 1;
    } else {
      p2 += 1;
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
var overlapTwoIntervals = function (a, b) {
  return [Math.max(a[0], b[0]), Math.min(a[1], b[1])];
};
```

**Оценка по времени:** O(n + m)

**Оценка по памяти:** O(n + m)

**Описание решения:**

https://kinescope.io/ontcNrmyr57r46qkufizsU

1. Перебираем интервалы в обоих списках и проверяем на пересечение по формуле `Math.max(a1, a2) <= Math.min(b1, b2)`

2. Если пересекаются, добавляем пересечение интервалов `[Math.max(a1, a2), Math.min(b1, b2)]` в результирующий массив

3. Самое сложное в задаче –– правильно инкрементировать указатели. Для этого проверяем на неравенство последних точек текущих интервалов. У чьего интервала последняя точка меньше, того указатель и увеличиваем
