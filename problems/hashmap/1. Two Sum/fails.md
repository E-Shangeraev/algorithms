Главный вывод: очень сильно тороплюсь запускать код. Сама идея алгоритма описана верно, но из-за спешки допустил синтаксические и даже одну логическую ошибку

Пропустил скобку. Не написал условие для else (хотя перед написанием кода прописал это). Неправильный синтаксис обращения к Map в JS:

```typescript
function twoSum(nums: number[], target: number): number[] {
    const hashmap = new Map<number, number>();

    for (let i = 0; i < nums.length; i++) {
        const curr = nums[i];
        const diff = target - curr;

        if (hashmap.has(diff) {
            return [hashmap[diff], hashmap[curr]];
        }
    }

    return [];
};
```

То же самое, только добавил скобку:

```typescript
function twoSum(nums: number[], target: number): number[] {
  const hashmap = new Map<number, number>();

  for (let i = 0; i < nums.length; i++) {
    const curr = nums[i];
    const diff = target - curr;

    if (hashmap.has(diff)) {
      return [hashmap[diff], hashmap[curr]];
    }
  }

  return [];
}
```

Вспомнил про невыполнение условия

```typescript
function twoSum(nums: number[], target: number): number[] {
  const hashmap = new Map<number, number>();

  for (let i = 0; i < nums.length; i++) {
    const curr = nums[i];
    const diff = target - curr;

    if (hashmap.has(diff)) {
      return [hashmap[diff], hashmap[curr]];
    } else {
      hashmap.set(curr, i);
    }
  }

  return [];
}
```

Вспомнил как обращаться к Map, но допустил логическую ошибку: у нас в мапе еще нет текущего элемента и нам нужен всего лишь индекс, который мы уже знаем на данной итерации:

```typescript
function twoSum(nums: number[], target: number): number[] {
  const hashmap = new Map<number, number>();

  for (let i = 0; i < nums.length; i++) {
    const curr = nums[i];
    const diff = target - curr;

    if (hashmap.has(diff)) {
      return [hashmap.get(diff), hashmap.get(curr)];
    } else {
      hashmap.set(curr, i);
    }
  }

  return [];
}
```
