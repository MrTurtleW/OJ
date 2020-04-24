
```java
public List<String> findWords(char[][] board, String[] words) {
    List<String> res = new ArrayList<>();
    TrieNode root = buildTrie(words);
    for (int i = 0; i < board.length; i++) {
        for (int j = 0; j < board[0].length; j++) {
            dfs (board, i, j, root, res);
        }
    }
    return res;
}

public void dfs(char[][] board, int i, int j, TrieNode p, List<String> res) {
    char c = board[i][j];
    if (c == '#' || p.next[c - 'a'] == null) return;
    p = p.next[c - 'a'];
    if (p.word != null) {   // found one
        res.add(p.word);
        p.word = null;     // de-duplicate
    }

    board[i][j] = '#';
    if (i > 0) dfs(board, i - 1, j ,p, res); 
    if (j > 0) dfs(board, i, j - 1, p, res);
    if (i < board.length - 1) dfs(board, i + 1, j, p, res); 
    if (j < board[0].length - 1) dfs(board, i, j + 1, p, res); 
    board[i][j] = c;
}

public TrieNode buildTrie(String[] words) {
    TrieNode root = new TrieNode();
    for (String w : words) {
        TrieNode p = root;
        for (char c : w.toCharArray()) {
            int i = c - 'a';
            if (p.next[i] == null) p.next[i] = new TrieNode();
            p = p.next[i];
       }
       p.word = w;
    }
    return root;
}

class TrieNode {
    TrieNode[] next = new TrieNode[26];
    String word;
}
```


```python
import string
from typing import List

mapping = {ch: ord(ch) - 97 for ch in string.ascii_lowercase}


class TrieNode:
    def __init__(self, data):
        self.children = [None for i in range(26)]
        self.word = None
        self.data = data


def buildTrie(words):
    root = TrieNode(None)

    for word in words:
        current = root
        for ch in word:
            if current.children[mapping[ch]] is None:
                current.children[mapping[ch]] = TrieNode(ch)
            current = current.children[mapping[ch]]

        current.word = word

    return root


class Solution:
    def __init__(self):
        self.res = []
        self.board = None
        self.trie_root = None

    def findWords(self, board: List[List[str]], words: List[str]) -> List[str]:
        self.board = board
        self.trie_root = buildTrie(words)
        for i in range(len(board)):
            for j in range(len(board[0])):
                self.dfs(self.trie_root, i, j)

        return self.res

    def dfs(self, node, i, j):
        c = self.board[i][j]
        if c == '#' or node.children[mapping[c]] is None:
            return

        node = node.children[mapping[c]]
        if node.word:
            self.res.append(node.word)
            node.word = None

        self.board[i][j] = '#'
        if i > 0:
            self.dfs(node, i-1, j)
        if i < len(self.board) - 1:
            self.dfs(node, i+1, j)

        if j > 0:
            self.dfs(node, i, j-1)
        if j < len(self.board[0]) - 1:
            self.dfs(node, i, j+1)

        self.board[i][j] = c


if __name__ == '__main__':
    board = [
        ['o', 'a', 'a', 'n'],
        ['e', 't', 'a', 'e'],
        ['i', 'h', 'k', 'r'],
        ['i', 'f', 'l', 'v']
    ]
    words = ["oath", "pea", "eat", "rain"]
    solution = Solution()
    print(solution.findWords(board, words))
```