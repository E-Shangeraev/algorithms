Ошибся в условии `right <= nums.length`. Из-за этого правый указатель выходил на 2 за пределы массива.

```typescript
function findMaxConsecutiveOnes(nums: number[]): number {
  let left = 0;
  let right = 0;
  let result = 0;

  while (left < nums.length) {
    while (right <= nums.length && nums[right] !== 0) {
      right++;
    }

    result = Math.max(result, right - left);

    left = right + 1;
    right = right + 1;
  }

  return result;
}
```
