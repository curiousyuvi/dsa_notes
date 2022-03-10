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

- Book allocation [problem](https://www.codingninjas.com/codestudio/problems/allocate-books_1090540) | Painter's partition [problem](https://www.codingninjas.com/codestudio/problems/painter-s-partition-problem_1089557) (using Binary Search O(n log n))
  - code snippet -
   ```c++
   bool isPossibleAnswer(int mid,vector<int>& arr,int n,int m){
    int i=0;
   while(m--){
       int sum=0;
       while(i<n){
           if((sum+arr[i])<=mid)
           {
               sum+=arr[i];
           }
           else
           break;
           i++;
       }
   }
    if(i<=n-1){
        return false;
    }
    
    return true;
    
   }
  int allocateBooks(vector<int> arr, int n, int m) {
    
      if(n<m)
          return -1;
        
        int sum=0;
        for(int i=0;i<n;i++){
            sum+=arr[i];
        }
        
        int min=0,max=sum,mid,ans=0;
    
        
        
        while(min<=max){
            mid=min+(max-min)/2;
            
            if(isPossibleAnswer(mid,arr,n,m))
                {
                   max=mid-1;
                   ans=mid;
                }
            else
                min=mid+1;
            
        }
    
       return ans;
    }
   ```

- Check if `n` is part of Fibonacci Sequence
  - if **(5n<sup>2</sup> - 4)** or **(5n<sup>2</sup> + 4)** is a perfect square

- **Stable vs Unstable sort** - In *stable sort* the order of elements with same value is not changed i.e. `i < j and A[i] = A[j] and m < n` while in *unstable     sort* the order is not preserved.

- **Sorting Algorithms**
  - **Selection Sort** O(n<sup>2</sup>) (unstable) : <br>
  In selection sort we have `n-1` rounds and in each round we take the minimum element to its right place, and eventually in every round we get sorted array part   from the start.
  
  - **Bubble Sort** O(n<sup>2</sup>) (stable) : <br>
  In bubble sort we have `n-1` rounds ande in each round we traverse the array and keep on checking two adjacent elemts and swap them if they are in wrong order,   thus in each traversal we take the maximum element to its right position, and eventually in every round we get sorted array part from the end.
  
  - **Insertion Sort** O(n<sup>2</sup>) (stable) : <br>
  We initially start with sorted part with only 1 element i.e. `arr[0]` and start traversing   from `i=1` and every time pick `arr[i]` take it to is its right       position in the sorted part of array by shifting elements.
  
- Char arrays are terminated with `'\0'` called the `null charachter`.
- To input a sentence in c++ we use `cin.getline(str,len);`.
- Spiral printing a 2d array
  - **Approach:** We print startingRow, endingColumn, endingRow, startingColumn in order and keep on increaing or decreading them after printing.
  - **Code:** 
  ```c++
  vector<int> spiralOrder(vector<vector<int>>& matrix) {
        
        vector<int> ans;
        int totalSize=(matrix[0].size())*(matrix.size());
        cout<<totalSize<<endl;
        
        int sr=0,ec=matrix[0].size()-1,er=matrix.size()-1,sc=0;
        
        while( (ans.size()<totalSize) ){
            for(int i=sc;ans.size()<totalSize && i<=ec;i++){
                ans.push_back(matrix[sr][i]);
            }
            sr++;
            
            for(int i=sr;ans.size()<totalSize && i<=er;i++){
                ans.push_back(matrix[i][ec]);
                
            }
            ec--;
            
            for(int i=ec;ans.size()<totalSize && i>=sc;i--){
                ans.push_back(matrix[er][i]);
                
            }
            er--;
            
            for(int i=er;ans.size()<totalSize && i>=sr;i--){
                ans.push_back(matrix[i][sc]);
                
            }
            sc++;
        }
        
        return ans;
        
    }
  ```
