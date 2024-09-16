## Решение

```typescript
function twoSum(nums: number[], target: number): number[] {
  const hashmap = new Map<number, number>();

  for (let i = 0; i < nums.length; i++) {
    const curr = nums[i];
    const diff = target - curr;

    if (hashmap.has(diff)) {
      return [hashmap.get(diff), i];
    } else {
      hashmap.set(curr, i);
    }
  }

  return [];
}
```

Оценка по времени: O(n), где n - размер списка nums

Оценка по памяти: O(n), где n - размер списка nums

Описание решения: Используем хешмапу, где ключ - сам элемент списка nums, а значение - индекс. На каждой итерации находим разницу между target и текущим элементом списка. Проверяем есть ли эта разница в нашей мапе и если да, то вовзвращаем результат вида [hashmap.get(diff), i]. Иначе добавляем текущий элемент в мапу. В случае если прошлись по всему списку и не нашли подходящие числа, возвращаем пустой массив
