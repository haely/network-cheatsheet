# DSA Cheatsheet

## Data Structures

### Arrays
```python
# Initialize an array in Python
arr = [1, 2, 3, 4, 5]

# Common operations
arr.append(6)  # O(1) - Add element at end
arr.pop()      # O(1) - Remove last element
arr.insert(2, 99)  # O(n) - Insert at index 2
```

### Linked Lists
```python
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

# Insert at head
head = ListNode(1)
head.next = ListNode(2)
```

### Stacks (LIFO)
```python
stack = []
stack.append(1)  # Push
stack.append(2)
stack.pop()      # Pop
```

### Queues (FIFO)
```python
from collections import deque
queue = deque()
queue.append(1)  # Enqueue
queue.append(2)
queue.popleft()  # Dequeue
```

### Hash Tables (Dictionaries)
```python
hash_map = {}
hash_map['key1'] = 10  # Insert
print(hash_map.get('key1'))  # O(1) Lookup
```

### Binary Search Tree (BST)
```python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

def insert(root, val):
    if not root:
        return TreeNode(val)
    if val < root.val:
        root.left = insert(root.left, val)
    else:
        root.right = insert(root.right, val)
    return root
```

### Heaps (Priority Queues)
```python
import heapq
min_heap = []
heapq.heappush(min_heap, 5)  # Insert
heapq.heappush(min_heap, 1)
heapq.heappop(min_heap)  # Extract min
```

### Graphs (Adjacency List Representation)
```python
graph = {
    'A': ['B', 'C'],
    'B': ['A', 'D', 'E'],
    'C': ['A', 'F'],
    'D': ['B'],
    'E': ['B', 'F'],
    'F': ['C', 'E']
}
```

## Algorithms

### Binary Search
```python
def binary_search(arr, target):
    left, right = 0, len(arr) - 1
    while left <= right:
        mid = (left + right) // 2
        if arr[mid] == target:
            return mid
        elif arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    return -1
```

### BFS (Breadth-First Search)
```python
from collections import deque
def bfs(graph, start):
    visited = set()
    queue = deque([start])
    while queue:
        node = queue.popleft()
        if node not in visited:
            print(node, end=' ')
            visited.add(node)
            queue.extend(graph[node])
```

### DFS (Depth-First Search)
```python
def dfs(graph, node, visited=set()):
    if node not in visited:
        print(node, end=' ')
        visited.add(node)
        for neighbor in graph[node]:
            dfs(graph, neighbor, visited)
```

### Dynamic Programming (Fibonacci - Memoization)
```python
def fib(n, memo={}):
    if n in memo:
        return memo[n]
    if n <= 1:
        return n
    memo[n] = fib(n-1, memo) + fib(n-2, memo)
    return memo[n]
```

### Sliding Window (Max Sum of Subarray of Size K)
```python
def max_sum_subarray(arr, k):
    max_sum, window_sum = 0, sum(arr[:k])
    for i in range(len(arr) - k):
        window_sum += arr[i + k] - arr[i]
        max_sum = max(max_sum, window_sum)
    return max_sum
```

### Topological Sort (Kahn's Algorithm)
```python
from collections import deque, defaultdict
def topological_sort(vertices, edges):
    graph = defaultdict(list)
    in_degree = {i: 0 for i in range(vertices)}
    for u, v in edges:
        graph[u].append(v)
        in_degree[v] += 1
    queue = deque([node for node in in_degree if in_degree[node] == 0])
    topo_order = []
    while queue:
        node = queue.popleft()
        topo_order.append(node)
        for neighbor in graph[node]:
            in_degree[neighbor] -= 1
            if in_degree[neighbor] == 0:
                queue.append(neighbor)
    return topo_order
```

### Dijkstra’s Algorithm
```python
import heapq
def dijkstra(graph, start):
    min_heap = [(0, start)]
    distances = {node: float('inf') for node in graph}
    distances[start] = 0
    while min_heap:
        curr_dist, node = heapq.heappop(min_heap)
        if curr_dist > distances[node]:
            continue
        for neighbor, weight in graph[node].items():
            distance = curr_dist + weight
            if distance < distances[neighbor]:
                distances[neighbor] = distance
                heapq.heappush(min_heap, (distance, neighbor))
    return distances
```

