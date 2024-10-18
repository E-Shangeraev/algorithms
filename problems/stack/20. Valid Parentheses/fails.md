Забыл слово `const` в цикле

```typescript
const brackets = {
  ')': '(',
  ']': '[',
  '}': '{',
};

function isValid(s: string): boolean {
  const stack: string[] = [];

  for (char of s) {
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
