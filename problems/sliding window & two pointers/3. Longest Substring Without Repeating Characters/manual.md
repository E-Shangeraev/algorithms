## Решение

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

    result = Math.max(result, right - left + 1);

    currentWindow.delete(s[left]);

    left = left + 1;
  }

  return result;
}
```

## Эталонное решение

```javascript
/**
 * @param {string} s
 * @return {number}
 */
var lengthOfLongestSubstring = function (s) {
  if (s.length === 0) {
    return 0;
  }
  let result = 0;

  let l = 0;
  let r = 0;
  // r - включительно идет, т е наше плавающее окно это [l, r]
  // включительно, т к r = 0, значит 0 символ уже входит в окно,
  // поэтому добавляем в windowChars
  let windowChars = new Set([s[0]]);

  // a b c a b a

  while (l < s.length) {
    // before
    // l
    // a b c a b a
    // r

    // бежим правым указателем пока в интервале [l, r]
    // находятся все последовательные числа
    while (r + 1 < s.length && !windowChars.has(s[r + 1])) {
      windowChars.add(s[r + 1]);
      r += 1;
    }

    // after
    // l
    // a b c a b a
    //     r

    // обновляем
    result = Math.max(result, r - l + 1);

    // когда двигаем левую границу убираем буквы
    windowChars.delete(s[l]);
    l += 1;

    // если r < l то обноввляенм r и windowChars
    if (r < l && l < s.length) {
      r = l;
      // r - включительно идет, поэтому добавляем в windowChars
      windowChars = new Set([s[r]]);
    }
  }
  return result;
};
```

**Оценка по времени:** O(n)

**Оценка по памяти:** O(n)

**Описание решения:**

https://kinescope.io/pvRQiaVdJtJz8mm9m1r5iA

1. Пересекающиеся окна. Ставим левый и правый указатели в начало массива. Создаем хешсет, который по-умолчанию содержит первый элемент строки.

2. Правый указатель двигается в случае, если следующего за ним элемента нет в сете.

3. Если условие для правого указателя выполняется, то добавляем следующий элемент в сет и увеличиваем указатель.

4. Если условие для правого указателя не выполняется, то считаем размер окна и удаляем элемент под левым указателем из сета.

5. Двигаем левый указатель на `left + 1`.
