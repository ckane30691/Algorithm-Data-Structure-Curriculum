# Partner A

## Smallest Difference (From algoexpert.io)
​
Write a function that takes in two non-empty arrays of integers. The function should find the pair of numbers (one from the first array, one from the second array) whose absolute difference is closest to zero. The function should return an array containing these two numbers, with the number from the first array in the first position. Assume that there will only be one pair of numbers with the smallest difference.

```JavaScript
function smallestDifference(arrayOne, arrayTwo) {
  // Write your code here.
}
```

### Hint 1
Would it help if the two arrays were sorted? If the arrays were sorted and you were looking at a given pair of numbers, could you efficiently find the next pair of numbers to look at? What are the runtime implications of sorting the arrays?

### Hint 2
Start by sorting both arrays, as per Hint #1. Put a pointer at the beginning of both arrays and evaluate the absolute difference of the pointer-numbers. If the difference is equal to zero, then you've found the closest pair; otherwise, increment the pointer of the smaller of the two numbers to find a potentially better pair. Continue until you get a pair with a difference of zero or until one of the pointers gets out of range of its array.

## Solution

```JavaScript
// O(nlog(n) + mlog(m)) time | O(1) space
function smallestDifference(arrayOne, arrayTwo) {
  arrayOne.sort((a, b) => a - b);
  arrayTwo.sort((a, b) => a - b);
  let idxOne = 0;
  let idxTwo = 0;
  let smallest = Infinity;
  let current = Infinity;
  let smallestPair = [];
  while (idxOne < arrayOne.length && idxTwo < arrayTwo.length) {
    let firstNum = arrayOne[idxOne];
    let secondNum = arrayTwo[idxTwo];
    if (firstNum < secondNum) {
      current = secondNum - firstNum;
      idxOne++;
    } else if (secondNum < firstNum) {
      current = firstNum - secondNum;
      idxTwo++;
    } else {
      return [firstNum, secondNum]
    }
    if (smallest > current) {
      smallest = current;
      smallestPair = [firstNum, secondNum]
    }
  }
  return smallestPair;
}
```