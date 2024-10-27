Ошибся в определении типа для массива `result`. Также не обязательно создавать новую переменную под сортированный массив, т.к. метод `.sort()` работает in-place.

```typescript
function merge(intervals: number[][]): number[][] {
  const sortedIntervals = intervals.sort((a, b) => a[0] - b[0]);
  const result: number[] = [sortedIntervals[0]];

  for (const current of sortedIntervals) {
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
