## Решение

```typescript
import { Interval } from '../home/lib/index';
/**
 * Definition of Interval:
 * export class Interval {
 *     start :number;
 *     end :number;
 *     constructor(start :number, end :number) {
 *         this.start = start;
 *         this.end = end;
 *     }
 * }
 */

export class Solution {
  /**
   * @param intervals: an array of meeting time intervals
   * @return: the minimum number of conference rooms required
   */
  minMeetingRooms(intervals: Interval[]): number {
    const points: number[][] = [];
    let maxRooms = 0;
    let currentRooms = 0;

    for (const i of intervals) {
      points.push([i.start, 1]);
      points.push([i.end, -1]);
    }

    points.sort((a, b) => {
      if (a[0] === b[0]) {
        return a[1] - b[1];
      }

      return a[0] - b[0];
    });

    for (const p of points) {
      currentRooms += p[1];
      maxRooms = Math.max(maxRooms, currentRooms);
    }

    return maxRooms;
  }
}
```

## Эталонное решение

```javascript
/**
 * @param {number[][]} intervals
 * @return {number}
 */
var minMeetingRooms = function (intervals) {
  const points = [];

  intervals.forEach(interval => {
    points.push([interval[0], 1]); // точка, +1 - что нужна еще одна комната
    points.push([interval[1], -1]); // точка, -1 - что комната освободилась
  });

  // Сортировка. [10, -1] будет перед [10, +1] - сначала освобождают комнаты, потом занимают
  points.sort((a, b) => {
    if (a[0] === b[0]) return a[1] - b[1];
    return a[0] - b[0];
  });

  let maxRoomNumbers = 0;
  let currRoomNumbers = 0;

  // Для каждого момента времени находим используемое число комнат и выбираем максимальное значение
  points.forEach(point => {
    currRoomNumbers += point[1];
    maxRoomNumbers = Math.max(maxRoomNumbers, currRoomNumbers);
  });

  return maxRoomNumbers;
};
```

**Оценка по времени:** O(n \* logn)

**Оценка по памяти:** O(n)

**Описание решения:**

https://kinescope.io/jKcW8EMp7tNautXUswg1D7

1. Метод точек. Создаем массив с точками. Первая цифра будет означать открытие комнаты `[interval[0], +1]`, а вторая закрытие `[interval[1], -1]`.

2. Сортируем получившийся массив точек по координате. Если координата совпадает, то сортируем по флагу открытия/закрытия (+1/-1). От этого условия зависит конечный результат. Если -1 поставить перед +1, то комната сначала закрывается и только после этого открывается новая. В таком случае количество необходимых комнат будет меньше, нежели в случае, когда сначала открываем новую, а потом закрываем старую.

3. Перебираем отсортированный массив точек. Тут нам важны только вторые цифры - единицы. Ищем максимум суммируя все 1/-1.
