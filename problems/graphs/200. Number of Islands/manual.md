## Решение

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
  const used: boolean[][] = Array.from({ length: grid.length }, () => Array(grid[0].length).fill(false));

  for (let i = 0; i < grid.length; i++) {
    for (let j = 0; j < grid[i].length; j++) {
      if (!used[i][j] && grid[i][j] === '1') {
        dfs(i, j, used, grid);
        result++;
      }
    }
  }

  return result;
}
```

## Эталонное решение

```javascript
/**
 * @param {character[][]} grid
 * @return {number}
 */
var numIslands = function (grid) {
  let result = 0;
  for (let i = 0; i < grid.length; i++) {
    for (let j = 0; j < grid[i].length; j++) {
      // если клетка '1' (земля)
      if (grid[i][j] === '1') {
        // запустить dfs, чтобы пометить все связанные клетки суши как '0'
        dfs(i, j, grid);
        // увеличить счетчик островов
        result++;
      }
    }
  }
  return result;
};

const dfs = (x, y, grid) => {
  // базовый случай: за пределами границ или клетка - вода ('0')
  if (x < 0 || x >= grid.length || y < 0 || y >= grid[0].length || grid[x][y] === '0') {
    return;
  }
  // пометить текущую клетку как воду ('0')
  grid[x][y] = '0';
  // рекурсивно исследовать соседние клетки
  dfs(x + 1, y, grid);
  dfs(x - 1, y, grid);
  dfs(x, y + 1, grid);
  dfs(x, y - 1, grid);
};
```

**Оценка по времени:** O(n \* m)

**Оценка по памяти:** O(n \* m) или O(1) если не заводить матрицу `used`

**Описание решения:**

https://www.youtube.com/watch?v=gPZ-LGDxyT4

Можно решать, как через DFC, так и через BFS. В данном случае решение представлено через DFS.

1. Заводим матрицу `used`, которая будет хранить клетки суши, которые уже обошли.

2. Обходим каждый элемент и запускаем рекурсивную функцию dfs, если встречаем сушу.

3. Функция dfs кладет переданную в нее клетку в матрицу `used` и проверяет клетки по вертикали и горизонтали вокруг нее.
