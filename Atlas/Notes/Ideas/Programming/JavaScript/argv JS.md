---
up:
  - "[[JavaScript MOC]]"
related: 
created: 2024-06-19
---

It is used to get the arguments passed to the node.js process when run in the command line.

```js
process.argv
```

**Return Value:** This property returns an array containing the arguments passed to the process when run it in the command line. The first element is the process execution path and the second element is the path for the js file.

## Examples
```js
// Include process module
const process = require('process');

// Printing argv property value
console.log(process.log);

// node index.js extra_argument1 extra_argument2 3
/* 
[ 'C:\\Program Files\\nodejs\\node.exe',
  'C:\\nodejs\\g\\process\\argv_1.js',
  'extra_argument1',
  'extra_argument2',
  '3' 
]
*/
```

```js
// Include process module
const process = require('process');

// Printing process.argv property value
var args = process.argv;

console.log("number of arguments is "+args.length);

args.forEach((val, index) => {

    console.log(`${index}: ${val}`);

});

// node index.js extra_argument1 extra_argument2 3
/* 
number of arguments is 5
0: C:\Program Files\nodejs\node.exe
1: C:\nodejs\g\process\argv_2.js
2: extra_argument1
3: extra_argument2
4: 3
*/
```