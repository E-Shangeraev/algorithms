## Решение

```typescript
const brackets = {
  ')': '(',
  ']': '[',
  '}': '{',
};

function isValid(s: string): boolean {
  const stack: string[] = [];

  for (const char of s) {
    if (char === '(' || char === '[' || char === '{') {
      stack.push(char);
      continue;
    }

    if (stack.at(-1) === brackets[char]) {
      stack.pop();
    } else {
      return false;
    }
  }

  return stack.length === 0;
}
```

## Эталонное решение

```javascript
/**
 * @param {string} s
 * @return {boolean}
 */
var isValid = function (s) {
  const stack = [];
  const pairs = { '{': '}', '(': ')', '[': ']' };
  for (let currentChar of s) {
    if (pairs[currentChar]) {
      // если скобка открытая - просто добавляем в стек
      stack.push(currentChar);
      continue;
    }

    // перед нами закрывающаяся скобка, но стек пуст
    if (stack.length === 0) {
      return false;
    }
    // удаляем последний элемент из стека
    const lastChar = stack.pop();
    // проверяем что последний элемент в стеке и текущий образуют пару
    // если пару не образуют, то вернем False
    if (pairs[lastChar] !== currentChar) {
      return false;
    }
  }
  return stack.length === 0;
};
```

**Оценка по времени:** O(n)

**Оценка по памяти:** O(1)

**Описание решения:**

https://kinescope.io/pgV5iKyvwueimD7teppP7o

1. Добавляем октрывающиеся скобки в стек.

2. Если встречаем закрывающую скобку того же типа, что последний элемент в стеке, то удаляем элемент из стека. Если тип скобок не совпадает, сразу возвращаем `false`

3. В конце проверяем, что стек пустой
