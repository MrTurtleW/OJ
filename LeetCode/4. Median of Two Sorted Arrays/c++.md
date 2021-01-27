```c++
class Solution {
public:
    double findMedianSortedArrays(vector<int>& nums1, vector<int>& nums2) {
        vector<int>* A, * B;
        if (nums1.size() > nums2.size()) {
            B = &nums1;
            A = &nums2;
        }
        else {
            A = &nums1;
            B = &nums2;
        }

        // i + j == m - i + n - j
        int i, j;

        int imin = 0, imax = A->size(), half = (A->size() + B->size() + 1) / 2;
        int max_of_left, min_of_right;

        // i = 0 ~ m, j = (m + n + 1)/2 - i
        while (imin <= imax) {
            // binary search
            // 要保证 B[j-1] <= A[i] and A[i-1] <= B[j]
            i = (imin + imax) / 2;
            j = half - i;

            // 调整i，以达到 B[j-1] <= A[i]
            // 如果增加i，则j会减小，那么B[j-1]则会减小
            // 如果减小i，则j会增大，B[j-1]会继续增大
            // 因此这里增加i
            if (i < A->size() && B->at(j - 1) > A->at(i)) {
                imin = i + 1;
            }
            
            // 调整i，以达到 A[i-1] <= B[j]
            // 如果增加i，则A[i-1]会继续增大，B[j]反而会减小
            // 如果减小i，则A[i-1]会减小，B[j]增大
            // 因此这里要减小i
            else if (i > 0 && A->at(i - 1) > B->at(j)) {
                imax = i - 1;
            }
            // 满足条件
            else {
                if (i == 0)
                    max_of_left = B->at(j - 1);
                else if (j == 0)
                    max_of_left = A->at(i - 1);
                else
                    max_of_left = max(A->at(i - 1), B->at(j - 1));

                if ((A->size() + B->size()) % 2 == 1)
                    return max_of_left;

                if (i == A->size())
                    min_of_right = B->at(j);
                else if (j == B->size())
                    min_of_right = A->at(i);
                else
                    min_of_right = min(A->at(i), B->at(j));

                return (max_of_left + min_of_right) / 2.0;
            }
        }
        return 0;
    }
};
```

