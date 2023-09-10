**Algorithm** - A process or set of steps to accomplish a task

## Problem Solving

### 1. Understand the Problem

**Example:** Write a function that takes in two numbers and returns their sum.

- **Can I restate the problem in my own words?**
- **What are the inputs that go into the problem?** - Might be more complicated than two numbers - are they int, float, etc.? How large? (JS for example won't add extremely large numbers)
- **What are the outputs that should come from the solution?** Should I return a string, a float, a rounded number, or maybe answer with an object?
- **Can the outputs be determined from the inputs?** (ie, do I have enough info to solve the problem? May not know for sure until we dive in) - What to do if we get only one input, or three?
- **How should I label the important pieces of data that are part of the problem?** `function add(num1, num2) {...} etc` For more complex functions, labeling is a step toward understanding.

### 2. Explore Concrete Examples

**Example:** Write a function that takes in a string and returns counts of each character in the string.

- **Start with simple examples** - `charCount('aaaa')` -> `{a: 4}` - This is one example of how I might render the solution. Or maybe assume that the alphabet is a starting point, and I'd just increment the count, ie `{ a:4, b:0, c:0, etc }`

- **Progress to more complex examples, empty inputs, invalid inputs** - What if someone enters numbers, or a boolean, or nothing? What should I do with spaces/punctuation?

### 3. Break It Down

From the example for #2, write out steps to take:

```
function charCount(str) {
  // make object to hold results
  // loop over str
    // if char is alphanumberic, AND is a key in the object, add one to the key's value
    // if char is alphanumberic, AND is NOT a key in the object, add key to object with value of 1
    // For other kinds of data (non-alphanumeric) skip
  // return object
}
```

In an interview, if you run out of time, or even don't complete the coding, you have still shown your process

### 4. Solve/Simplify

- **Find the core difficulty of the problem** (ie, the scary part) - It could be making sure each char is alphanumeric. Might draw a blank on the best way to do it. So...
- **Temporarily ignore it** - Just put everything into the object and plan to come back to it once the function is (mostly) working
- **Write a simplified solution**
- **Then incorporate that difficulty back in**

The key in an interview is, even when confused, to demonstrate your process, your problem-solving ability

### 5. Look Back and Refactor

- **Can you check the result?**
- **Can you derive the result differently?**
- **Can you understand it at a glance?**
- **Can you use the result or method for some other problem?**
- **Can you improve the performance of your solution?**
- **Can you think of other ways to refactor?**
- **How have others solved this problem?**

`obj[char] = obj[char] > 0 ? obj[char]++ : 1;` can be simplified to `obj[char] = obj[char]++ || 1;` In each case, if obj[char] already exists in my object, we increment its value; otherwise, we add it with a value of 1;

\*\*George Polya, How to Solve It
