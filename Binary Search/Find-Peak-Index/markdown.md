# ⛰️ Find Peak Element – DSA Problem  

## 📝 Problem Statement  

A **peak element** is an element that is **strictly greater than its neighbors**.  

Given an integer array `nums`, return the **index of any one peak element**.  

- You may assume `nums[-1] = -∞` and `nums[n] = -∞`.  
- This means the first and last elements can also be peaks if they are greater than their only neighbor.  

⚡ Requirement: The algorithm must run in **O(log n)** time.  

---

## 📥 Input  

- `nums[]`: array of integers  

## 📤 Output  

- Index of any one peak element  

---

## 🧪 Examples  

### Example 1  
```
Input:  nums = [1,2,3,1]  
Output: 2  
Explanation: 3 is a peak element at index 2
```  

### Example 2  
```
Input:  nums = [1,2,1,3,5,6,4]  
Output: 5  
Explanation: Both nums[1] = 2 and nums[5] = 6 are peaks.  
We can return either 1 or 5.
```  

---

## 💡 Brute Force Approach – Step-by-Step Explanation  

Check each element and see if it is greater than its neighbors:  

Example:  
```
nums = [1,2,3,1]
```  

- `nums[0] = 1` → compare with `nums[1] = 2` → not a peak ❌  
- `nums[1] = 2` → compare with `1` and `3` → not a peak ❌  
- `nums[2] = 3` → compare with `2` and `1` → peak ✅ return index = 2  

### Brute Force Code Idea  
```java
for (int i = 0; i < n; i++) {
    if ((i == 0 || nums[i] > nums[i-1]) &&
        (i == n-1 || nums[i] > nums[i+1])) {
        return i;
    }
}
```

---

## ❌ Why Brute Force Fails  

- Brute force scans all `n` elements.  
- **Time Complexity = O(n)**  
- But problem demands **O(log n)**  

We need **Binary Search**! 🔥  

---

## ⚡ Optimal Approach – Binary Search  

Observation:  
- if mid is peak one **return mid**
- If `nums[mid] < nums[mid+1]`, then a peak **must exist on the right side**.  
- Otherwise, if `nums[mid] > nums[mid+1]`, then a peak **must exist on the left side**.  

This works because of the `-∞` boundary condition.  

### 🎯 Binary Search Strategy  

```java
if(nums.length==1) return 0;
int start = 0;
int end = nums.length-1;
while(start<=end){
    int mid = start + (end-start)/2;
    if((mid-1>=0?nums[mid-1]:Integer.MIN_VALUE)<nums[mid] && nums[mid]>(mid+1<nums.length?nums[mid+1]:Integer.MIN_VALUE)){
        return mid;
    }
    else if(mid+1<nums.length && nums[mid]<nums[mid+1]){
        start = mid+1;
    }
    else{
        end = mid-1;
    }
}
return -1;
```

---

## ⏱️ Time and Space Complexity  

| Approach        | Time Complexity | Space Complexity |
|----------------|-----------------|------------------|
| Brute Force     | O(n)            | O(1)             |
| Binary Search   | O(log n)        | O(1)             |

---

## ✅ Summary  

- A **peak element** is larger than its neighbors.  
- Brute force scans all elements but takes **O(n)**.  
- Using **binary search** on the slope direction, we find a peak in **O(log n)**.  
- Always works due to the `-∞` boundaries ensuring at least one peak.  
