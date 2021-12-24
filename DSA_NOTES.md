# DSA NOTES

- #### Array Rotation in O(n) time and O(1) space
  - reverse the partial arrays
  - then reverse the whole array
  - keep in mind to reduce `k(rotation factor)` if `k>=array.size()` 

- #### Maximum Subarray or Kandane's Algorithm O(n) time O(1) space
  - suppose you have localMaxSubArray ending at previous index
  - then the localMaxSubArray for current index will be `max(localMaxSubArray+arr[i] , arr[i])`

- #### Best Time to Buy and Sell Stock [LeetCode Problem](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)
  - keep track of the `minOnLeft` and `maxProfit`
  - in each traversal if `arr[i]` is less than `minOnLeft` update it or else update `maxProfit` as `max(maxProfit,minOnLeft-arr[i])`

- #### Why we use `m = l+(r-l)/2` instead of `m = (l+r)/2` in Binary Search
  - To avoid overflow in case l and r are close to INT_MAX


