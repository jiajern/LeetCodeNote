# Double LinkedList

Using map for quick access. Use double linkedList for quick remove and add

```java
class LRUCache {
    class DLinkedNode {
        int val;
        int key;
        DLinkedNode prev;
        DLinkedNode next;
    }
    DLinkedNode head, tail;
    Map<Integer, DLinkedNode> cache;
    int capacity;
    int size;

    public LRUCache(int capacity) {
        head = new DLinkedNode();
        tail = new DLinkedNode();
        head.next = tail;
        tail.prev = head;
        cache = new HashMap<>();
        this.capacity = capacity;
        this.size = 0;
    }
    
    public int get(int key) {
        if (cache.containsKey(key)) {
            DLinkedNode node = cache.get(key);
            removeNode(node);
            addHead(node);
            return node.val;
        }
        else return -1;
    }
    
    public void put(int key, int value) {
        if (cache.containsKey(key)) {
            DLinkedNode node = cache.get(key);
            node.val = value;
            removeNode(node);
            addHead(node);
        } else {
            if (size >= capacity) {
                cache.remove(tail.prev.key);
                removeNode(tail.prev);
                size--;
            }
            DLinkedNode newNode = new DLinkedNode();
            newNode.val = value;
            newNode.key = key;
            addHead(newNode);
            cache.put(key, newNode);
            size++;
        }
    }
    private void addHead(DLinkedNode node) {
        node.next = head.next;
        head.next.prev = node;
        head.next = node;
        node.prev = head;
    }
    private void removeNode(DLinkedNode node) {
        node.prev.next = node.next;
        node.next.prev = node.prev;
    }
}

/**
 * Your LRUCache object will be instantiated and called as such:
 * LRUCache obj = new LRUCache(capacity);
 * int param_1 = obj.get(key);
 * obj.put(key,value);
 */
```
