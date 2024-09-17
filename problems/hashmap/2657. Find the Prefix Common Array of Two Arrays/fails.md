Не учел случай с одинаковыми числами на одном индексе. В таком случае нужно уменьшать commonCount на единицу

```typescript
function findThePrefixCommonArray(A: number[], B: number[]): number[] {
  const hashsetA = new Set<number>();
  const hashsetB = new Set<number>();
  const result: number[] = [];
  let commonCount = 0;

  for (let i = 0; i < A.length; i++) {
    hashsetA.add(A[i]);
    hashsetB.add(B[i]);

    if (hashsetA.has(B[i])) {
      commonCount++;
    }

    if (hashsetB.has(A[i])) {
      commonCount++;
    }

    result[i] = commonCount;
  }

  return result;
}
```
