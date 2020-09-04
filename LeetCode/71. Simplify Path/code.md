```java
class Solution {
    public String simplifyPath(String path) {
        LinkedList<String> vector = new LinkedList<>();
        String[] pathSplit = path.split("/");
        for (String s: pathSplit) {
            if (s.equals(".") || s.equals("")) {
            }
            else if (s.equals("..")) {
                if (vector.size() != 0)
                    vector.remove(vector.size()-1);
            }
            else {
                vector.add(s);
            }
        }
        return "/" + String.join("/", vector);
    }
}
```

