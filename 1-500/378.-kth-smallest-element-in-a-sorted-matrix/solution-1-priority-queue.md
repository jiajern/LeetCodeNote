# Solution 1 Priority Queue

### Approach

Using **PriorityQueue** to store one element from each row.

```java
class MyHeapNode {
    int row;
    int col;
    int val;
    public MyHeapNode(int row, int col, int val) {
        this.row = row;
        this.col = col;
        this.val = val;
    }
    public int getValue() {
        return this.val;
    }
    public int getRow() {
        return this.row;
    }
    public int getCol() {
        return this.col;
    }
}
class Solution {
    public int kthSmallest(int[][] matrix, int k) {
        int N = matrix.length;
        PriorityQueue<MyHeapNode> minHeap = new PriorityQueue<>(N, (a, b) -> (a.getValue() - b.getValue()));
        
        for(int r = 0; r < N; r++) {
            minHeap.offer(new MyHeapNode(r, 0, matrix[r][0]));
        }
        
        MyHeapNode element = minHeap.peek();
        
        while(k-- > 0) {
            element = minHeap.poll();
            int r = element.getRow(), c = element.getCol() + 1;
            if (c < N) minHeap.offer(new MyHeapNode(r, c, matrix[r][c]));
        }
        return element.getValue();
    }
}
```
