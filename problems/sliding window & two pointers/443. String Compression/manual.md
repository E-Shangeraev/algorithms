## Решение

```typescript
function compress(chars: string[]): number {
  let left = 0;
  let right = 0;
  const result: string[] = [];

  while (left < chars.length) {
    while (right + 1 < chars.length && chars[right] === chars[right + 1]) {
      right++;
    }

    const count = right + 1 - left;

    result.push(chars[left]);

    if (count > 1) {
      const digits = count.toString().split('');

      for (const d of digits) {
        result.push(d);
      }
    }

    left = right + 1;
    right = right + 1;
  }

  for (let i = 0; i < result.length; i++) {
    chars[i] = result[i];
  }

  return result.length;
}
```

## Эталонное решение

```javascript
/**
 * @param {string[]} chars
 * @return {number}
 */
var compress = function (chars) {
  let l = 0;
  let r = 0;
  let result = [];
  while (l < chars.length) {
    // before
    // l
    // a a a b b a a
    // r

    // бежим правым указателем пока в интервале [l, r]
    // находятся все одинаковые символы
    while (r + 1 < chars.length && chars[r] === chars[r + 1]) {
      r++;
    }
    // after
    // l
    // a a a b b a a
    //     r

    // обновляем ответ
    let windowSize = r - l + 1;
    if (windowSize === 1) {
      result.push(chars[r]);
    } else {
      result.push(chars[r]);
      result.push(...String(windowSize));
    }

    // интервалы не пересекаются, поэтому сдвигаем
    // на r + 1 - именно отсюда будет начинаться
    // следующий интервал
    l = r + 1;
    r = r + 1;
  }
  for (let i = 0; i < result.length; i++) {
    chars[i] = result[i];
  }
  return result.length;
};
```

**Оценка по времени:** O(n), где n - длины массива chars

**Оценка по памяти:** O(n)

**Описание решения:**

https://kinescope.io/vvgDUXKd8u88PyMfv1HRWv

1. Непересекающиеся окна. Ставим левый и правый указатели в начало массива.

2. Правый указатель двигается если следующий элемент равен текущему.

3. Находим количество повторов `count` по формуле `right + 1 - left`.

4. Если `count` равен 1, то в результирующий массив пушим только символ. Иначе приводим `count` к строке и пушим помимо символа каждую цифру из строки `count`.

5. Двигаем оба указателя на `right + 1`.
