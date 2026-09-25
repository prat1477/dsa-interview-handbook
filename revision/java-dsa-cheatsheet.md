# Java DSA Cheatsheet

Quick reference for **Java 17+** interview code. Prefer readability over cleverness.

## Collections

```java
List<Integer> list = new ArrayList<>();
Deque<Integer> stack = new ArrayDeque<>();
Deque<Integer> queue = new ArrayDeque<>();
```

## HashMap / HashSet (learned)

```java
Set<Integer> seen = new HashSet<>();
if (!seen.add(num)) { /* duplicate */ }

Map<Integer, Integer> indexByValue = new HashMap<>();
indexByValue.containsKey(needed);
indexByValue.put(nums[i], i); // after lookup

frequency.put(num, frequency.getOrDefault(num, 0) + 1);
```

Say **O(1) average-case** lookup/update, not guaranteed O(1).

## Heap (learned)

```java
PriorityQueue<Integer> minHeap = new PriorityQueue<>();
PriorityQueue<Integer> maxHeap = new PriorityQueue<>(Comparator.reverseOrder());

PriorityQueue<Map.Entry<Integer, Integer>> byFreq =
    new PriorityQueue<>(Comparator.comparingInt(Map.Entry::getValue));

heap.offer(entry);
if (heap.size() > k) {
    heap.poll(); // does NOT auto-cap
}
// peek = look; poll = look + remove
```

`offer`/`poll` are O(log n). Comparator only when natural order is wrong.

```java
TreeMap<Integer, String> tm = new TreeMap<>();
TreeSet<Integer> ts = new TreeSet<>();
```

## Arrays

```java
int[] a = new int[n];
Arrays.fill(a, 0);
Arrays.sort(a);
int idx = Arrays.binarySearch(a, target); // sorted only

// Copy / convert
int[] copy = Arrays.copyOf(a, a.length);
List<Integer> boxed = Arrays.stream(a).boxed().toList();
```

## Strings

```java
char[] chars = s.toCharArray();
StringBuilder sb = new StringBuilder();
sb.append(c);
String built = sb.toString();
// s.charAt(i) — O(1); substring creates new String
```

## Graph adjacency

```java
List<List<Integer>> adj = new ArrayList<>();
for (int i = 0; i < n; i++) adj.add(new ArrayList<>());
// undirected edge u-v:
adj.get(u).add(v);
adj.get(v).add(u);
```

## TreeNode (define in interview)

```java
class TreeNode {
    int val;
    TreeNode left, right;
    TreeNode(int val) { this.val = val; }
}
```

## ListNode

```java
class ListNode {
    int val;
    ListNode next;
    ListNode(int val) { this.val = val; }
}
```

## Useful idioms

```java
// Infinity for min/max init
int min = Integer.MAX_VALUE;
int max = Integer.MIN_VALUE;

// Safe sum — use long when product/sum may overflow int
long sum = 0L;

// Entry iteration
for (var e : map.entrySet()) {
    e.getKey();
    e.getValue();
}

// 2D grid directions (4-way)
int[][] dirs = {{1,0},{-1,0},{0,1},{0,-1}};
```

## Avoid in interviews unless necessary

- Streams for hot loops (readability vs debug)
- `Integer` autoboxing in tight inner loops without reason
- Concurrent collections without concurrency story

Expand this sheet as you implement problems in the handbook. Collections internals
(`hashCode`, treeification, `ConcurrentHashMap`) wait until a problem needs them.
