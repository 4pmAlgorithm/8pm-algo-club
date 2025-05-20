# 8pm-algo-club

## 05/22/2025 Thurs
https://leetcode.com/problems/best-time-to-buy-and-sell-stock/




## 05/19/2025 Mon
Problem:
Write a recursive function reverseString(str) that returns the reversed version of a string.

js
```
reverseString("hello")
→ reverseString("ello") + "h"
→ (reverseString("llo") + "e") + "h"
→ ((reverseString("lo") + "l") + "e") + "h"
→ (((reverseString("o") + "l") + "l") + "e") + "h"
→ (v((( "o" ) + "l") + "l") + "e") + "h"
→ "olleh"

///
🪜 Call Stack Visualization
Here’s what happens on the call stack:
///
Call	Value Returned
reverseString("hello")	waits for result of "ello"
reverseString("ello")	waits for result of "llo"
reverseString("llo")	waits for result of "lo"
reverseString("lo")	waits for result of "o"
reverseString("o")	returns "o" (base case!)

///
Then it resolves upward:
reverseString("lo")    → "o" + "l"  = "ol"
reverseString("llo")   → "ol" + "l" = "oll"
reverseString("ello")  → "oll" + "e" = "olle"
reverseString("hello") → "olle" + "h" = "olleh"

///
function reverseString(str) {
  if (str.length <= 1) return str;
  return reverseString(str.slice(1)) + str[0];
}

```



## 05/14/2025 Wed
js 
```
function recursiveSum(n) {
  if (n === 1) {
    return 1;
  }
  return n + recursiveSum(n - 1);
}
```
-----
recursiveSum(3)
  -> recursiveSum(2)
    -> recursiveSum(1)
-----
Then it unwinds:
-----
recursiveSum(1) returns 1
recursiveSum(2) returns 2 + 1 = 3
recursiveSum(3) returns 3 + 3 = 6

🧠 In short:
recursion uses the call stack.

Every recursive call waits for the next one to finish before it can complete.

This is why deeply recursive functions can run into a "Maximum call stack size exceeded" error — the stack has a size limit.





## 05/12/2025 
94. Binary Tree Inorder Traversal
https://leetcode.com/problems/binary-tree-inorder-traversal/description/



```
var inorderTraversal = function(root) {
    let result = []
    let current = root;

    //morris algorithm
    //1 tourist(current) 
    //2 while the tourist is not null
    //3 set a guide(current.left) to look at the left sub tree
    //4if there's no left sub node, then push that node to the result
  
        while(current !== null){
            let leftNode = current.left; //referencing 

            if(current.left !== null){
                    while(leftNode.right !== null && leftNode.right !==current){
                        leftNode = leftNode.right;
                    }
                    if(leftNode.right === null ){
                        leftNode.right = current;
                        current = current.left;
                    } else {
                        leftNode.right = null
                        result.push(current.val);
                        current = current.right
                    } 
                } else {
                result.push(current.val)
                current = current.right
            }
        }
    return result
};
```

```
var inorderTraversal = function(root) {
    // Array to store the result (node values in inorder)
    const result = [];
    
    // Stack to keep track of nodes
    const stack = [];
    
    // Current node pointer
    let current = root;
    
    // Continue until we've processed all nodes
    while (current !== null || stack.length > 0) {
        // Traverse to the leftmost node, pushing all nodes along the way
        while (current !== null) {
            stack.push(current);
            current = current.left;
        }
        
        // Pop the last node (leftmost unprocessed node)
        current = stack.pop();
        
        // Process the node (add value to result)
        result.push(current.val);
        
        // Move to the right subtree
        current = current.right;
    }
    
    return result;
};
```


## 05/05/2025  
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
js
```
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

```