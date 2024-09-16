Синтаксическая ошибка. Попытался использовать цикл for ... in для массива (он только для объектов)

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

  for (let [num, count] in Object.entries(hashmap)) {
    freqList[count].push(num);
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

Ошибка несоответствия типов. Забыл привести num (строчный ключ объекта) к числу.

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
    freqList[count].push(num);
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
