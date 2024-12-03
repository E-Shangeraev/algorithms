Ошибка в определении матрицы `used`, т.к. каждая строка ссылается на один и тот же массив

```typescript
function inBounds(x: number, y: number, grid: string[][]) {
  return x >= 0 && x < grid.length && y >= 0 && y < grid[0].length;
}

function dfs(x: number, y: number, used: boolean[][], grid: string[][]) {
  if (!inBounds(x, y, grid)) return;

  if (used[x][y] || grid[x][y] === '0') return;

  used[x][y] = true;

  const steps = [
    [0, -1],
    [-1, 0],
    [0, 1],
    [1, 0],
  ];

  for (const step of steps) {
    const nextX = x + step[0];
    const nextY = y + step[1];

    dfs(nextX, nextY, used, grid);
  }
}

function numIslands(grid: string[][]): number {
  let result = 0;
  const used: boolean[][] = Array(grid.length).fill(Array(grid[0].length).fill(false));

  for (let i = 0; i < grid.length; i++) {
    for (let j = 0; j < grid[i].length; j++) {
      if (used[i][j] || grid[i][j] === '0') {
        continue;
      }
      dfs(i, j, used, grid);
      result++;
    }
  }

  return result;
}
```
