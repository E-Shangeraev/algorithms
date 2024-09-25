Забыл, что в методе `reduce` необходимо возвращать значение

```typescript
class NumArray {
  nums: number[];
  px: number[];

  constructor(nums: number[]) {
    this.nums = nums;
    this.px = [0];
    this.fillPrefixArray();
  }

  fillPrefixArray(): void {
    this.nums.reduce((acc, cur) => {
      acc += cur;

      this.px.push(acc);
    }, 0);
  }

  sumRange(left: number, right: number): number {
    return this.px[right + 1] - this.px[left];
  }
}
```
