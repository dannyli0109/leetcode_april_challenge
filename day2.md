## Day2

### [Happy Number](https://leetcode.com/explore/other/card/30-day-leetcoding-challenge/528/week-1/3284/)

---

Write an algorithm to determine if a number is "happy".

A happy number is a number defined by the following process: Starting with any positive integer, replace the number by the sum of the squares of its digits, and repeat the process until the number equals 1 (where it will stay), or it loops endlessly in a cycle which does not include 1. Those numbers for which this process ends in 1 are happy numbers.

**Example:**

```
Input: 19
Output: true
Explanation: 
12 + 92 = 82
82 + 22 = 68
62 + 82 = 100
12 + 02 + 02 = 1
```

--- 

- Because only 1 and 7 is happy number when n is below 10

```cs
public class Solution {
    public bool IsHappy(int n) {
        if (n == 1 || n == 7) return true;
        if (n < 10) return false;
        int sum = 0;
        while(n > 0) 
        {
            sum += (n % 10) * (n % 10) ;
            n /= 10;
        }
        return IsHappy(sum);
    }
}
```

OR

- Storing all visited number into a list, keep going until we hit one number two times, we have an infinit loop

```cs
public class Solution {
    List<int> tested = new List<int>();
    public bool IsHappy(int n) {
        if (n == 1) return true;
        int sum = 0;
        while(n > 0) 
        {
            sum += (n % 10) * (n % 10) ;
            n /= 10;
        }
        if (tested.IndexOf(sum) > -1) return false;
        tested.Add(sum);
        return IsHappy(sum);
    }
}
```
