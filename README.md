# 8pm-algo-club

* 05/12/2025 
94. Binary Tree Inorder Traversal
https://leetcode.com/problems/binary-tree-inorder-traversal/description/



* 05/05/2025  
20. Valid Parentheses

https://leetcode.com/problems/valid-parentheses/description/

JS
```
function isValid(characters) {
    if (characters.length % 2 === 1) {
      return false;
    }
  
    const stack = [];
    const characterMap = {
      ")": "(",
      "]": "[",
      "}": "{",
    };
  
    for (let i = 0; i <= characters.length - 1; i++) {
      console.log("1", stack);
      if (
        characters[i] === "(" ||
        characters[i] === "[" ||
        characters[i] === "{"
      ) {
        stack.push(characters[i]);
        console.log("2", stack);
      }
      //also if array.length is 1
      else if (characterMap[characters[i]] === stack[stack.length - 1]) {
        stack.pop();
        console.log("3", stack);
      } else {
        return false;
      }
    }
  
    return stack.length === 0;
  }
```

### Step-by-step: Stack Changes for `{[()]}`

* only push OPENING.
* check CLOSING, if it pairs with the last element(matching OPENING) in the stack, pop the last element.
* return false if the closing bracket shows before opening bracket.
| Character | Action                      | Stack Before     | Stack After      | Notes                                 |
|-----------|-----------------------------|------------------|------------------|---------------------------------------|
| `{`       | Opening → push to stack     | `[]`             | [`{`]            | Save the opening bracket              |
| `[`       | Opening → push to stack     | [`{`]            | [`{`, `[`]       | Save the opening bracket              |
| `(`       | Opening → push to stack     | [`{`, `[`]       | [`{`, `[`, `(`]  | Save the opening bracket              |
| `)`       | Closing → pop & compare     | [`{`, `[`, `(`]  | [`{`, `[`]       | `(` matches `mapping[")"]` → OK ✅    |
| `]`       | Closing → pop & compare     | [`{`, `[`]       | [`{`]            | `[` matches `mapping["]"]` → OK ✅    |
| `}`       | Closing → pop & compare     | [`{`]            | `[]`             | `{` matches `mapping["}"]` → OK ✅    |
Final Stack: [] (Empty)
✅ All brackets matched correctly → Valid

