超时：

```python
import traceback


def get_sum_of_selected(selected):
    _sum = 0
    for good in selected:
        _sum += price[good]
    return _sum


def get_weight_sum_of_selected(selected):
    _sum = 0
    for good in selected:
        _sum += importance[good] * price[good]

    return _sum


def find_max(selected=[], index=0):
    global max_val

    if get_sum_of_selected(selected) > N:
        return

    temp = get_weight_sum_of_selected(selected)
    if max_val < temp:
        max_val = temp

    if index >= len(price):
        return

    # 如果当前物品是主件，则直接递归添加和不添加
    if affiliate[index] == 0:
        find_max(selected + [index], index + 1)
        find_max(selected, index + 1)
    # 如果是附件，则需要做一些判断
    else:
        # 如果主件没有买，或主件的附件个数大于2，不能买此附件
        if affiliate[index] - 1 not in selected or selected.count(affiliate[index] - 1) > 2:
            find_max(selected, index + 1)
        else:
            find_max(selected + [index], index + 1)
            find_max(selected, index + 1)


try:
    while True:
        N, m = input().split()
        max_val = 0
        N = int(N)
        price = []
        importance = []
        affiliate = []
        for i in range(int(m)):
            v, p, q = input().split()
            price.append(int(v))
            importance.append(int(p))
            affiliate.append(int(q))

        find_max()
        print(max_val)

except:
    traceback.print_exc()
```

换一种方式：

```python
def find_max(N, selected=[], index=0):

    # 没有商品可选
    if index == m:
        return 0

    # 当前商品为附件，如果主件没有购买，则不能购买
    if qs[index] != 0 and qs[index]-1 not in selected:
        res = find_max(N, selected, index+1)
    # 当前商品为主件，或者为附件，且主件已经购买，并且主件的附件数小于2
    else:
        # 钱不够，不能买当前物品
        if N < vs[index]:
            res = find_max(N, selected, index + 1)
        else:
            # 购买
            res_buy = find_max(N - vs[index], selected + [index], index + 1) + vs[index] * ps[index]
            # 不购买
            res_not_buy = find_max(N, selected, index + 1)
            res = max(res_buy, res_not_buy)

    return res


try:
    while True:
        N, m = input().split()
        N = int(N)
        m = int(m)
        vs = []
        ps = []
        qs = []
        for i in range(m):
            v, p, q = input().split()
            vs.append(int(v))
            ps.append(int(p))
            qs.append(int(q))

        print(find_max(N))
except:
    pass
```

不能加缓存？
- 前面选了主件，后面可以选附件的时候会有一个最大值，但是前面没有选主件，后面在利用这个缓存就会出错


动态规划：

```python
class Good:
    def __init__(self, v, vp):
        self.v = v
        self.vp = vp

try:
    while True:
        N, m = input().split()
        # 价格都是10的倍数，除以10节省内存和运行时间
        N = int(N) // 10
        m = int(m)
        goods = []
        # 因为数据的主件id是按行的，所以要缓存起来，用于查找
        caches = {}
        for i in range(m):
            v, p, q = map(int, input().split())
            v = v // 10
            good = Good(v, v*p)
            if q == 0:
                goods.append([good, None, None])
                caches[i] = len(goods)-1
            elif goods[caches[q-1]][1] is None:
                goods[caches[q-1]][1] = good
            else:
                goods[caches[q-1]][2] = good

        f = [0 for i in range(N + 1)]

        for good in goods:
            for j in range(N, -1, -1):
                master = good[0]
                if j < master.v:
                    continue

                # 先从 `选主件` 和 `不选主件` 中选加权和较大的
                _max = max(f[j], f[j-master.v] + master.vp)
                # 主件和附件1
                if good[1] and j >= master.v + good[1].v:
                    _max = max(_max, f[j-master.v-good[1].v] + master.vp + good[1].vp)

                # 主件和附件二
                if good[2] and j >= master.v + good[2].v:
                    _max = max(_max, f[j-master.v-good[2].v] + master.vp + good[2].vp)

                # 主件、附件一、附件二
                if good[2] and j >= master.v + good[1].v + good[2].v:
                    _max = max(_max, f[j-master.v-good[1].v-good[2].v] + master.vp + good[1].vp + good[2].vp)

                f[j] = _max

        print(f[N] * 10)


except:
    import traceback;traceback.print_exc()
```

java

```java
import java.util.*;

public class Solution {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        // 总钱数
        int N = scanner.nextInt() / 10;
        // 购买物品个数
        int m = scanner.nextInt();
        int[] f = new int[N + 1];
        // 分组，goods[i][0]为主件，goods[i][1]为附件1，goods[i][2]为附件2
        List<Good[]> goods = new ArrayList<>();

        Map<Integer, Integer> caches = new HashMap<>();

        for (int i = 0; i < m; i++) {
            int v = scanner.nextInt() / 10;
            int p = scanner.nextInt();
            int q = scanner.nextInt();

            Good t = new Good(v, v * p);
            if (q == 0) {
                goods.add(new Good[]{t, null, null});
                caches.put(i, goods.size()-1);
            } else if (goods.get(caches.get(q-1))[1] == null){
                goods.get(caches.get(q-1))[1] = t;
            } else {
                goods.get(caches.get(q-1))[2] = t;
            }
        }

        for (Good[] good: goods) {
            for (int j = N; j >= 0 ; j--) {
                //以下代码从分组中选择价值最大的。共五种情况：
                // - 不选主件，
                // - 选主件，
                // - 选附件1和主件，
                // - 选附件2和主件，
                // - 选附件1和附件2和主件
                // master为主件
                Good master = good[0];
                if (j < master.v)
                    continue;

                // 选主件或不选主件的较大者
                int max = Math.max(f[j], f[j - master.v] + master.vp);

                // 选主件和附件1
                if (good[1] != null && j >= master.v + good[1].v) {
                    max = Math.max(f[j - master.v -good[1].v] + master.vp + good[1].vp, max);
                }
                // 选主件和附件二
                if (good[2] != null && j >= master.v + good[2].v) {
                    max = Math.max(f[j - master.v -good[2].v] + master.vp + good[2].vp, max);
                }
                // 选主件和附件1、2，若附件二不为空，则附件一肯定不为空
                if (good[2] != null && j >= master.v + good[1].v + good[2].v) {
                    max = Math.max(f[j - master.v - good[1].v - good[2].v] + master.vp + good[1].vp + good[2].vp, max);
                }
                f[j] = max;
            }
        }

        System.out.println(f[N] * 10);
    }
}

class Good {
    int v;
    int vp;
    public Good(int v, int vp) {
        this.v = v;
        this.vp = vp;
    }
}
```