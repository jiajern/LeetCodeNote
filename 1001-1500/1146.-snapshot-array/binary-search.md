# Binary Search

```java
/*
[
 [0,2]
 [0,3,1,6]
 [0,1]
]
*/
class SnapshotArray {
    class SnapShotElement {
        public int val;
        public int snapId;
        SnapShotElement(int val, int snapId) {
            this.val = val;
            this.snapId = snapId;
        }
        @Override
        public String toString() {
            return "id: " + this.snapId + " val: " + this.val;
        }
    }
    
    int snapCount;
    List<List<SnapShotElement>> container;
    
    public SnapshotArray(int length) {
        snapCount = 0;
        container = new ArrayList<>();
        for (int i = 0; i < length; i++) {
            List<SnapShotElement> element = new ArrayList<>();
            element.add(new SnapShotElement(0,0));
            container.add(element);
        }
    }
    
    public void set(int index, int val) {
        // if we did set element before
        int L = container.get(index).size();
        SnapShotElement lastSSElement = container.get(index).get(L-1);
        if (lastSSElement.snapId == snapCount) {
            lastSSElement.val = val;
        } else {
            container.get(index).add(new SnapShotElement(val, snapCount));
        }
    }
    
    public int snap() {
        snapCount++;
        return snapCount-1;
    }
    
    public int get(int index, int snap_id) {
        return bs(container.get(index), snap_id).val;
    }
    
    private SnapShotElement bs(List<SnapShotElement> list, int snapId) {
        int left = 0, right = list.size();
        while (left < right) {
            int mid = left + ((right - left) / 2);
            if (list.get(mid).snapId == snapId) return list.get(mid);
            else if (list.get(mid).snapId > snapId) right = mid;
            else left = mid+1;
        }
        if (left >= list.size()) return list.get(left-1);
        return list.get(left).snapId > snapId ? list.get(left-1) : list.get(left);
    }
}

/**
 * Your SnapshotArray object will be instantiated and called as such:
 * SnapshotArray obj = new SnapshotArray(length);
 * obj.set(index,val);
 * int param_2 = obj.snap();
 * int param_3 = obj.get(index,snap_id);
 */
```
