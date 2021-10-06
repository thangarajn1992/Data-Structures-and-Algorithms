# Queue and BFS

## Queue and BFS

One common application of Breadth-first Search \(BFS\) is to find the shortest path from the root node to the target node. In this article, we provide an example to explain how queue is applied in a BFS algorithm step by step.

#### An Example <a id="an-example"></a>

Here we provide an example to show how BFS is used to find the shortest path between the root node `A` and the target node `G`.

![](../../.gitbook/assets/image%20%2855%29.png)



#### Insights

**1. What is the processing order of the nodes?**

In the first round, we process the root node. In the second round, we process the nodes next to the root node; in the third round, we process the nodes which are two steps from the root node; so on and so forth.

Similar to tree's level-order traversal, `the nodes closer to the root node will be traversed earlier`.

If a node `X` is added to the queue in the `kth` round, the length of the shortest path between the root node and `X` is exactly `k`. That is to say, **you are already in the shortest path the first time you find the target node.**

**2. What is the enqueue and dequeue order of the queue?**

We first enqueue the root node. Then in each round, we process the nodes which are already in the queue one by one and add all their neighbors to the queue. **It is worth noting that the newly-added nodes `will not` be traversed immediately but will be processed in the next round.**

The processing order of the nodes is `the exact same order` as how they were `added` to the queue, which is First-in-First-out \(FIFO\). That's why we use a queue in BFS.

## BFS Template

Previously, we have already introduced two main scenarios of using BFS: `do traversal` or `find the shortest path`. Typically, it happens in a tree or a graph. As we mentioned in the chapter description, BFS can also be used in more abstract scenarios.

> It will be important to determine the nodes and the edges before doing BFS in a specific question. Typically, the node will be an actual node or a status while the edge will be an actual edge or a possible transition.

### Template 1

```java
/**
 * Return the length of the shortest path between root and target node.
 */
int BFS(Node root, Node target) {
    Queue<Node> queue;  // store all nodes which are waiting to be processed
    int step = 0;       // number of steps neeeded from root to current node
    // initialize
    add root to queue;
    // BFS
    while (queue is not empty) {
        step = step + 1;
        // iterate the nodes which are already in the queue
        int size = queue.size();
        for (int i = 0; i < size; ++i) {
            Node cur = the first node in queue;
            return step if cur is target;
            for (Node next : the neighbors of cur) {
                add next to queue;
            }
            remove the first node from queue;
        }
    }
    return -1;          // there is no path from root to target
}
```

1. As shown in the code, in each round, the nodes in the queue are the nodes which are `waiting to be processed`.
2. After each outer `while` loop, we are `one step farther from the root node`. The variable `step` indicates the distance from the root node and the current node we are visiting.

### Template 2

Sometimes, it is important to make sure that we `never visit a node twice`. Otherwise, we might get stuck in an infinite loop, _e.g._ in graph with cycle. If so, we can add a hash set to the code above to solve this problem. Here is the pseudo-code after modification:

```java
/**
 * Return the length of the shortest path between root and target node.
 */
int BFS(Node root, Node target) {
    Queue<Node> queue;  // store all nodes which are waiting to be processed
    Set<Node> visited;  // store all the nodes that we've visited
    int step = 0;       // number of steps neeeded from root to current node
    // initialize
    add root to queue;
    add root to visited;
    // BFS
    while (queue is not empty) {
        step = step + 1;
        // iterate the nodes which are already in the queue
        int size = queue.size();
        for (int i = 0; i < size; ++i) {
            Node cur = the first node in queue;
            return step if cur is target;
            for (Node next : the neighbors of cur) {
                if (next is not in visited) {
                    add next to queue;
                    add next to visited;
                }
            }
            remove the first node from queue;
        }
    }
    return -1;          // there is no path from root to target
}
```

> There are some cases where one does not need keep the `visited` hash set:
>
> 1. You are absolutely sure there is no cycle, for example, in tree traversal;
> 2. You do want to add the node to the queue multiple times.



