## Day24

### [LRU Cache][(https://leetcode.com/explore/challenge/card/30-day-leetcoding-challenge/531/week-4/3308/](https://leetcode.com/explore/challenge/card/30-day-leetcoding-challenge/531/week-4/3309/))

---

Design and implement a data structure for Least Recently Used (LRU) cache. It should support the following operations: `get` and `put`.

`get(key)` - Get the value (will always be positive) of the key if the key exists in the cache, otherwise return -1.
`put(key, value)` - Set or insert the value if the key is not already present. When the cache reached its capacity, it should invalidate the least recently used item before inserting a new item.

The cache is initialized with a **positive** capacity.

**Follow up:**

Could you do both operations in **O(1)** time complexity?

**Example:**
```
LRUCache cache = new LRUCache( 2 /* capacity */ );

cache.put(1, 1);
cache.put(2, 2);
cache.get(1);       // returns 1
cache.put(3, 3);    // evicts key 2
cache.get(2);       // returns -1 (not found)
cache.put(4, 4);    // evicts key 1
cache.get(1);       // returns -1 (not found)
cache.get(3);       // returns 3
cache.get(4);       // returns 4
```

---

- use a list to sort the most resent keys
- if a key is used, remove the key and add that to the back
- when the capacity is reached, remove the first item in the list

```cs
public class LRUCache {
    int capacity;
    Dictionary<int, int> map;
    List<int> list;
    int count;
    
    public LRUCache(int capacity) {
        this.capacity = capacity;
        map = new Dictionary<int, int>();
        list = new List<int>();
        count = 0;
    }
    
    public int Get(int key) {
        if (map.ContainsKey(key)) {
            list.Remove(key);
            list.Add(key);
            return map[key];
        }
        return -1;
    }
    
    public void Put(int key, int value) {
        if (map.ContainsKey(key)) {
            map[key] = value;
            list.Remove(key);
        }
        else {
            if (count >= capacity) {
                int keyToRemove = list[0];
                map.Remove(keyToRemove);
                list.Remove(keyToRemove);
                map.Add(key, value);
            }
            else {
                map.Add(key, value);
                count++;
            }
        }
        list.Add(key);
    }
}

/**
 * Your LRUCache object will be instantiated and called as such:
 * LRUCache obj = new LRUCache(capacity);
 * int param_1 = obj.Get(key);
 * obj.Put(key,value);
 */
 ```