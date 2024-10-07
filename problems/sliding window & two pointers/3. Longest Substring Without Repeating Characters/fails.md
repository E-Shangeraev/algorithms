Сначала очишал окно на каждой итерации, не учитывая, что на следующей оно должно было содержать от 1 до 2 элементов.

```typescript
function lengthOfLongestSubstring(s: string): number {
  let left = 0;
  let right = 0;
  let result = 0;
  const currentWindow = new Set<string>([s[left]]);

  while (left < s.length) {
    while (right + 1 < s.length && !currentWindow.has(s[right + 1])) {
      currentWindow.add(s[right + 1]);
      right++;
    }

    currentWindow.clear();

    result = Math.max(result, right - left + 1);

    left = left + 1;
  }

  return result;
}
```
