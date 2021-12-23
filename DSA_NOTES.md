# DSA NOTES

### Array Rotation in O(n) time and O(1) space
- reverse the partial arrays
- then reverse the whole array
- keep in mind to reduce k(rotation factor) if k>=array.size() 

### Maximum Subarray or Kandane's Algorithm O(n) time O(1) space
- suppose you have localMaxSubArray ending at previous index
- then the localMaxSubArray for current index will be ```max(localMaxSubArray+arr[i] , arr[i])```


