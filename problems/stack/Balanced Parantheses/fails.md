Забыл про проверку на неравенство нулю, когда скобка закрывающаяся

```javascript
module.exports = {
  //param A : string
  //return an integer
  solve: function (A) {
    let balance = 0;

    for (const char of A) {
      if (char === '(') {
        balance++;
      } else if (char === ')') {
        balance--;
      }
    }

    return balance === 0 ? 1 : 0;
  },
};
```
