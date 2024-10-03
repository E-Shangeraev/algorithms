По невнимательности вернул массив `nums`

```typescript
function moveZeroes(nums: number[]): void {
  let s = 0;
  let f = 1;

  while (f < nums.length) {
    if (nums[f] !== 0) {
      [nums[s], nums[f]] = [nums[f], nums[s]];
      s++;
    }

    f++;
  }

  return nums;
}
```

Быстрый указатель начинал всегда с первого индекса, что приводило к лишним свопам. Например, в кейсе `[2, 1]`, вместо исходного массива возвращался `[1, 2]`.

```typescript
function moveZeroes(nums: number[]): void {
  let s = 0;
  let f = 1;

  while (f < nums.length) {
    if (nums[f] !== 0) {
      [nums[s], nums[f]] = [nums[f], nums[s]];
      s++;
    }

    f++;
  }
}
```
