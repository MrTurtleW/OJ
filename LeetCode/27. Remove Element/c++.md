```c++
#include<iostream>
#include<vector>

using namespace std;

class Solution {
public:
    int removeElement(vector<int>& nums, int val) {
        int current = 0;
        for (int i=0; i<nums.size(); i++){
            if (nums[i] != val) {
                nums[current++] = nums[i];
            }
        }
        return current;
    }
};

int main() {
    Solution solution;

    vector<int> nums{};

    int result = solution.removeElement(nums, 3);
    for (int i=0;i<result;i++) {
        cout << nums[i] << endl;
    }

}
```

