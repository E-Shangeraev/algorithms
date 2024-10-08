Забыл передать функции `good` второй аргумент

```typescript
function search(nums: number[], target: number): number {
  let l = 0;
  let r = nums.length;

  while (l - r !== 1) {
    const mid = Math.floor((l + r) / 2);

    if (good(mid)) {
      l = mid;
    } else {
      r = mid;
    }
  }

  return nums[l] === target ? l : -1;
}

function good(n: number, target: number): boolean {
  return n <= target;
}
```

Неправильно определил условие для цикла + функция `good` сравнивает индекс с таргетом, а не число под индексом

```typescript
function search(nums: number[], target: number): number {
  let l = 0;
  let r = nums.length;

  while (l - r !== 1) {
    const mid = Math.floor((l + r) / 2);

    if (good(mid, target)) {
      l = mid;
    } else {
      r = mid;
    }
  }

  return nums[l] === target ? l : -1;
}

function good(n: number, target: number): boolean {
  return n <= target;
}
```

Функция `good` сравнивает индекс с таргетом, а не число под индексом

```typescript
function search(nums: number[], target: number): number {
  let l = 0;
  let r = nums.length;

  while (r - l !== 1) {
    const mid = Math.floor((l + r) / 2);

    if (good(mid, target)) {
      l = mid;
    } else {
      r = mid;
    }
  }

  return nums[l] === target ? l : -1;
}

function good(n: number, target: number): boolean {
  return n <= target;
}
```
