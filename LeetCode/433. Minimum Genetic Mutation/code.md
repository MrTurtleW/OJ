# 2020-04-29

```python
class Solution:
    def minMutation(self, start: str, end: str, bank: List[str]) -> int:
        level = 0

        queue = [start]
        visited = set()

        gene = ['A', 'C', 'G', 'T']

        while queue:
            size = len(queue)

            for i in range(size):
                gene_list = list(queue[0])
                for index in range(len(gene_list)):
                    for g in gene:
                        if g != gene_list[index]:
                            gene_list[index] = g
                            str_gene_list = ''.join(gene_list)
                            if str_gene_list not in visited and str_gene_list in bank:
                                queue.append(str_gene_list)
                                visited.add(str_gene_list)

                                if str_gene_list == end:
                                    return level + 1

                            gene_list[index] = queue[0][index]

                del queue[0]

            level += 1

        return -1
```