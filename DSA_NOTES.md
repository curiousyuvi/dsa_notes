# DSA NOTES

- #### Array Rotation in O(n) time and O(1) space (Double Reverse Method)
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

- #### Two sum (Two pointer appraoch) O(n) time and O(1) space [LeetCode Problem](https://leetcode.com/problems/two-sum/)
  -  We first sort the array
  -  then we take two integers as `i = 0` and `j = n-1`
  -  then in a `while(i<j)` loop we check if `arr[i] + arr[j] < target` so we increase `i` , if `arr[i] + arr[j] > target` we decrease `j` and else we get our answer

- #### Merge two sorted arrays in O(1) space (Gap Method)
  - First calculate `gap = ceil(m+n/2)`
  - Take two elements from start seperated from gap and swap them if fomer is grater than later and kepp on traversing
  - then calculate gap again by `gap = ceil(gap/2)` and do the same steps
  - break the loop after `gap == 1`

- #### Move Zeroes (Two pointer approach)[LeetCode Problem](https://leetcode.com/problems/move-zeroes/) 
  - We take keep track of index of zero element from start
  - We traverse the array and if `arr[i]!=0`, we swap it with `arr[j]` and do `j++` but if `arr[i]==0` we just `continue`
  - Code Snippet :
  ```c++
  
  void moveZeroes(vector<int>& nums) {
        
        int n=nums.size(),j=0;
                
        
        for(int i=0;i<n;i++)
        {
          if(nums[i]!=0 && nums[j]==0){
              swap(nums[i],nums[j]);
          }
            
            if(nums[j]!=0)
                j++;
            
        }
        
    }
  ```
- #### Find first and last occurence of an integer in a sorted array in O(log n) time.
  ```c++
  
  int binSearch(vector<int>& nums, int target,int searchType){
        int l=0,r=nums.size()-1,m,best=-1;
        
        
        
        
        while(l<=r){
            m=l+(r-l)/2;
            if(nums[m]==target){
                best=m;
                if(searchType==-1)
                   {r=m-1;}
                else if(searchType==1)
                    {l=m+1;}
                else
                    break;
                
            }
            else if(nums[m]<target)
            l=m+1;
            else if(nums[m]>target){
                r=m-1;
            }
            
        }
        
        
        
        
        return best;
    }
    
    vector<int> searchRange(vector<int>& nums, int target) {
        
        
        if(nums.size()==1){
            if(target==nums[0]){
                vector<int> ans={0,0};
                return ans;
            }
        }
        int a=-1,b=-1;
        
        
        
        if(binSearch(nums,target,0)!=-1){
            a=binSearch(nums,target,-1);
            b=binSearch(nums,target,1);
            
        }
        
        vector<int> ans={a,b};
            return ans;
    }
    
    ```


