# C

```c
/**
 * C solution in O(n) time, using open addressing hash table.
 */
#define SIZE 50000

int hash(int key) {
    int r = key % SIZE;
    return r < 0 ? r + SIZE : r;
}

void insert(int *keys, int *values, int key, int value) {
    int index = hash(key);
    while (values[index]) {
        index = (index + 1) % SIZE;
    }
    keys[index] = key;
    values[index] = value;
}

int search(int *keys, int *values, int key) {
    int index = hash(key);
    while (values[index]) {
        if (keys[index] == key) {
            return values[index];
        }
        index = (index + 1) % SIZE;
    }
    return 0;
}

int* twoSum(int* nums, int numsSize, int target) {
    int keys[SIZE];
    int values[SIZE] = {0};
    for (int i = 0; i < numsSize; i++) {
        int complements = target - nums[i];
        int value = search(keys, values, complements);
        if (value) {
            int *indices = (int *) malloc(sizeof(int) * 2);
            indices[0] = value - 1;
            indices[1] = i;
            return indices;
        }
        insert(keys, values, nums[i], i + 1);
    }
    return NULL;
} 
```

# C++

```c++
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        std::map<int,int> nums_map;
        std::vector<int> result;
        for (int i = 0; i < nums.size(); i++){
            nums_map[nums[i]] = i;
        }
        for (int i = 0; i < nums.size(); i++){
            int value = target - nums[i];
            if (nums_map.find(value) != nums_map.end() && nums_map[value] != i) {
                result.push_back(i);
                result.push_back(nums_map[value]);
                return result;
            }
        }
    }
};
```

# Javascript

```javascript
const twoSum = function(nums, target) {
    const comp = {};
    for(let i=0; i<nums.length; i++){
        if(comp[nums[i] ]>=0){
            return [ comp[nums[i] ] , i]
        }
        comp[target-nums[i]] = i
    }
};
```

# Python

```python
class Solution(object):
    def twoSum(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[int]
        """
        for i in range(len(nums)):
            for j in range(1, len(nums)-i):
                if nums[i] + nums[i+j] == target:
                    return [i, i+j]
```
超时

```python
class Solution:
    def twoSum(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[int]
        """
        _dict = {}
        for i in range(len(nums)):
            x = nums[i]
            if target - x in _dict:
                return [_dict[target-x], i]
            _dict[x] = i
```