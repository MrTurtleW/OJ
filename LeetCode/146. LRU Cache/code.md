# 自己写的

```python
class LRUCache:

    class Node:
        def __init__(self, key, value):
            self.key = key
            self.value = value
            self.next = None
            self.prev = None

        def __str__(self):
            return '{{{}: {}}}'.format(self.key, self.value)

    def __init__(self, capacity: int):
        assert capacity > 0, "capacity must be greater than 0"
        self.capacity = capacity
        self.head = None

    @property
    def tail(self):
        node = self.head
        if node is None:
            return None
        while node.next != None:
            node = node.next

        return node

    @property
    def length(self):
        length = 0
        if self.head is None:
            return length

        node = self.head
        while node:
            node = node.next
            length += 1
    
        return length

    def get(self, key: int) -> int:
        node = self.head
        while node != None and node.key != key:
            node = node.next

        if node is None:
            return -1

        if self.head is node:
            return node.value

        if node.prev:
            node.prev.next = node.next
        if node.next:
            node.next.prev = node.prev

        self.head.prev = node
        node.next = self.head
        node.prev = None
        self.head = node

        return node.value

    def put(self, key: int, value: int) -> None:
        node = LRUCache.Node(key, value)
        if self.head is None:
            self.head = node
        else:
            self.head.prev = node
            node.next = self.head
            self.head = node
            node = self.head.next

            while node:
                if node.key == key:
                    if node.prev:
                        node.prev.next = node.next
                    if node.next:
                        node.next.prev = node.prev

                node = node.next

            while self.length > self.capacity:
                self.tail.prev.next = None

    def print(self):
        node = self.head
        print('cache', end=' ')
        while node != None:
            print(node, end=', ')
            node = node.next

        print()

if __name__ == '__main__':
    op = ["LRUCache","get","put","get","put","put","get","get"]

    param = [[2],[2],[2,6],[1],[1,5],[1,2],[1],[2]]

    cache = LRUCache(param[0][0])
    for o, p in zip(op[1:], param[1:]):
        print(getattr(cache, o)(*p))
```