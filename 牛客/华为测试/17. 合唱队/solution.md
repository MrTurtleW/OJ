题目理解：
1. 所有人都已经站好位，不能再改变位置了，只能从当中去掉人组成合唱队。


最长递增子序列：比如题中所给出的示例：186 186 150 200 160 130 197 200，先看每个人的左边可能出现最多的人。
- 首先如果第一个数186在中间，左边没有数，就自己一个人，所以是1；
- 第二个数186因为左边那个人跟他一边高，没有比他矮的了，所以也是1；
- 第三个数150，左边的人都比他高，他如果是中间的话左边也他自己一个人，所以还是1；
- 第四个数200，因为不能换位置，所以只能留186或者150，加上自己，就是2
- 最后再以197为例，左边保留150,160是左边人最多的情况，再加上自己，就是3。

所以每个人左边人最多的情况（加上自己）就是（186）1 1 1 2 2 1 3 4（200）。

```
186  186  150  200  160  130  197  200
1    1    1    2    2    1    3    4
```

同理，看一下每个人右边可能出现最多的人，这时我们从后往前看。
- 200在最右面，所以自己一个人，是1；
- 197最右面没有比他矮的，自己，是1
- 160左边一个比他矮的，所以算上自己是2
- 186右面为 160，130，加上自己，是3


所以每个人右边人做多的情况（加上自己）就是（186）3 3 2 3 2 1 1 1（200）

```
186  186  150  200  160  130  197  200
3    3    2    3    2    1    1    1
```

这两行数据相加，就可以得到自己如果是中间的那个人，可以得到的最大的合唱队人数。当然，自己加了两遍，所以得减掉一个自己。另外题目问的是最少去掉的人，所以最后的结果：

```math
总人数 - 该数所在队列人数 = 需要出队的人数
```

```java
import java.util.Scanner;

public class Solutionh {
    public static void main(String[] args) {
        Scanner in = new Scanner(System.in);
        while (in.hasNext()) {
            int num = in.nextInt();
            if(num<=2){
                System.out.println(0);
            }
            int[] members=new int[num];//存储每一个数据元素
            int[] left_queue=new int[num];//数据元素从左到右对应的最大递增子序列数
            int[] right_queue=new int[num];//数据元素从右到左对应的最大递增子序列数
            for(int i=0;i<num;i++){//初始化各个数组数据
                members[i]=in.nextInt();
                left_queue[i]=1;
                right_queue[i]=1;
            }
            for(int i=0;i<num;i++){
                for(int j=0;j<i;j++){
                    if(members[i]>members[j]&&left_queue[j]+1>left_queue[i])
                        left_queue[i]=left_queue[j]+1;
                }
            }
            for(int i=num-1;i>=0;i--){
                for(int j=num-1;j>i;j--){
                    if(members[i]>members[j]&&right_queue[j]+1>right_queue[i])
                        right_queue[i]=right_queue[j]+1;
                }
            }
            int max=0;
            for(int i=0;i<num;i++){
                if(left_queue[i]+right_queue[i]>max)
                    max=left_queue[i]+right_queue[i];
            }
            System.out.println(num-max+1);
        }
    }
}
```

使用bisect：

```python
import bisect


def calculate(_list):
    # 每次向b中加一个list中的元素
    b = [9999] * len(_list)
    b[0] = _list[0]
    res = [1]
    for i in range(1, len(_list)):
        pos = bisect.bisect_left(b, _list[i])
        res += [pos + 1]
        b[pos] = _list[i]
    return res


while True:
    try:
        n = int(input())
        s = list(map(int, input().split()))
        left = calculate(s)  # 正序遍历位置
        right = calculate(s[::-1])[::-1]  # 逆序遍历位置
        a = max(left[i] + right[i] for i in range(n))  # 两次遍历的结果相加
        print(n - a + 1)  # a中的那个人多加了一次 故要+1
    except:
        break
```