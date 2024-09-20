Сначала сильно переусложнил решение + оно не работало

```typescript
function canPermutatePalindrome(s: string) {
  const hashmap = {};
  let maxVal = -Infinity;

  for (let char of s) {
    hashmap[char] = (hashmap[char] ?? 0) + 1;

    if (hashmap[char] > maxVal) {
      maxVal = hashmap[char];
    }
  }

  const array = new Array(maxVal + 1).fill(0);

  for (let char of hashmap) {
    const index = hashmap[char];
    array[index]++;
  }

  for (let i = 1; i < array.length; i++) {
    if (i === 1 && array[i] > 1) return false;

    if (isOdd(i) && array[i] > 0) return false;
  }

  return true;
}

function isOdd(n: number): boolean {
  return Math.abs(n % 2) == 1;
}
```
