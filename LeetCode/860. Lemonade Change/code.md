```java
class Solution {
    private int[] left;
    public boolean lemonadeChange(int[] bills) {
        left = new int[]{0, 0};
        for (int bill: bills) {
            int change = (bill - 5) / 5;
            if (!checkChange(change))
                return false;
            if (change < 2)
                left[change]++;
        }
        return true;
    }

    private boolean checkChange(int change) {
        if (change == 0)
            return true;
        else if (change == 1 && left[0] > 0) {
            left[0]--;
            return true;
        }
        else if (change == 2) {
            if (left[1] > 0) {
                left[1]--;
                return true;
            }
            else if (left[0] > 1) {
                left[0] -= 2;
                return true;
            }
        }
        else if (change == 3) {
            if (left[0] > 0 && left[1] > 0) {
                left[0]--;
                left[1]--;
                return true;
            }

            else if (left[0] > 2) {
                left[0] -= 3;
                return true;
            }
        }
        return false;
    }
}
```