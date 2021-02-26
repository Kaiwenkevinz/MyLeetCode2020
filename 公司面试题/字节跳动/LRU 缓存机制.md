### 哈希表 + 双链表
一开始想用数组实现，但是发现用数组没办法使put和get达到O(1)，因为元素在数组中的增加和删除伴随着整个数组的移动。  
由此想到用链表实现增加和删除O(1)的时间，但问题来了，删除某个元素需要先找到它，如果需要遍历链表的话那又不是O(1)了。  
由此想到用哈希表存储每个key对应的node的地址，这样根据key就可以瞬间定位node。
```java
class DLinkedList {
    private Node head;
    private Node tail;

    static class Node {
        private int k;
        private int v;
        private Node prev;
        private Node next;
        Node(int k, int v) {
            this.k = k;
            this.v = v;
            this.prev = null;
            this.next = null;
        }
        public void setValue(int v) { this.v = v; }
        public int getValue() { return this.v; }
        public int getKey() { return this.k; }
    }

    DLinkedList() {
        // 伪头部
        this.head = new Node(-1, -1);
        // 伪尾部
        this.tail = new Node(-2, -2);
        this.head.next = this.tail;
        this.tail.prev = this.head;
    }

    public void addToTail(Node node) {
        node.next = this.tail;
        node.prev = this.tail.prev;
        this.tail.prev.next = node;
        this.tail.prev = node;
    }

    private void removeNode(Node node) {
        node.prev.next = node.next;
        node.next.prev = node.prev;
    }

    public void moveToTail(Node node) {
        this.removeNode(node);
        this.addToTail(node);
    }

    public Node removeHead() {
        Node node = this.head.next;
        this.removeNode(this.head.next);
        return node;
    }
}


class LRUCache {

    private Map<Integer, DLinkedList.Node> map;
    private DLinkedList dLinkedList;
    private int capacity;
    private int size;

    public LRUCache(int capacity) {
        this.capacity = capacity;
        this.map = new HashMap<>();
        this.dLinkedList = new DLinkedList();
        this.size = 0;
    }


    public int get(int key) {
        if (!map.containsKey(key)) {
            return -1;
        } else {   // 存在key，返回value，更新key到tail
            DLinkedList.Node node = map.get(key);   // 拿到node
            int value = node.getValue();
            this.dLinkedList.moveToTail(node);  // 移动key到tail
            return value;
        }
    }

    // 如果key存在，更新value，并把node移动到队尾
    // 如果key不存在，队尾加入新node
    public void put(int key, int value) {
        if (!map.containsKey(key)) {
            DLinkedList.Node node = new DLinkedList.Node(key, value);   // 准备新增的node
            if (this.size < this.capacity) {   // 还有容量，直接加
                this.dLinkedList.addToTail(node);
                size++;
            } else {  // 容量满了，先删掉一个，再加
                DLinkedList.Node removedNode = this.dLinkedList.removeHead();
                this.map.remove(removedNode.getKey());     // 删除了链表里的node，哈希表也得更新
                this.dLinkedList.addToTail(node);
            }
            this.map.put(key, node);    // 往链表里加了node，哈希表也得更新
        } else {  // key已经存在，直接更新value，并移到尾部
            DLinkedList.Node node = map.get(key);
            node.setValue(value);
            this.dLinkedList.moveToTail(node);
        }
    }
}
```

### 面试等通知法：继承LinkedHashMap
```java
class LRUCache extends LinkedHashMap<Integer, Integer> {
    private int capacity;
    public LRUCache(int capacity) {
        super(capacity, 0.75f, true);
        this.capacity = capacity;
    }
    

    public int get(int key) {
        return super.getOrDefault(key, -1);
    }
    

    public void put(int key, int value) {
        super.put(key, value);
    }

    @Override
    protected boolean removeEldestEntry(Map.Entry<Integer, Integer> eldest) {
        return super.size() > capacity;
    } 
}

/**
 * Your LRUCache object will be instantiated and called as such:
 * LRUCache obj = new LRUCache(capacity);
 * int param_1 = obj.get(key);
 * obj.put(key,value);
 */
```

