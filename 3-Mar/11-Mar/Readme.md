# Binary Search with c++ source code

reference: https://www.geeksforgeeks.org/binary-search/

## Initially, the code was not compiling using clang++ because of ``` #include <bits/stdc++.h>``` was not recognized. I created the bits directory and copised the stdcc.h source code on github  


## Source code
```
#include <bits/stdc++.h> 
using namespace std; 
  
int binarySearch(int arr[], int l, int r, int x) 
{ 
    // if r is the beginning index
    if (r >= l) { 
        int mid = l + (r - l) / 2; 
  
        if (arr[mid] == x) 
            return mid; 
 
        if (arr[mid] > x) 
            return binarySearch(arr, l, mid - 1, x); 
  
        return binarySearch(arr, mid + 1, r, x); 
    } 
  
    // We reach here when element is not 
    // present in array 
    return -1; 
} 
  
int main(void) 
{ 
    int arr[] = { 2, 3, 4, 10, 40 }; 
    int x = 10; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    int result = binarySearch(arr, 0, n - 1, x); 
    (result == -1) ? cout << "Element is not present in array"
                   : cout << "Element is present at index " << result; 
    return 0; 
} 
```
### Takeaway: l is the first index while r is the last index. ``` int n = sizeof(arr) / sizeof(arr[0]);``` computed total bytes of the array divided the bytes of one element.
### Boh recursions would adjust based on if the target value is greater or less than the target.


