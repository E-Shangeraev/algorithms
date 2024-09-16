## Решение

```typescript
function topKFrequent(nums: number[], k: number): number[] {
  const hashmap: Record<number, number> = {};
  let maxRepeats = -Infinity;

  for (let i = 0; i < nums.length; i++) {
    const curr = nums[i];
    hashmap[curr] = (hashmap[curr] ?? 0) + 1;

    if (hashmap[curr] > maxRepeats) {
      maxRepeats = hashmap[curr];
    }
  }

  const freqList: number[][] = Array.from({ length: maxRepeats + 1 }, () => []);

  for (let [num, count] of Object.entries(hashmap)) {
    freqList[count].push(+num);
  }

  const result: number[] = [];

  for (let i = freqList.length - 1; i >= 0; i--) {
    for (let num of freqList[i]) {
      if (k === 0) {
        return result;
      }

      result.push(num);
      k--;
    }
  }

  return result;
}
```

**Оценка по времени:** O(n), где n - размер списка nums

**Оценка по памяти:** O(n), где n - размер списка nums

**Описание решения:**

1. составляем мапу с числом повторений. Сохраняем максимальное число повторений.

   `maxRepeats = 3`

   `{ 1: 3, 2: 2, 3: 2 }`

2. создаем массив массивов, где индексом будет кол-во повторений. Длина массива - максимальное число повторений + 1. И заполняем массив

   `[[], [], [2,3] [1]]`

3. Идем в обратном порядке по массиву и возвращаем k наиболее частых элементов. k на каждой итерации надо уменьшать на единицу и если k === 0, возвращать результат
