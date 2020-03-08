# 自己写的

```java
class Solution {
    public int[] plusOne(int[] digits) {
        int index = digits.length - 1;
        boolean cap = true;

        while (index >=0 && cap) {
            digits[index] += 1;
            if (digits[index] >= 10) {
                digits[index--] -= 10;
            }
            else{
                cap = false;
            }
        }
        if (cap) {
            int result[] = new int[digits.length + 1];
            result[0] = 1;
            index = 1;
            for (int digit: digits) {
                result[index++] = digit;
            }
            return result;
        }
        else{
            return digits;
        }
    }
}
```

# 题解

```java
public int[] plusOne(int[] digits) {
        
    int n = digits.length;
    for(int i=n-1; i>=0; i--) {
        if(digits[i] < 9) {
            digits[i]++;
            return digits;
        }
        
        digits[i] = 0;
    }
    
    int[] newNumber = new int [n+1];
    newNumber[0] = 1;
    
    return newNumber;
}
```