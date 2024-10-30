Сначала решал через объединение интервалов. Не учел, что 1 может пересекаться со 2, 2 с 3, но при этом 1 с 3 не пересекаются. В данном случае ответом был бы 1 дротик, вместо 2. Плюс по памяти можно решить оптимальнее.

Тут задача решится, если в 17 строке max и min поменять местами. Однако, опять же, память получится О(n)

```typescript
function findMinArrowShots(points: number[][]): number {
  points.sort((a, b) => a[0] - b[0]);

  const bursted = [points[0]];

  for (let i = 1; i < points.length; i++) {
    const current = points[i];
    const prev = bursted.at(-1);

    if (Math.max(prev[0], current[0]) <= Math.min(prev[1], current[1])) {
      bursted.pop();
      bursted.push([Math.min(prev[0], current[0]), Math.max(prev[1], current[1])]);
    } else {
      bursted.push(current);
    }
  }

  return bursted.length;
}
```
