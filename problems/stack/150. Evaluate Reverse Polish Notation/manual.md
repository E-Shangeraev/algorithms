## Решение

```typescript
function evalRPN(tokens: string[]): number {
  const stack: number[] = [];

  for (const char of tokens) {
    switch (char) {
      case '+':
        stack.push(stack.pop() + stack.pop());
        break;
      case '-': {
        const b = stack.pop();
        const a = stack.pop();

        stack.push(a - b);
        break;
      }
      case '*':
        stack.push(Math.trunc(stack.pop() * stack.pop()));
        break;
      case '/': {
        const b = stack.pop();
        const a = stack.pop();

        stack.push(Math.trunc(a / b));
        break;
      }
      default:
        stack.push(Number(char));
    }
  }

  return stack[0];
}
```

**Оценка по времени:** O(n)

**Оценка по памяти:** O(1)

**Описание решения:**

1. Закидываем в стек только числа (не забываем приводить строки)

2. Если встречаем знак, то производим соответствующую операцию. Тут важно помнить про сохранение порядка чисел в операциях деления и нахождения разности

3. В конце стек содержит всего одно число –– оно и будет ответом.
