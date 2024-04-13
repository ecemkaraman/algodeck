# Array

## 5 ways to reverse an array

```python
import array as arr

a = arr.array('i', [1,2,3,4,5]) #declare the data type as int (i)

# 1.Swap the elements at the opposite indexes
l = len(a)
# going through the array only halfway!!
for i in range(l // 2):
    a[i], a[l - i - 1] = a[l - i - 1], a[i] # swap the elements

# 2. reverse() method ->fastest, suitable for long arrays
a.reverse()

# 3. reversed() method ->returns an iterator
reversed_a = reversed(a)

#4. Slicing - returns a reversed copy of the original array [::-1]
reverse_a = a[::-1]

#5. Using recursion
def reverseArray(arr):
    if len(arr) == 1:
        return arr
    #print(arr) ->You can uncomment this to know how recursion works
    return reverseArray(arr[1:]) + arr[0:1]
```

[#array](array.md)

## Array complexity: access, search, insert, delete

Access: O(1)

Search: O(n)

Insert: O(n)

Delete: O(n)

[#array](array.md) [#complexity](complexity.md)

## Binary search in a sorted array algorithm

```python
def binarySearch(nums: List[int], target: int) -> int:
    l, r = 0, len(nums)
    while l < r :
        m = (l + r) // 2;
        if nums[m] < target:
            l = m + 1;
        else: 
            r = m;
    return l;
```

### Further Reading

- [Nearly All Binary Searches and Mergesorts are Broken](https://ai.googleblog.com/2006/06/extra-extra-read-all-about-it-nearly.html) by the Google AI Blog

[#array](array.md)

## Find an element in a rotated sorted array

Solution: binary search

Check first if the array is rotated. If not, apply normal binary search

If rotated, find pivot (the only element for which the next element to it is smaller than it)

Find the sorted half (either 1 or both halves will be sorted) ->rotation pivot isn't always = mid

Then, check if the element is in 0..pivot-1 or pivot..len-1

```python
def search(self, nums: List[int], target: int) -> int:
	left, right = 0, len(nums) - 1

        while left <= right:
            mid = (left + right) // 2

            if nums[mid] == target:
                return mid

            # Check if left half is sorted
            if nums[left] <= nums[mid]:
                if nums[left] <= target < nums[mid]:
                    right = mid - 1
                else:
                    left = mid + 1
            # Otherwise, right half is sorted
            else:
                if nums[mid] < target <= nums[right]:
                    left = mid + 1
                else:
                    right = mid - 1

        return -1
}
```
Time complexity: O(log n)
Space complexity: O(1)
[#array](array.md)

## How to detect if an element is a pivot in a rotated sorted array

Only element whose previous is bigger (also the pivot is the smallest element)

[#array](array.md)

## How to find a pivot element in a rotated array

Binary search -> left, right = 0, len(a)-1
if a[mid-1] > a[mid], pivot = mid-1
else if a[mid+1] < a[mid], pivot = mid

 if a[left] > a[mid], consider left half. O/w right half

Pivot = the index where the array rotation occurred - aka highest value
eg. arr[] = {3, 4, 5, 1, 2}, pivot=5

COME BACK LATER
```python
def find_pivot(arr):
    left, right = 0, len(arr) - 1
    
    while left < right:
        mid = (left + right) // 2
        
        # If mid > first element, pivot is on the right side
        if arr[mid-1] < arr[mid]:
            left = mid 
        else:
            right = mid
    
    # When left == right, we've found the pivot.
    return left

# Example usage:
arr = [4, 5, 6, 7, 0, 1, 2]
pivot_index = find_pivot(arr)
print("Pivot index:", pivot_index)
print("Pivot element:", arr[pivot_index])
```

[#array](array.md)

## Given an array, move all the 0 to the left while maintaining the order of the other elements
   
Example: 1, 0, 2, 0, 3, 0 => 0, 0, 0, 1, 2, 3

Two pointers: Move all non zero numbers to the left. 
Both L&R start at 0. 
left = where the next non-zero element will be moved
right = index of the current element being processed

If current element is non-zero, swap left&right

```python
def moveZeroes(self, nums: List[int]) -> None:
        left = 0

        for right in range(len(nums)):
            if nums[right] != 0:
                nums[right], nums[left] = nums[left], nums[right]
                left += 1
        
        return nums
```

Time complexity: O(n)
Space complexity: O(1)

[#array](array.md)

## How to find the duplicates in an array

- Hashtable
- Sorting the array then iterating over each element and check if previous = current

[#array](array.md)

## How to manage a dynamic array

When full, create a new array of twice the size, copy items (System.arraycopy is optimized for that)

Shrink: 
- Not when one-half full (otherwise worst case is too expensive: double-shrink-double-shrink etc.)
- Solution: one-quarter full

[#array](array.md)

## How to test if the array is sorted in ascending or descending order

Test first and last element (no iteration)

[#array](array.md)

## Rotate an array by n elements (n can be negative)
   
Example: 1, 2, 3, 4, 5 with n = 3 => 3, 4, 5, 1, 2

- Reverse the initial array
- Reverse from 0 to n-1
- Reverse from n to len - 1

```python
def rotate(self, nums: List[int], k: int) -> None:
        def rev(l, r):
            while l < r:
                nums[l], nums[r] = nums[r], nums[l]
                l += 1
                r -= 1
        
        n = len(nums)
	k = ((k * -1) % n) * -1 if k < 0 else k % n; # Case when k>n or k<-n
	k = (n - (k * -1)) if k < 0 else k; # Case when k is negative
        
        rev(0, n-1)  # Reverse the entire array
        rev(0, k-1)  # Reverse the first k elements
        rev(k, n-1)  # Reverse the remaining elements
```

Time complexity: O(n)
Space complexity: O(1)

[#array](array.md)
