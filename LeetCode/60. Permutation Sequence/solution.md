If $n=4$, you have ${1,2,3,4}$. If you were to list out all the permutations you have

- 1 + permutations of (2, 3, 4)
- 2 + permutations of (1, 3, 4)
- 3 + permutations of (1, 2, 4)
- 4 + permutations of (1, 2, 3)

We know that the number of permutations of $n$ numbers is $n!$, so each of those permuations of 3 numbers there are 6 possible permutations. Meaning there would be a total of 24 permutations in this particular one. So if you were to look for the 14th permutations, it would be in the 3+permutations of (1, 2, 4) subset.

To programmatlically get that, you take $k=13$ (index starts from 0) and divide that by the 6 we got from the factorial. Then the problem repeats with less numbers.

```java
import java.util.ArrayList;
import java.util.List;

class Solution {
    public String getPermutation(int n, int k) {
        List<Integer> numbers = new ArrayList<>();
        int[] factorial = new int[n+1];
        StringBuilder sb = new StringBuilder();

        // create an array of factorial lookup
        // factorial[] = { 1, 1, 2, 6, 24, ..., n! }

        // create a list of numbers to get indices
        // numbers = { 1, 2, 3, 4 }
        factorial[0] = 1;
        for (int i=1; i<=n; i++) {
            factorial[i] = factorial[i-1] * i;
            numbers.add(i);
        }

        // index starts from 0
        k--;

        for (int i = 1; i <= n; i++) {
            int index = k / factorial[n-i];
            sb.append(numbers.get(index));
            numbers.remove(index);
            k -= index * factorial[n-i];
        }

        return sb.toString();
    }

    public static void main(String[] args) {
        Solution solution = new Solution();
        System.out.println(solution.getPermutation(3, 3));
    }
}
```

