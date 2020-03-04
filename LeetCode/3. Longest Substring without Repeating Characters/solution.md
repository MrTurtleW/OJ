# Approach 1: Brute Force

Check all the substring one by one to see if it has no duplicate character.

```java
public class Solution {
    public int lengthOfLongestSubstring(String s) {
        int n = s.length();
        int ans = 0;
        for (int i = 0; i < n; i++)
            for (int j = i + 1; j <= n; j++)
                if (allUnique(s, i, j)) ans = Math.max(ans, j - i);
        return ans;
    }

    public boolean allUnique(String s, int start, int end) {
        Set<Character> set = new HashSet<>();
        for (int i = start; i < end; i++) {
            Character ch = s.charAt(i);
            if (set.contains(ch)) return false;
            set.add(ch);
        }
        return true;
    }
}
```

- Time complexity: `$O(n^3)$`

    To verify if characters within inde range `[i, j)` are all unique, we need to scan all of them, Thus, it costs `$O(j-i)$` time.

    For a given `i`, the sum of time costed by each `$j\in [i+1,n]$` is `$\displaystyle \sum_{i+1}^n O(j-i)$`

    Thus, the sum of all the time comsumption is 

    ```math
    O(\sum_{i=0}^{n-1}(\sum_{j=i+1}^n(j-i)))=O(\sum_{i=0}^{n-1}\frac{(1+n-i)(n-i)}{2})=O(n^3)
    ```

- Space complexity: `$O(min(n,m))$`. We need `$O(k)$` space for checking a substring has no duplicate characters, where `$k$` is the size of the Set. The size of the Set is upper bounded by the size of the string `$n$` and the size of the charset/alphabet `$m$`. 

# Approach 2: Sliding Window

In the naive approaches, we repeatedly check a substring to see if it has duplicate character. But it is unnecessary. If a substring `$s_{ij}$` from index `$i$` to `$j - 1$` is already checked to have no duplicate characters. We only need to check if `$s[j]$` is already in the substring `$s_{ij}$`

To check if a character is already in the substring, we can scan the substring, which leads to an `$O(n^2)$` algorithm. But we can do better.

By using HashSet as a sliding window, checking if a character in the current can be done in `$O(1)$`.

```java
public class Solution {
    public int lengthOfLongestSubstring(String s) {
        int n = s.length();
        Set<Character> set = new HashSet<>();
        int ans = 0, i = 0, j = 0;
        while (i < n && j < n) {
            // try to extend the range [i, j]
            if (!set.contains(s.charAt(j))){
                set.add(s.charAt(j++));
                ans = Math.max(ans, j - i);
            }
            else {
                set.remove(s.charAt(i++));
            }
        }
        return ans;
    }
}
```

- Time complexity: `$O(2n)=O(n)$`
- Space complexity: `$O(min(m, n))$`

# Approach 3: Sliding Window Optimized

The above solution requires at most 2n steps. In fact, it could be optimized to require only n steps. Instead of using a set to tell if a character exists or not, we could define a mapping of the characters to its index. Then we can skip the characters immediately when we found a repeated character.

The reason is that if `$s[j]$` have a duplicate in the range `$[i, j)$` with index `$j'$`, we don't need to increase ii little by little. We can skip all the elements in the range `$[i, j']$` and let ii to be `$j' + 1$` directly.

```java
public class Solution {
    public int lengthOfLongestSubstring(String s) {
        int n = s.length(), ans = 0;
        Map<Character, Integer> map = new HashMap<>(); // current index of character
        // try to extend the range [i, j]
        for (int j = 0, i = 0; j < n; j++) {
            if (map.containsKey(s.charAt(j))) {
                i = Math.max(map.get(s.charAt(j)), i);
            }
            ans = Math.max(ans, j - i + 1);
            map.put(s.charAt(j), j + 1);
        }
        return ans;
    }
}
```

The previous implements all have no assumption on the charset of the string s.

If we know that the charset is rather small, we can replace the Map with an integer array as direct access table.

Commonly used tables are:
- `int[26]` for Letters 'a' - 'z' or 'A' - 'Z'
- `int[128]` for ASCII
- `int[256]` for Extended ASCII

```java
public class Solution {
    public int lengthOfLongestSubstring(String s) {
        int n = s.length(), ans = 0;
        int[] index = new int[128]; // current index of character
        // try to extend the range [i, j]
        for (int j = 0, i = 0; j < n; j++) {
            i = Math.max(index[s.charAt(j)], i);
            ans = Math.max(ans, j - i + 1);
            index[s.charAt(j)] = j + 1;
        }
        return ans;
    }
}
```

- Time complexity: `$O(n)$`
- Space Complexity(HashMap): `$O(min(m, n))$`
- Space complexity(Table): `$O(m)$`

