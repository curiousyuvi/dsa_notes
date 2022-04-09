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
  
  vector<int> searchRange(vector<int>& nums, int target) {
        int n=nums.size();
        int l=0,r=n-1,mid,best=-1;
        
        while(l<=r)
        {
            mid=l+(r-l)/2;
            
            if(nums[mid]>target)
            {
                r=mid-1;
            
            }
            else if(nums[mid]<target)
                l=mid+1;
            else
            {
                best=mid;
                r=mid-1;
            }
            
        }
        
        int ans1=best;
        
        l=best+1;
        r=n-1;
        best= -1;
        
        while(l<=r)
        {
            mid=l+(r-l)/2;
            
            if(nums[mid]>target)
            {
                r=mid-1;
            
            }
            else if(nums[mid]<target)
                l=mid+1;
            else
            {
                best=mid;
                l=mid+1;
            }
            
        }
        
        int ans2= best;
        
        if(ans2==-1)
            ans2=ans1;
        
        vector<int> ans={ans1,ans2};
        
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
  
  - **Insertion Sort** O(n<sup>2</sup>) (stable) : [**CODE**](https://gist.github.com/curiousyuvi/0c4b281dacbdf3317debbc0a92c99f65) <br>
  We initially start with sorted part with only 1 element i.e. `arr[0]` and start traversing   from `i=1` and every time pick `arr[i]` take it to is its right       position in the sorted part of array by shifting elements.
  
 - **Merge Sort** O(n<sup>2</sup>) (stable) : [**CODE**](https://gist.github.com/curiousyuvi/15b0126112071bdc7b4f53ffe2de1bb8) <br>
 Recursively merge two sorted arrays.
  
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
- **Binary search in 2d array (m x n) :** <br>
  **Appraoch :** Consider it a 1d array with `startIdx=0` and `endIndex=(m x n) - 1` and we calculate mid every time and do basic binary search but to get the element we write `arr[mid/n][mid%n]`.
  
- **Sieve of Eratosthenes** (For finding all prime numbers in 1..n) T.C. => `O(n*log(log(n)))` : <br>
  ```c++
   int n;
   vector<bool> is_prime(n+1, true);
   is_prime[0] = is_prime[1] = false;
   for (int i = 2; i * i <= n; i++) {
      if (is_prime[i]) {
        for (int j = i * i; j <= n; j += i)
            is_prime[j] = false;
      }
    }
  ```
  
- **Segmented Sieve** (for finding primes in L..R where `1<=R<=10e12` and `(R-L)<=10e6`) T.C. => `O((R-L+1)log(R) + sqrt(R))` - <br>
  ```c++
  void sieve(char arr[], ll n)
  {
    for (ll i = 0; i <= n; i++)
        arr[i] = true;
    arr[0] = false;
    arr[1] = false;

    for (ll i = 2; i * i <= n; i++)
    {
        if (arr[i])
        {
            for (ll j = i * i; j <= n; j += i)
            {
                arr[j] = false;
            }
        }
    }
  }

  void segmentedSieve(char arr[], ll l, ll r)
  {
    ll rsqrt = sqrt(r);

    char sieveArr[rsqrt + 1];
    sieve(sieveArr, rsqrt);

    for (ll i = 2; i <= rsqrt; i++)
    {
        if (sieveArr[i])
        {
            ll firstMultiple = (((l) / i) + 1) * i;
            if (l % i == 0)
                firstMultiple -= i;

            for (ll j = max(firstMultiple, i * i) - l; j <= (r - l); j++)
                if (!((j + l) % i))
                    arr[j] = false;
        }
    }
  }
  ```
- **Heap** - <br>
  - Max Heap using STL => `priority_queue<int> max_heap;`
  - Min Heap using STL => `priority_queue<int,vector<int>,greater<int>> min_heap;`

- **GCD - Euclidean Algorithm** T.C. => O(log(a+b)) - <br>
  ```c++
  int gcd(int a, int b)
  {
    if (a == 0)
        return b;
    return gcd(b % a, a);
  }
  ```
- **GCD and LCM -** <br>
  - `GCD(a,b) * LCM(a,b) = a * b`

- **Fast Modular Exponentiation** T.C. => O(logn)- <br>
  ```c++
  int mpow(int base, int exp, int mod)
  {
    base %= mod;
    int result = 1;
    while (exp > 0)
    {
        if (exp & 1)
            result = ((long long)result * base) % mod;
        base = ((long long)base * base) % mod;
        exp >>= 1;
    }
    return result;
  }
  ```
  
- **Catalan Numbers** - <br>
  - `[ 1 , 1 , 2 , 5 , 14 , 42, ....]`
  - `[ C0, C1, C2, C3, C4, C5, ....]`
  -  `Cn = (i=0 to i=n-1) Σ (Ci x C(i-1))`
  -  DP code to get nth Catalan Number :
  ```c++
  void solve()
  {
    int i, j, n, m;
    cin >> n;
    int arr[n + 1] = {0};
    arr[0] = 1;
    arr[1] = 1;

    for (int i = 2; i <= n; i++)
    {
        int j = 0, k = i - 1, ans = 0;
        while (j < i && k >= 0)
        {
            ans += arr[j] * arr[k];
            j++;
            k--;
        }
        arr[i] = ans;
    }

    cout<<arr[n]<<endl;
  }
  ```
