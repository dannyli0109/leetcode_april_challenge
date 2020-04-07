## Day6

### [Group Anagrams](https://leetcode.com/explore/challenge/card/30-day-leetcoding-challenge/528/week-1/3288/)

---

Given an array of strings, group anagrams together.

**Example:**

```
Input: ["eat", "tea", "tan", "ate", "nat", "bat"],
Output:
[
  ["ate","eat","tea"],
  ["nat","tan"],
  ["bat"]
]
```

**Note:**
- All inputs will be in lowercase.
- The order of your output does not matter.

---

- sort by alphabetical order
- store sorted string in the map with the index in the output array and if new anagrams are found, add them to the output array

```cs
public class Solution {
    string SortString(string input)
    {
        char[] characters = input.ToArray();
        Array.Sort(characters);
        return new string(characters);
    }
    
    public IList<IList<string>> GroupAnagrams(string[] strs) {
        int index = 0;
        var map = new Dictionary<string, int>();
        IList<IList<string>> output = new List<IList<string>>();
        
        for(int i = 0; i < strs.Length; i++) {
            string s = SortString(strs[i]);
            if (!map.ContainsKey(s)) {
                map.Add(s, index);
                output.Add(new List<string>());
                index++;
            }
            int arrIndex = map[s];
            output[arrIndex].Add(strs[i]);
        }
        return output;
    }
}
```