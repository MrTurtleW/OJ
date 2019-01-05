`https://leetcode.com/problems/median-of-two-sorted-arrays/discuss/2471/Very-concise-O(log(min(MN)))-iterative-solution-with-detailed-explanation`

First, let's see the concept of "MEDIAN" in a slightly unconventional way. That is:
    
**If we cut the sorted array to two halves of EQUAL LENGTHS, then median is the AVERAGe OF Max(lower_half) and Min(upper_half).**

For Example, for `[2,3,5,7]`, we make the cut between 3 and 5:

```
[2 3 / 5 7]
```

Then the median is `(3+5)/2`. 

For `[2,3,4,5,6]`, we make the cut right through 4 like this:

```
[2 3 (4/4) 5 7]
```

Since we split 4 into two halves, we say now both the lower and upper subarray contain 4. This notion also leads to the correct answer: (4+4)/2=4

For convenience, let's use L to represent the number immediately left to the cut, and R the right counterpart. In [2,3,5,7], for instance, we have L=3 and R=5, respectively


We observe the index of L and R have the following relationship with the length of the array N:

```
N        Index of L / R
1               0 / 0
2               0 / 1
3               1 / 1  
4               1 / 2      
5               2 / 2
6               2 / 3
7               3 / 3
8               3 / 4
```

It is not hard to conclude that index of L=(N-1)/2. Thus, the median can be represented as

```
(L + R)/2 = (A[(N-1)/2] + A[N/2])/2
```

To get ready for the two array situation, let's add a few imaginary 'positions' in between numbers, and treat numbers as 'positions' as well

```
[6 9 13 18]  ->   [# 6 # 9 # 13 # 18 #]    (N = 4)
position index     0 1 2 3 4 5  6 7  8     (N_Position = 9)
		  
[6 9 11 13 18]->   [# 6 # 9 # 11 # 13 # 18 #]   (N = 5)
position index      0 1 2 3 4 5  6 7  8 9 10    (N_Position = 11)
```

As you can see, there are always exactly 2*N+1 positions regardless of length N. Therefore, the middle cut should always be made on the Nth position. Since index(L)=(N-1)/2 and index(R)=N/2. In this situation, we can infer that **index(L) = (cutPosition-1)/2. index(R)=(cutPosition)/2**

Now for the two-array case:

```
A1: [# 1 # 2 # 3 # 4 # 5 #]    (N1 = 5, N1_positions = 11)

A2: [# 1 # 1 # 1 # 1 #]     (N2 = 4, N2_positions = 9)
```

Similar to the one-array problem, we need to find a cut that divides the two arrays each into two halves such that **any number in the two left halves <= any number in the two right halves**

We can also make the following observations:

1. There are 2N1+2N2+2 position altogether. Therefore, there must be exactly N1+N2 positions on each side of the cut, and 2 positions directly on the cut.

2. Therefore, when we cut at position C2=K in A2, then the cut position in A1 must be C1=N1+N2-k
3. When the cuts are made, we'd have two L's and two R's. They are

```
L1 = A1[(C1-1)/2]; R1 = A1[C1/2];
L2 = A2[(C2-1)/2]; R2 = A2[C2/2];
```
Now how do we decide if this cut is the cut we want? Because L1, L2 are the greatest numbers on the left halves and R1, R2 are the smallest numbers on the right, we only need

```
L1 <= R1 && L1 <= R2 && L2 <= R1 && L2 <= R2
```


To make sure that any number in lower halves <= any number in upper halves. As a matter of fact, since L1<=R1 and L2<=R2 are naturally guaranteed because A1 and A2 are sorted. We only need to make sure:

```
L1 <= R2 and L2 <= R1
```

Now we can use simple binary search to find out the result

Two side notes:

1. Since C1 and C2 can be mutually determined from each other, we can just move one of them first, then calculate the other accordingly.
2. The only edge case is when a cut falls on the 0th(first) or the 2Nth(last) position. To solve this problem, we can imagine that both A1 and A2 actually have two extra elements, INT_MIN at A[-1] and INT_MAX at A[N].

```c++
 double findMedianSortedArrays(vector<int>& nums1, vector<int>& nums2) {
    int N1 = nums1.size();
    int N2 = nums2.size();
    if (N1 < N2) return findMedianSortedArrays(nums2, nums1);	// Make sure A2 is the shorter one.
    
    int lo = 0, hi = N2 * 2;
    while (lo <= hi) {
        int mid2 = (lo + hi) / 2;   // Try Cut 2 
        int mid1 = N1 + N2 - mid2;  // Calculate Cut 1 accordingly
        
        double L1 = (mid1 == 0) ? INT_MIN : nums1[(mid1-1)/2];	// Get L1, R1, L2, R2 respectively
        double L2 = (mid2 == 0) ? INT_MIN : nums2[(mid2-1)/2];
        double R1 = (mid1 == N1 * 2) ? INT_MAX : nums1[(mid1)/2];
        double R2 = (mid2 == N2 * 2) ? INT_MAX : nums2[(mid2)/2];
        
        if (L1 > R2) lo = mid2 + 1;		// A1's lower half is too big; need to move C1 left (C2 right)
        else if (L2 > R1) hi = mid2 - 1;	// A2's lower half too big; need to move C2 left.
        else return (max(L1,L2) + min(R1, R2)) / 2;	// Otherwise, that's the right cut.
    }
    return -1;
} 
```