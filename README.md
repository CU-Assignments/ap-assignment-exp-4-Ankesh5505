# experiment-no.-4-22BCS_IOT-701B
# Longest Nice Substring & Maximum Subarray Solutions

## 1. Longest Nice Substring

### Problem Statement

A string s is called *nice* if, for every letter in the alphabet that appears in s, both its uppercase and lowercase versions also appear.

Given a string s, return the longest nice substring of s. If there are multiple longest nice substrings, return the earliest occurrence. If none exist, return an empty string.

### Example Inputs & Outputs

java
Input: s = "YazaAay"
Output: "aAa"

Input: s = "Bb"
Output: "Bb"

Input: s = "c"
Output: ""


### Approach

- Use a *set* to store all characters in the string.
- Iterate through the string to find characters that do *not* have both uppercase and lowercase versions.
- Recursively split the string at those points and check both parts.
- Return the longest valid substring found.

### Java Implementation

java
class Solution {
    public String longestNiceSubstring(String s) {
        if (s.length() < 2) return "";

        Set<Character> set = new HashSet<>();
        for (char c : s.toCharArray()) {
            set.add(c);
        }

        for (int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            if (set.contains(Character.toUpperCase(c)) && set.contains(Character.toLowerCase(c))) {
                continue;
            }

            String left = longestNiceSubstring(s.substring(0, i));
            String right = longestNiceSubstring(s.substring(i + 1));
            return left.length() >= right.length() ? left : right;
        }
        return s;
    }
}


---

## 2. Maximum Subarray (Kadane’s Algorithm)

### Problem Statement

Given an integer array nums, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.

### Example Inputs & Outputs

java
Input: nums = [-2,1,-3,4,-1,2,1,-5,4]
Output: 6  // (Subarray: [4,-1,2,1])

Input: nums = [1]
Output: 1

Input: nums = [5,4,-1,7,8]
Output: 23  // (Subarray: [5,4,-1,7,8])


### Approach

- Use *Kadane’s Algorithm*, which keeps track of:
  - The *current subarray sum* (currentSum).
  - The *maximum sum found so far* (maxSum).
- Iterate through the array and update currentSum by either:
  - Adding the current number to the existing subarray.
  - Starting a new subarray if the current number is greater than currentSum + nums[i].
- Update maxSum whenever currentSum becomes larger.

### Java Implementation

java
class Solution {
    public int maxSubArray(int[] nums) {
        int maxSum = nums[0];
        int currentSum = nums[0];
        
        for (int i = 1; i < nums.length; i++) {
            currentSum = Math.max(nums[i], currentSum + nums[i]);
            maxSum = Math.max(maxSum, currentSum);
        }
        return maxSum;
    }
}


---

## Complexity Analysis

| Algorithm                                 | Time Complexity      | Space Complexity         |
| ----------------------------------------- | -------------------- | ------------------------ |
| *Longest Nice Substring*                | O(n²) (Worst case) | O(n) (Recursion depth) |
| *Maximum Subarray (Kadane’s Algorithm)* | O(n)               | O(1)                   |

---

## How to Run

1. Copy and paste the Java code into a .java file.
2. Compile and run using:
   sh
   javac Solution.java
   java Solution
   
3. Modify test cases in the main method as needed.

---

## Notes

- The *Longest Nice Substring* solution is recursive and can be optimized further.
- *Kadane’s Algorithm* is an efficient approach for solving the *Maximum Subarray* problem in linear time.

---

## Submitted by:

Ankesh Kumar


UID-22BET10135
