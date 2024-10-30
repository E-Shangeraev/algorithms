Неправильно двигал указатели

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

    if (p1 <= p2) {
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
