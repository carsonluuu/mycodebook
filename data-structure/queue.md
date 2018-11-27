# Queue

### 什么是队列（Queue）？

队列（queue）是一种采用**先进先出**（FIFO，first in first out）策略的抽象数据结构。比如生活中排队，总是按照先来的先服务，后来的后服务。队列在数据结构中举足轻重，其在算法中应用广泛，**最常用的就是在宽度优先搜索\(BFS）中，记录待扩展的节点**。

队列内部存储元素的方式，一般有两种，**数组**（array）和**链表**（linked list）。两者的最主要区别是：

* 数组对**随机访问**有较好性能。
* 链表对**插入**和**删除**元素有较好性能。

在各语言的标准库中：

* Java常用的队列包括如下几种：

  `ArrayDeque`：数组存储。实现Deque接口，而Deque是Queue接口的子接口，代表**双端队列**（double-ended queue）。

  `LinkedList`：链表存储。实现List接口和Duque接口，不仅可做队列，还可以作为双端队列，或栈（stack）来使用。

### 如何自己用数组实现一个队列？

队列的主要操作有：

* `add()`
  队尾追加元素
* `poll()`
  弹出队首元素
* `size()`
  返回队列长度
* `empty()`
  判断队列为空

下面利用Java的`ArrayList`和一个头指针实现一个简单的队列。（注意：为了将重点放在实现队列上，做了适当简化。该队列仅支持整数类型，若想实现泛型，可用反射机制和object对象传参；此外，可多做安全检查并抛出异常）

```java
class MyQueue {
    private ArrayList<Integer> elements;  // 用ArrayList存储队列内部元素
    private int pointer;  // 表示队头的位置

    // 队列初始化
    public MyQueue() {
        this.elements = new ArrayList<>();
        pointer = 0;
    }

    // 获取队列中元素个数
    public int size() {
        return this.elements.size() - pointer;
    }

    // 判断队列是否为空
    public boolean empty() {
        return this.size() == 0;
    }

    // 在队尾添加一个元素
    public void add(Integer e) {
        this.elements.add(e);
    }

    // 弹出队首元素，如果为空则返回null
    public Integer poll() {
        if (this.empty()) {
            return null;
        }
        return this.elements.get(pointer++);
    }
}
```

### 队列在工业界的应用

队列可用于实现消息队列（message queue），以完成异步（asynchronous）任务。

“消息”是计算机间传送的数据，可以只包含文本；也可复杂到包含嵌入对象。当消息“生产”和“消费”的速度不一致时，就需要消息队列，临时保存那些已经发送而并未接收的消息。例如集体打包调度，服务器繁忙时的任务处理，事件驱动等等。

常用的消息队列实现包括[RabbitMQ](http://www.rabbitmq.com/)，[ZeroMQ](http://zeromq.org/)等等。

### DOC Intro

A collection designed for holding elements prior to processing. Besides basic[`Collection`](https://docs.oracle.com/javase/7/docs/api/java/util/Collection.html)operations, queues provide additional insertion, extraction, and inspection operations. Each of these methods exists in two forms: one throws an exception if the operation fails, the other returns a special value \(either null or false, depending on the operation\). The latter form of the insert operation is designed specifically for use with capacity-restricted Queue implementations; in most implementations, insert operations cannot fail.

|  | _Throws exception_ | _Returns special value_ |
| :--- | :--- | :--- |
| **Insert** | [`add(e)`](https://docs.oracle.com/javase/7/docs/api/java/util/Queue.html#add%28E%29) | [`offer(e)`](https://docs.oracle.com/javase/7/docs/api/java/util/Queue.html#offer%28E%29) |
| **Remove** | [`remove()`](https://docs.oracle.com/javase/7/docs/api/java/util/Queue.html#remove%28%29) | [`poll()`](https://docs.oracle.com/javase/7/docs/api/java/util/Queue.html#poll%28%29) |
| **Examine** | [`element()`](https://docs.oracle.com/javase/7/docs/api/java/util/Queue.html#element%28%29) | [`peek()`](https://docs.oracle.com/javase/7/docs/api/java/util/Queue.html#peek%28%29) |

Queues typically, but do not necessarily, order elements in a FIFO \(first-in-first-out\) manner. Among the exceptions are priority queues, which order elements according to a supplied comparator, or the elements' natural ordering, and LIFO queues \(or stacks\) which order the elements LIFO \(last-in-first-out\). Whatever the ordering used, the\_head\_of the queue is that element which would be removed by a call to[`remove()`](https://docs.oracle.com/javase/7/docs/api/java/util/Queue.html#remove%28%29)or[`poll()`](https://docs.oracle.com/javase/7/docs/api/java/util/Queue.html#poll%28%29). In a FIFO queue, all new elements are inserted at the\_tail\_of the queue. Other kinds of queues may use different placement rules. EveryQueueimplementation must specify its ordering properties.

The[`offer`](https://docs.oracle.com/javase/7/docs/api/java/util/Queue.html#offer%28E%29)method inserts an element if possible, otherwise returningfalse. This differs from the[`Collection.add`](https://docs.oracle.com/javase/7/docs/api/java/util/Collection.html#add%28E%29)method, which can fail to add an element only by throwing an unchecked exception. Theoffermethod is designed for use when failure is a normal, rather than exceptional occurrence, for example, in fixed-capacity \(or "bounded"\) queues.

The[`remove()`](https://docs.oracle.com/javase/7/docs/api/java/util/Queue.html#remove%28%29)and[`poll()`](https://docs.oracle.com/javase/7/docs/api/java/util/Queue.html#poll%28%29)methods remove and return the head of the queue. Exactly which element is removed from the queue is a function of the queue's ordering policy, which differs from implementation to implementation. Theremove\(\)andpoll\(\)methods differ only in their behavior when the queue is empty: theremove\(\)method throws an exception, while thepoll\(\)method returnsnull.

The[`element()`](https://docs.oracle.com/javase/7/docs/api/java/util/Queue.html#element%28%29)and[`peek()`](https://docs.oracle.com/javase/7/docs/api/java/util/Queue.html#peek%28%29)methods return, but do not remove, the head of the queue.

TheQueueinterface does not define theblocking queue methods, which are common in concurrent programming. These methods, which wait for elements to appear or for space to become available, are defined in the[`BlockingQueue`](https://docs.oracle.com/javase/7/docs/api/java/util/concurrent/BlockingQueue.html)interface, which extends this interface.

Queue implementations generally do not allow insertion ofnullelements, although some implementations, such as[`LinkedList`](https://docs.oracle.com/javase/7/docs/api/java/util/LinkedList.html), do not prohibit insertion ofnull. Even in the implementations that permit it,nullshould not be inserted into aQueue, asnullis also used as a special return value by thepollmethod to indicate that the queue contains no elements.

Queue implementations generally do not define element-based versions of methodsequalsandhashCodebut instead inherit the identity based versions from classObject, because element-based equality is not always well-defined for queues with the same elements but different ordering properties.

# Deque

A linear collection that supports element insertion and removal at both ends. The name deque is short for "double ended queue" and is usually pronounced "deck". Most Deque implementations place no fixed limits on the number of elements they may contain, but this interface supports capacity-restricted deques as well as those with no fixed size limit.

---

The twelve methods described above are summarized in the following table:

|  | **First Element \(Head\)** | **First Element \(Head\)** | **Last Element \(Tail\)** | **Last Element \(Tail\)** |
| :--- | :--- | :--- | :--- | :--- |
|  | _Throws exception_ | _Special value_ | _Throws exception_ | _Special value_ |
| **Insert** | [`addFirst(e)`](https://docs.oracle.com/javase/7/docs/api/java/util/Deque.html#addFirst%28E%29) | [`offerFirst(e)`](https://docs.oracle.com/javase/7/docs/api/java/util/Deque.html#offerFirst%28E%29) | [`addLast(e)`](https://docs.oracle.com/javase/7/docs/api/java/util/Deque.html#addLast%28E%29) | [`offerLast(e)`](https://docs.oracle.com/javase/7/docs/api/java/util/Deque.html#offerLast%28E%29) |
| **Remove** | [`removeFirst()`](https://docs.oracle.com/javase/7/docs/api/java/util/Deque.html#removeFirst%28%29) | [`pollFirst()`](https://docs.oracle.com/javase/7/docs/api/java/util/Deque.html#pollFirst%28%29) | [`removeLast()`](https://docs.oracle.com/javase/7/docs/api/java/util/Deque.html#removeLast%28%29) | [`pollLast()`](https://docs.oracle.com/javase/7/docs/api/java/util/Deque.html#pollLast%28%29) |
| **Examine** | [`getFirst()`](https://docs.oracle.com/javase/7/docs/api/java/util/Deque.html#getFirst%28%29) | [`peekFirst()`](https://docs.oracle.com/javase/7/docs/api/java/util/Deque.html#peekFirst%28%29) | [`getLast()`](https://docs.oracle.com/javase/7/docs/api/java/util/Deque.html#getLast%28%29) | [`peekLast()`](https://docs.oracle.com/javase/7/docs/api/java/util/Deque.html#peekLast%28%29) |

This interface extends the[`Queue`](https://docs.oracle.com/javase/7/docs/api/java/util/Queue.html)interface. When a deque is used as a queue, FIFO \(First-In-First-Out\) behavior results. Elements are added at the end of the deque and removed from the beginning. The methods inherited from theQueueinterface are precisely equivalent toDequemethods as indicated in the following table:

| **QueueMethod** | **EquivalentDequeMethod** |
| :--- | :--- |
| [`add(e)`](https://docs.oracle.com/javase/7/docs/api/java/util/Queue.html#add%28E%29) | [`addLast(e)`](https://docs.oracle.com/javase/7/docs/api/java/util/Deque.html#addLast%28E%29) |
| [`offer(e)`](https://docs.oracle.com/javase/7/docs/api/java/util/Queue.html#offer%28E%29) | [`offerLast(e)`](https://docs.oracle.com/javase/7/docs/api/java/util/Deque.html#offerLast%28E%29) |
| [`remove()`](https://docs.oracle.com/javase/7/docs/api/java/util/Queue.html#remove%28%29) | [`removeFirst()`](https://docs.oracle.com/javase/7/docs/api/java/util/Deque.html#removeFirst%28%29) |
| [`poll()`](https://docs.oracle.com/javase/7/docs/api/java/util/Queue.html#poll%28%29) | [`pollFirst()`](https://docs.oracle.com/javase/7/docs/api/java/util/Deque.html#pollFirst%28%29) |
| [`element()`](https://docs.oracle.com/javase/7/docs/api/java/util/Queue.html#element%28%29) | [`getFirst()`](https://docs.oracle.com/javase/7/docs/api/java/util/Deque.html#getFirst%28%29) |
| [`peek()`](https://docs.oracle.com/javase/7/docs/api/java/util/Queue.html#peek%28%29) | [`peekFirst()`](https://docs.oracle.com/javase/7/docs/api/java/util/Deque.html#peek%28%29) |

Deques can also be used as LIFO \(Last-In-First-Out\) stacks. This interface should be used in preference to the legacy[`Stack`](https://docs.oracle.com/javase/7/docs/api/java/util/Stack.html)class. When a deque is used as a stack, elements are pushed and popped from the beginning of the deque. Stack methods are precisely equivalent toDequemethods as indicated in the table below:

| **Stack Method** | **EquivalentDequeMethod** |
| :--- | :--- |
| [`push(e)`](https://docs.oracle.com/javase/7/docs/api/java/util/Deque.html#push%28E%29) | [`addFirst(e)`](https://docs.oracle.com/javase/7/docs/api/java/util/Deque.html#addFirst%28E%29) |
| [`pop()`](https://docs.oracle.com/javase/7/docs/api/java/util/Deque.html#pop%28%29) | [`removeFirst()`](https://docs.oracle.com/javase/7/docs/api/java/util/Deque.html#removeFirst%28%29) |
| [`peek()`](https://docs.oracle.com/javase/7/docs/api/java/util/Deque.html#peek%28%29) | [`peekFirst()`](https://docs.oracle.com/javase/7/docs/api/java/util/Deque.html#peekFirst%28%29) |

Note that the[`peek`](https://docs.oracle.com/javase/7/docs/api/java/util/Deque.html#peek%28%29)method works equally well when a deque is used as a queue or a stack; in either case, elements are drawn from the beginning of the deque.

This interface provides two methods to remove interior elements,[`removeFirstOccurrence`](https://docs.oracle.com/javase/7/docs/api/java/util/Deque.html#removeFirstOccurrence%28java.lang.Object%29)and[`removeLastOccurrence`](https://docs.oracle.com/javase/7/docs/api/java/util/Deque.html#removeLastOccurrence%28java.lang.Object%29).

