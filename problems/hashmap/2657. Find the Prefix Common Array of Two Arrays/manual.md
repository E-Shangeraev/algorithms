## Решение

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

    if (A[i] === B[i]) {
      commonCount--;
    }

    result[i] = commonCount;
  }

  return result;
}
```

**Оценка по времени:** O(n), где n - размер списка A или B

**Оценка по памяти:** O(n), где n - размер списка A или B. Создается 2 хешсета, но константы в Big O-notation опускаем

**Описание решения:**
Решение учитывает дубликаты

1. Обходим число из списка записываем в соответствующий сет.

2. Проверяем встречалось ли число из списка `A` в сете `B` и наоборот. Если встречалось, увеличиваем счетчик на единицу. Однако если встречаются 2 одинаковых числа, то счетчик нужно уменьшить на 1.

3. Записываем на каждой итерации значение счетчика по соответствующему индексу
