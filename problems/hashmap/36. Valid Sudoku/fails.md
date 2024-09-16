В TypeScript `isNaN` принимает только числа и `NaN`. В чистом JavaScript такой ошибки бы не было

```typescript
function isValidSudoku(board: string[][]): boolean {
  const rows = new Set<string>();
  const cols = new Set<string>();
  const boxes = new Set<string>();

  for (let i = 0; i < board.length; i++) {
    for (let j = 0; j < board[i].length; j++) {
      const current = board[i][j];

      if (isNaN(current)) {
        continue;
      }

      const rowElement = `[${i}, ${current}]`;

      if (rows.has(rowElement)) {
        return false;
      } else {
        rows.add(rowElement);
      }

      const colElement = `[${j}, ${current}]`;

      if (cols.has(colElement)) {
        return false;
      } else {
        cols.add(colElement);
      }

      const boxIndex = Math.floor(i / 3) * 3 + Math.floor(j / 3);
      const boxElement = `[${boxIndex}, ${current}]`;

      if (boxes.has(boxElement)) {
        return false;
      } else {
        boxes.add(boxElement);
      }
    }
  }

  return true;
}
```
