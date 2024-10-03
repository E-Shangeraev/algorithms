Использовал пересекающееся название переменной `height`

```typescript
function maxArea(height: number[]): number {
  let left = 0;
  let right = height.length - 1;
  let maxAmount = 0;

  while (left <= right) {
    const length = right - left;
    const height = Math.min(height[left], height[right]);
    maxAmount = Math.max(maxAmount, length * height);

    if (height[left] <= height[right]) {
      left++;
    } else {
      right--;
    }
  }

  return maxAmount;
}
```
