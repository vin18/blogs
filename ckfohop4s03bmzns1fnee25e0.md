## DSA - Find the duplicate number in an array

## Introduction
Welcome to the first post of the series, **Data Structures and Algorithms Playlist**. In this series, we will solve commonly asked Data Structures and Algorithm questions that are asked during interviews. We will start with a brute force solution and get to the optimal solution while discussing various time and space complexities of every approach. <br>
In this article, we will solve the question -  **Find the duplicate number in an array**.

## Prerequisite:
Basic understanding of arrays. 

## Problem statement

Given an array of integers `nums` containing `n + 1` integers where each integer is in the range `[1, n]` inclusive.

There is only one duplicate number in `nums`, return this duplicate number. If there is no duplicate return `-1`.

Example 1: <br>
Input: nums = [1, 3, 4, 2, 2] <br>
Output: 2 

Example 2: <br>
Input: nums = [3, 1, 3, 4, 2] <br>
Output: 3

Problem link: [Leetcode](https://leetcode.com/problems/find-the-duplicate-number/) <br>
Category: Arrays

## Solution 1: Basic approach
```
// Brute Force approach
public static int findDuplicate(int arr[]) {
  for (int i = 0; i < arr.length; i++) {
    for (int j = 0; j < arr.length; j++) {
       if (arr[i] == arr[j]) 
        return arr[i];
    }
  }
  return -1;
}
// Time Complexity: O(n^2)
// Space Complexity: O(1)
```

1. Iterate through every element of an array using a loop.
2. For each element, we will use another loop to iterate the rest of the elements.
3. Compare the `arr[i]` with `arr[j]`.
4. If the element is found return that element, `arr[i]`.
5. If not found, return `-1`.

We are using two nested loops, one for iterating each element and another to compare that element through the rest of the elements in the array. Hence, the time complexity of this approach is `O(n^2)`.
Since we are not using any extra array, space complexity is O(1).

## Solution 2 - By Sorting Arrays
```
public static int findDuplicate(int arr[]) {
  if (arr.length <= 0) {
    return -1;
  }
  Collections.sort(arr);
  for (int i = 0; i < arr.length; i++) {
    if (arr[i] == arr[i + 1]) {
      return arr[i];
    }
  }
  return -1;
}
```
1. We handle the edge case if the array is empty or not. If it's empty simply return `-1`.
2. We sort the array using a good sorting algorithm like merge or quicksort. We can also use the built-in sort() method in Java.
3. We use a loop to iterate through the array.
4. After sorting the array, there would be one instance where the duplicate elements are present in the consecutive memory locations. We check for that condition - `arr[i] == arr[i + 1]`.
5. If it's true, we return that element, `return arr[i]`.
6. If the element is not found, we simply return `-1`.

In this approach, we are sorting the array using Collections.sort() (internally uses Merge sort) that takes `O(n logn)`. Also, we are iterating through all elements to compare two consecutive memory locations. So, the total time complexity is `O(n logn + n)`. We drop the lower term, hence the time complexity of this approach is O(n logn). 
We are not using any extra space, hence the space complexity of this approach is O(1).

## Solution 3 - By using Hashmaps
```
public static int findDuplicate(int arr[]) {
  int output[] = new int[arr.length];

}
```
