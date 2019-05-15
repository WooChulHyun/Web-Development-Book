# Control statement

### Control statement

Typically, the code is executed sequentially from top to bottom. Control statements can be used to artificially control the execution flow of code.

| Classification | Control statement |
| :--- | :--- |
| Conditional statement | if/else, switch, try/catch/finally |
| Loop statement | while, do/while, for, for/in, for/of |
| Jump statement | break, continue, return, throw |

#### 

### Conditional statement

A conditional statement determines the execution of a code block\(block statement\) according to the evaluation of a given conditional expression. A conditional expression is an expression that can be evaluated as a Boolean value.



#### **if/else**

if/else statement determines the code block to execute according to the evaluation result of the given conditional expression \(an expression that can be evaluated as a Boolean value\), that is, a logical true or false. If the evaluation result of the conditional expression is not a boolean value, it is coerced into a Boolean value to distinguish logical true or false.

```javascript
if (conditional expression) {
  // This code block is executed if the conditional expression is true.
} else {
  // This code block is executed if the conditional expression is false.
}
```

If you want to add a conditional expression, use the else if statement.

The else if and else statements are optional and may not be used. The if and else statements can not be used more than once, but else if statements can be used multiple times.

```javascript
if (conditional expression 1) {
  // This code block is executed if the conditional expression 1 is true.
} else if (conditional expression 2) {
  // This code block is executed if the conditional expression 2 is true.
} else if (conditional expression 3) {
  // This code block is executed if the conditional expression 3 is true.
}else {
  // If conditional expression 1,2 and 3 are all false, this code block is executed.
}
```

```javascript
const x = 2;
let result;

if (x % 2) {
  // 2 % 2 is 0 and 0 is false
  result = 'odd';
} else {
  result = 'even';
}

console.log(result); // even
```

```javascript
let year;

if (year % 400 === 0 || (year % 4 == 0 && year % 100 !== 0)) {
  console.log('leap year');
}

```

\*\*\*\*

#### **switch**

The switch statement evaluates a given expression and moves the execution order into a case statement with an expression that matches the value. The case statement specifies an expression that represents a case and ends with a colon. Then place the statements to be executed.

If there is no case statement with an expression that matches the expression in the switch statement, the execution sequence moves to the default statement. It can be used with the default option or not.

```javascript
switch (expression statement) {
  case expression statement1:
    //The statement to be executed if the expression in the switch
    //statement matches the expression 1
    break;
  case expression statement2:
    //The statement to be executed if the expression in the switch
    //statement matches the expression 2
    break;
  default:
    //a statement to be executed when there is no case statement
    //with an expression that matches the expression in the switch statement;
}
```

```javascript
const month = 9;
let monthName;

switch (month) {
  case 1:
    monthName = 'January';
    break;
  case 2:
    monthName = 'February';
    break;
  case 3:
    monthName = 'March';
    break;
  case 4:
    monthName = 'April';
    break;
  case 5:
    monthName = 'May';
    break;
  case 6:
    monthName = 'June';
    break;
  case 7:
    monthName = 'July';
    break;
  case 8:
    monthName = 'August';
    break;
  case 9:
    monthName = 'September';
    break;
  case 10:
    monthName = 'October';
    break;
  case 11:
    monthName = 'November';
    break;
  case 12:
    monthName = 'December';
    break;
  default:
    monthName = 'Invalid month';
}

console.log(monthName); // September
```

```javascript
const year = 2000;
const month = 2;
let days = 0;

switch (month) {
  case 1:
  case 3:
  case 5:
  case 7:
  case 8:
  case 10:
  case 12:
    days = 31;
    break;
  case 4:
  case 6:
  case 9:
  case 11:
    days = 30;
    break;
  case 2:
    days =            (year % 4 === 0 && year % 100 !== 0) || year % 400 === 0 ? 29 : 28;
    break;
  default:
    console.log('Invalid month');
}

console.log(days); // 29
```



### Loop Statement

A loop statement executes a code block when the evaluation result of a given conditional expression is true. Then check the conditional expression again and if it is still true, run the code block again. This is repeated until the conditional expression is false.

\*\*\*\*

#### **while**

The while statement executes the code block repeatedly if the evaluation result of the given conditional expression is true. If the evaluation result of the condition statement becomes false, the execution is terminated.

```javascript
let count = 0;

while (count < 3) {
  console.log(count);
  count = count + 1;
} // 0 1 2
```

```javascript
function fact(n) {
  let k = 1;
  let i = 1;
  while (i < n) {
    console.log('i: ' + i + ', k: ' + k);
    k *= ++i;
  }
  console.log('i: ' + i + ', k: ' + k);
  return k;
}

console.log(fact(5)); // 120

// i: 1, k: 1
// i: 2, k: 2
// i: 3, k: 6
// i: 4, k: 24
// i: 5, k: 120
```

\*\*\*\*

#### **do/while**

do/while statement executes the code block first and evaluates the conditional expression. Therefore, the code block is executed more than once.

```javascript
function fact(n) {
  let k = 1;
  let i = n;
  do {
    k *= i--;
  } while (i > 0);
  return k;
}

console.log(fact(5)); // 120
```

\*\*\*\*

#### **for**

```javascript
for (Variable declaration or assignment statement;
        Conditional expression; Increase / decrease expression) {
  //Statement to be repeated if conditional expression is true;
}
```

```javascript
for (let i = 0; i < 5; i++) {
  console.log(i);
}
// 0
// 1
// 2
// 3
// 4
```

> step 1: i = 0
>
> step 2: Is i less than 5? --&gt; true
>
> step 3: console.log\(i\) --&gt; 0 \(currently i = 0\)
>
> step 4: \(i = i + 1\) === \(i++\) --&gt; i = 1
>
> step 5: Is i less than 5? --&gt; true
>
> step 6: console.log\(i\) --&gt; 1 \(currently i = 1\)
>
> step 7: \(i = i + 1\) === \(i++\) --&gt; i = 2
>
> if i === 5
>
> step 8: Is i less than 5? --&gt; false --&gt; stop

```javascript
for (let i = 0; i < 10; i += 2) {
  console.log(i);
}

// 0
// 2
// 4
// 6
// 8
```

```javascript
for (let i = 0; i < 10; ) {
  console.log(i);
  i += 2;
}

// 0
// 2
// 4
// 6
// 8
```

\*\*\*\*

#### **Nested loop**

```javascript
const N = 20;

for (let a = 1; a <= N; a++) {
  for (let b = 1; b <= N; b++) {
    for (let c = 1; c <= N; c++) {
      if (a * a + b * b === c * c) {
        console.log(`${a}^2 +${b}^2 = ${c}^2`);
      }
    }
  }
}

// 3^2 +4^2 = 5^2
// 4^2 +3^2 = 5^2
// 5^2 +12^2 = 13^2
// 6^2 +8^2 = 10^2
// 8^2 +6^2 = 10^2
// 8^2 +15^2 = 17^2
// 9^2 +12^2 = 15^2
// 12^2 +5^2 = 13^2
// 12^2 +9^2 = 15^2
// 12^2 +16^2 = 20^2
// 15^2 +8^2 = 17^2
// 16^2 +12^2 = 20^2
```

\*\*\*\*

#### **for/in**

```javascript
const ALPHABET = ["a", "b", "c", "d"];

for (const key in ALPHABET) {
  console.log(key);
}

// 0 --> index
// 1 --> index
// 2 --> index
// 3 --> index
```

```javascript
const ALPHABET = ["a", "b", "c", "d"];

for (const key in ALPHABET) {
  console.log(ALPHABET[key]);
}

// a
// b
// c
// d
```

```javascript
const USER_INFO = {
  name: 'hi',
  age: 20
};

for (const key in USER_INFO) {
  console.log(key);
}

// name
// age
```

```javascript
const USER_INFO = {
  name: "hi",
  age: 20
};

for (const key in USER_INFO) {
  console.log(userInfo[key]);
}

// hi
// 20
```



### Jump Statement

#### **label**

Usage:

> label name: statement

If you put label to sentence, you can jump to it after executing break or continue statement.

```javascript
foo: {
  console.log(1);
  break foo; // Escape foo block statement.
  console.log(2);
}

// 1
```

\*\*\*\*

#### **break**

The labeled break statement is used to exit the entire loop, usually within the inner loop of the nested loop.

```javascript
const B = [8, 9, 7, 3, 5];

for (let i = 0; i < A.length; i++) {
  for (let j = 0; j < B.length; j++) {
    if (A[i] === B[j]) {
      console.log(`${A[i]} ${B[j]}`);
    }
  }
}

// 3 3
// 5 5
```

```javascript
const A = [1, 2, 3, 4, 5];
const B = [8, 9, 7, 3, 5];

loop: for (let i = 0; i < A.length; i++) {
  for (let j = 0; j < B.length; j++) {
    if (A[i] === B[j]) {
      console.log(`${A[i]} ${B[j]}`);
      break loop;
    }
  }
}


// 3 3
```

\*\*\*\*

#### **continue**

|  |  |
| :--- | :--- |
| While | Go back to the beginning of the loop and reevaluate the conditional expression. If the result is true, the loop is executed from the beginning. |
| do/while | Skips the middle and evaluates the last conditional expression of the loop. If the result is true, the loop is executed from the beginning. |
| for | Evaluates conditional expressions after executing iterative expressions. If the result is true, the loop is executed successively. |
| for/in | Go back to the beginning of the loop. Starts working on the next property of the property assigned to the specified variable. |

```javascript
let i = 0;
let n = 0;

while (i < 5) {
  i++;

  if (i === 3) {
    continue;
  }

  n += i;
  console.log(n);
}

// 1
// 3
// 7
// 12
```

```javascript
const A = [1, -2, 3, -4, 5];

for (let i = 0, sum = 0; i < A.length; i++) {
  if (A[i] < 0) continue;
  sum += A[i];
  console.log(sum);
}

// 1
// 4
// 9
```

