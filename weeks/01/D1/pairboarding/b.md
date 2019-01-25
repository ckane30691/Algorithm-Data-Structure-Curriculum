# Partner B

## Three Number Sum
​
Write a function that takes in a non-empty array of distinct integers and an integer representing a target sum. The function should find all triplets in the array that sum up to the target sum and return a two-dimensional array of all these triplets. The numbers in each triplet should be ordered in ascending order, and the triplets themselves should be ordered in ascending order with respect to the numbers they hold. If no three numbers sum up to the target sum, the function should return an empty array.

Sample input: `[12, 3, 1, 2, -6, 5, -8, 6], 0`
Sample output: `[[-8, 2, 6], [-8, 3, 5], [-6, 1, 5]]`

```JavaScript
function threeNumberSum(array, targetSum) {
  // Write your code here.
}
```

### Hint 1
Try sorting the array and traversing it once. At each number, place a left pointer on the number immediately to the right of your current number and a right pointer on the final number in the array. Check if the current number, the left number, and the right number sum up to the target sum. How can you proceed from there, remembering the fact that you sorted the array?

### Hint 2
Since the array is now sorted (see Hint #1), you know that moving the left pointer mentioned in Hint #1 one place to the right will lead to a greater left number and thus a greater sum. Similarly, you know that moving the right pointer one place to the left will lead to a smaller right number and thus a smaller sum. This means that, depending on the size of each triplet's (current number, left number, right number) sum relative to the target sum, you should either move the left pointer, the right pointer, or both to obtain a potentially valid triplet.

## Solution
```JavaScript
// O(n^2) time | O(n) space
function threeNumberSum(array, targetSum) {
  array.sort((a, b) => a - b);
  const triplets = [];
  for (let i = 0; i < array.length - 2; i++) {
    let left = i + 1;
    let right = array.length - 1;
    while (left < right) {
      const currentSum = array[i] + array[left] + array[right];
      if (currentSum === targetSum) {
        triplets.push([array[i], array[left], array[right]]);
        left++;
        right--;
      } else if (currentSum < targetSum) {
        left++;
      } else if (currentSum > targetSum) {
        right--;
      }
    }
  }
  return triplets;
}
```