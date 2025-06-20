# 8pm-algo-club

## ⏱ Time complexity = How many steps the algorithm takes as input size grows.

## 🧠 Space complexity = How much extra memory it uses as input size grows.

## 6/19
https://leetcode.com/problems/remove-duplicates-from-sorted-array/?envType=problem-list-v2&envId=array
26. Remove Duplicates from Sorted Array

```js
  if (nums.length === 0) return 0;

  let k = 1; // pointer to place the next unique element

  for (let i = 1; i < nums.length; i++) {
    if (nums[i] !== nums[i - 1]) {
      nums[k] = nums[i];
      k++;
    }
  }

  return k;
```
//For every new number that’s not equal to the one before, copy it to nums[k] and increment k.


## 6/16 
https://leetcode.com/problems/remove-element/description/?envType=problem-list-v2&envId=array
27. Remove Element
```js
function removeElement(nums, val) {

    let result = 0;
    for(let i = 0; i < nums.length; i++) {
        if(nums[i] === val) nums[i] = '_';
        else result++;
    }
    nums.sort((a, b) => a === '_' ? 1 : -1);
    return result;

```


## 6/12
https://leetcode.com/problems/contains-duplicate/
217. Contains Duplicate


```js

| Version                 | Time Complexity  | Space Complexity       | Notes                                    |
|-------------------------|------------------|------------------------|------------------------------------------|
| `.forEach()` + `.filter()`| ❌ O(n²)      | ❌ O(n²) (temp arrays)  | Very inefficient                        |
| `Set`                  | ✅ O(n)           | ✅ O(n)                | Best mix of readability & performance    |
| `Object`               | ✅ O(n)           | ✅ O(n)                | Works                                    |


function containsDuplicate (nums) {
    let isRepeated = false;

    nums.forEach((currentNumber, index) = {
        const numsNotCurrentNum = nums.filter((num, idx) => num === currentNumber);
          if (numsNotCurrentNum.length > 1) {
          isRepeated = true;
    );
    return isRepeated;
}



var containsDuplicate = function (nums) {

    const set = new Set();
    for (let i = 0; i < nums.length; i++) {
        if (set.has(nums[i])) {
            return true;
        }
        else {
            set.add(nums[i])
        }

    }
    return false;
};

// 

    let obj = {}

    for(let i = 0; i < nums.length; i++){
        console.log(obj.hasOwnProperty(obj[nums[i]]))
        if (obj.hasOwnProperty(obj[nums[i]])){
            return true
        }

        obj[nums[i]] = 1
    
    }
    console.log(obj)
    return false

```

## 6/5
https://leetcode.com/problems/valid-palindrome/description/
125. Valid Palindrome

```js
function isPalindrome(phrase) {
  const alphanumerics = "abcdefghijklmnopqrstuvwxyz0123456789";
  const cleaned = [];

  // Step 1: Build cleaned version with only lowercase letters and numbers
  for (let i = 0; i < phrase.length; i++) {
    const char = phrase[i].toLowerCase();
    if (alphanumerics.includes(char)) {
      cleaned.push(char);
    }
  }

  // Step 2: Use two-pointer approach to check palindrome
  let left = 0;
  let right = cleaned.length - 1;

  while (left < right) {
    if (cleaned[left] !== cleaned[right]) {
      return false;
    }
    left++;
    right--;
  }

  return true;
}

// ✅ Try it
console.log(isPalindrome("A man, a plan, a canal: Panama")); // true
console.log(isPalindrome("No lemon, no melon")); // true
console.log(isPalindrome("race a car")); // false

```



## 6/2/2025 Mon
https://leetcode.com/problems/valid-anagram/description/
Valid Anagram

* most optimal 
```js
var isAnagram = function(s, t) {
    if (s.length !== t.length) return false;

    const count = new Array(26).fill(0);
    const aCharCode = 'a'.charCodeAt(0);

    for (let i = 0; i < s.length; i++) {
        count[s.charCodeAt(i) - aCharCode]++;
        count[t.charCodeAt(i) - aCharCode]--;
    }

    // If all counts are zero, t is an anagram of s
    return count.every(c => c === 0);
};
```

⏱ Time Complexity: O(n)
n = length of the strings.

Goes through both strings once → total time = n.

🧠 Space Complexity: O(1)
Fixed size array of 26 letters (a to z), doesn't grow with input.

✅ Fastest and most memory-efficient version, but assumes only lowercase a–z letters.



* 
```js
var isAnagram = function(s, t) {
    if (s.length !== t.length) return false;
    let objs={};
    let objt={};
    for(let i=0;i <s.length;i++){
        if(objs[s[i]]){
            objs[s[i]]++;
        }
        else
        objs[s[i]]=1;
    }
    for(let i=0;i<s.length;i++){
        if(objt[t[i]]){
            objt[t[i]]++;
        }
        else
        objt[t[i]]=1;
    }
    for(let val in objs){
        if(objs[val]!=objt[val])return false;
    }
    return true;
};
```
⏱ Time Complexity: O(n)
Goes through both strings → O(n).

🧠 Space Complexity: O(k)
k = number of unique characters.

Worst case: if every letter is different → extra space grows with input.

✅ Easier to understand and works with any characters (Unicode-friendly), but uses more memory.

*
```js
var isAnagram = function(s, t) {

    if(s.length !== t.length){
        return false
    } else {

    let dictionary = {}

    for (let i = 0; i < s.length; i++){
        console.log(s[i])
        if(dictionary[s[i]]){
            dictionary[s[i]] +=1
        }else{
            dictionary[s[i]] = 1
        }
    }
    console.log(dictionary)

    for (let i = 0; i < t.length; i++){
        console.log(t[i])
        if(dictionary[t[i]]){
            dictionary[t[i]] -=1
        }else{
            dictionary[t[i]] = 1
        }
    }
    console.log(dictionary)

    let added = 0

    for (const key in dictionary){
        if(dictionary.hasOwnProperty(key)){
            const value = dictionary[key]
            added += value
        }
    }

    if( added === 0 ){
        return true
    }
    }

    return false
};
```
⏱ Time Complexity: O(n)
Loops through both strings, and a small loop at the end → still O(n).

🧠 Space Complexity: O(k)
One object instead of two → slightly better space usage than solution #2.

Still depends on unique letters.

✅ Memory-efficient and works with any characters. Clean logic.





## 5/29/2025 Thurs
https://leetcode.com/problems/climbing-stairs
70. Climbing Stairs

```js
var climbStairs = function(n) {
    let one = 1;
    let two = 1;

    for (let i = 0 ; i < n-1; i ++){
        console.log(i)
        let temp = one;
        one = one + two
        two = temp
    }
    return one
};
```
## 05/22/2025 Thurs
https://leetcode.com/problems/best-time-to-buy-and-sell-stock/


```js
var maxProfit = function(prices) {
  let result = 0

  for ( let i = 0; i < prices.length; i++) {

        console.log("-----i-----", prices[i])

        let maxJ = 0
        let profit = 0
    for (let j = i+1; j < prices.length; j++){
   
        if(prices[j] > maxJ){
            maxJ = prices[j]
        }

        console.log("-j-", prices[j])
        console.log("---maxJ--", maxJ)

        profit = maxJ - prices[i]
        console.log("DDDD", profit)
    }

    if(profit > result){
        result = profit
        }
    console.log("+++R++", result)
  }
  return result

};
```


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