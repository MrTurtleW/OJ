```c++
#include<iostream>
#include<vector>

using namespace std;

class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
        if (nums.size() < 2) {
            return nums.size();
        }
        int current = 0;
        for (int i = 1; i < nums.size(); i++) {
            if (nums[i] != nums[current]) {
                nums[++current] = nums[i];
            }
        }
        return current+1;
    }
};

int main() {
    Solution solution;

    vector<int> nums{0,0,1,1,1,2,2,3,3,4};

    int result = solution.removeDuplicates(nums);
    for (int i=0; i<result; i++) {
        cout << nums[i] << endl;
    }
}
```

