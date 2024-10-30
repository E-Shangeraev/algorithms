## Решение

```typescript
function findMinArrowShots(points: number[][]): number {
  points.sort((a, b) => a[0] - b[0]);

  let result = 1;
  let lastPoint = points[0];

  for (let i = 1; i < points.length; i++) {
    const current = points[i];

    if (Math.max(lastPoint[0], current[0]) <= Math.min(lastPoint[1], current[1])) {
      lastPoint = [Math.max(lastPoint[0], current[0]), Math.min(lastPoint[1], current[1])];
    } else {
      lastPoint = current;
      result++;
    }
  }

  return result;
}
```

## Эталонное решение

```javascript
/**
 * @param {number[][]} points
 * @return {number}
 */
var findMinArrowShots = function (points) {
  points.sort((a, b) => a[0] - b[0]); // O(n * log n)
  let result = 1;
  let lastPoint = points[0];
  for (let i = 1; i < points.length; i++) {
    let point = points[i];
    // если интервалы пересекаются, то для них используем 1 стрелу
    // и стараемся набрать как можно больше интервалов под 1 стрелу
    if (isOverlapping(lastPoint, point)) {
      lastPoint = overlapTwoIntervals(lastPoint, point);
      continue;
    }
    // если нет пересичений значит нужна еще 1 доп стрела и обновляем
    // последний интервал (last_point)
    lastPoint = point;
    result += 1;
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

**Оценка по времени:** O(n logn + n), т.к. присутствует сортировка

**Оценка по памяти:** O(1)

**Описание решения:**

https://kinescope.io/viTn41nQJ8CF57UdHg11Vb

1. Задача на пересечение интервалов. Сперва необходимо отсортировать массив по первым точкам интервалов

2. Далее проверяем на пересечение. Если пересекаются, то идем дальше. А если нет, то увеличиваем количество стрел
