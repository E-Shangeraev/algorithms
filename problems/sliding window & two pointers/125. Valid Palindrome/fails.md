Не учел, что символ может быть числом. Дальше было несколько попыток проверить символ на число. Оказывается, если в JavaScript приводить пустую строку к числу (`Number('')`, `Number(' ')`, `+''`), то вернется `0`.

```typescript
function isPalindrome(s: string): boolean {
  let left = 0;
  let right = s.length - 1;

  while (left <= right) {
    if (!isLetter(s[left])) {
      left++;
      continue;
    }

    if (!isLetter(s[right])) {
      right--;
      continue;
    }

    if (s[left].toLowerCase() !== s[right].toLowerCase()) {
      return false;
    }

    left++;
    right--;
  }

  return true;
}

function isLetter(char: string): boolean {
  return char !== char.toLowerCase();
}
```
