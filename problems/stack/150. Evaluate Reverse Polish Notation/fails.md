Не привел строку к числу

```typescript
function evalRPN(tokens: string[]): number {
  const stack: string[] = [];

  for (const char of tokens) {
    switch (char) {
      case '+':
        stack.push(stack.pop() + stack.pop());
        break;
      case '-':
        stack.push(stack.pop() - stack.pop());
        break;
      case '*':
        stack.push(stack.pop() * stack.pop());
        break;
      case '/':
        stack.push(stack.pop() / stack.pop());
        break;
      default:
        stack.push(char);
    }
  }

  return stack[0];
}
```

Не учел порядок следования чисел в операции `.pop()`

```typescript
function evalRPN(tokens: string[]): number {
  const stack: number[] = [];

  for (const char of tokens) {
    switch (char) {
      case '+':
        stack.push(Number(stack.pop()) + Number(stack.pop()));
        break;
      case '-':
        stack.push(Number(stack.pop()) - Number(stack.pop()));
        break;
      case '*':
        stack.push(Number(stack.pop()) * Number(stack.pop()));
        break;
      case '/':
        stack.push(Number(stack.pop()) / Number(stack.pop()));
        break;
      default:
        stack.push(Number(char));
    }
  }

  return stack[0];
}
```

Не добавил фигурные скобки, в следствие чего переменные `a` и `b` пересоздавались в одном скоупе. Плюс не учитывал, что нужно брать только целую часть от деления и умножения.

```typescript
function evalRPN(tokens: string[]): number {
  const stack: number[] = [];

  for (const char of tokens) {
    switch (char) {
      case '+':
        stack.push(stack.pop() + stack.pop());
        break;
      case '-':
        const b = stack.pop();
        const a = stack.pop();
        stack.push(a - b);
        break;
      case '*':
        stack.push(stack.pop() * stack.pop());
        break;
      case '/':
        const b = stack.pop();
        const a = stack.pop();
        stack.push(a / b);
        break;
      default:
        stack.push(Number(char));
    }
  }

  return stack[0];
}
```
