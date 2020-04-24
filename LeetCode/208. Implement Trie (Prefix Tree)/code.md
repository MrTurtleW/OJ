```java
class Trie {
    Node root;

    /** Initialize your data structure here. */
    public Trie() {
        root = new Node();
    }

    /** Inserts a word into the trie. */
    public void insert(String word) {
        Node current = root;
        for (int i = 0; i < word.length(); i++) {
            if (current.data[word.charAt(i) - 'a'] == null) {
                current.data[word.charAt(i) - 'a'] = new Node();
            }
            current = current.data[word.charAt(i) - 'a'];
        }
        current.isEnd = true;
    }

    /** Returns if the word is in the trie. */
    public boolean search(String word) {
        Node current = root;
        for (int i=0; i < word.length(); i++) {
            if (current.data[word.charAt(i) - 'a'] == null)
                return false;
            current = current.data[word.charAt(i) - 'a'];
        }
        return current.isEnd;
    }

    /** Returns if there is any word in the trie that starts with the given prefix. */
    public boolean startsWith(String prefix) {
        Node current = root;
        for (int i=0; i < prefix.length(); i++) {
            if (current.data[prefix.charAt(i) - 'a'] == null)
                return false;
            current = current.data[prefix.charAt(i) - 'a'];
        }
        return true;
    }

    class Node {
        Node[] data;
        boolean isEnd = false;

        Node() {
            data = new Node[26];
        }
    }
}
```