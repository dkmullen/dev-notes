# Time Complexity

## Constants and smaler terms don't matter

- 0(500) simplifies to 0(1) -constant - Means that no matter how many inputs, the function runs once
- O(2n) simplifes to O(n) - linear - The function runs n times (n = num of inputs)
- O(1000n + 50) simplifies to O(n)
- 0(13n^2) simplifies to 0(n^2) - quadratic - The function runs n^2 times

- O(n^3) Cubic
- O(2n) Exponential

The trend is the same no matter how much the function is doing. If one input causes 500 operations and 2 inputs cause 1000, etc., that's linear growth (O(n)) no matter what.

## Big O Shorthands in code

1. Arithemtic operations are constant
2. Var assignment is constant
3. Accessing elements in an array (by index) or object (by key) is constant
4. In a loop, the complexity is the length of the loop times the complexity of whatever happens in the loop

# Space Complexity

The amount of memory taken up; here we focus on the inside of the algorithm

- Most primitives are constant space
- Strings require O(n) space (50 chars takes up 50 'spaces')
- Reference types generally are O(n) where n is the len of an array or the num of keys in an obj

```
// Takes an array of numbers
function sum (array) {
  let count = 0;
  array.forEach((i) => {
    count+=i;
  })
  return count;
}
sum([1,2,3,4,5,6])
```

The above is O(1) space b/c there is only the count variable plus the current 'i'; It is O(n) time because the loop runs once for each item in the array

```
// Takes an array of numbers
function double (array) {
  let newArray = [];
  array.forEach((i) => {
      newArray.push(2 * i)
  })
  return newArray;
}
double([1,2,3,4,5,6])
```

The above is O(n) space because the len of the array input determins the length of the output;

## Logarithms

The inverse of exponetiation

- log2(8) = 3 - log base 2 of 8 = 3, or 2^3 = 8
- The above could be expressed: 2 to what power gives us 8?

For shorthand, it's common to say log(8), refering to base 2. The log of a number roughly measures the number of times you can divide it by two before you get a value that is less than or equal to one.

O(log n) is very good time complexity, just a bit slower than O(1)

=====

## Complexity of JS objects and their methods

### Objects

- **Insertion, removal, access** of items in an object is O(1), or constant time, the best we can do.
- **Searching** is O(N), or linear. Might have to look at items one by one to find a certain value, so function runs as many times as there are values.

- **Object.keys, Object.values, Object.entries** = O(n)
- **<myObject>.hasOwnProperty('property')** = O(1)

### Arrays

Order can come at a cost. Use when you need order; otherwise, maybe not.

- **Access** by index = O(1)
- **Adding to / removing from the end** (push & pop) - O(1)
- **Adding to ? removing fromthe beginning** (unshift, shift) - O(N) b/c everything has to be reindexed
- **Searching** O(N)
- **Concat, slice, splice, forEach, map, filter, reduce, etc.** - O(N)
  **Sort** - O(N \* log N)

Takeaways - Objects are fast when you don't need order. With arrays, add and remove to the end if you can.
