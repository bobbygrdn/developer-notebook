![queue](https://deadpan-gravity-1d7.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fac1da9c2-2018-447a-bd9a-cc9443bc01da%2FData_Queue.svg?id=3f1861da-f74a-4634-bbcb-ac7de548e551&table=block&spaceId=d5d6fc9b-c7c0-4b6b-a6fc-cdce77529a52&userId=&cache=v2)

# Queue

- A collection of entities that are maintained in a sequence and can be modified by the addition of entities at one end of the sequence and the removal of entities from the other end of the sequence.
- The end of the sequence at which elements are added is called the *back*, *tail* or *rear* of the queue.
- The end at which elements are removed is called the *head* or *front* of the queue.
- The operation of adding an element to the rear of the queue is known as *enqueue*.
- The operation of removing an element from the front is know as *dequeue*.
- Other operations may alse be allowed, often including *peek* or *front* operation that returns the value of the next element to be dequeued without dequeuing the element.
- The operations of a queue make it a *first-in-first-out* (**FIFO**) data structure.
    - In a FIFO data structure, the first element added to the queue will be the first one to be removed.
- A queue is an example of a *linear* data structure or a *sequential collection*.
- Common implementations are *circular buffers* and *linked lists*.
- Queues provide services in computer science, transport, and operations research where various entities such as data, objects, persons, or events are stored and held to be processed later. In these contexts, the queue performs the function of a [buffer](https://en.wikipedia.org/wiki/Buffer_(computer_science)). Another usage of queues is in the implementation of [breadth-first search](https://en.wikipedia.org/wiki/Breadth-first_search).

## Time Complexity

![Time Table](https://deadpan-gravity-1d7.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F2151ab72-5985-4d48-821d-76121b937e41%2FQueue_Time_Complexity.jpg?id=4476bbf8-a7a4-4c57-b7d2-fe790a20f2b1&table=block&spaceId=d5d6fc9b-c7c0-4b6b-a6fc-cdce77529a52&width=550&userId=&cache=v2)

## Implementation

- One characteristic of a queue is that it does not have a specific capacity. Regardless of how many elements are already contained, a new element can always be added. It can also be empty, at which point removing an element will be impossible until a new element has been added again.
- Queue *overflow* results from trying to add an element onto a full queue and queue *underflow*
 happens when trying to remove an element from an empty queue.
- An efficient implementation is one that can perform the operations—en-queuing and de-queuing—in [O(1) time](https://en.wikipedia.org/wiki/Big_O_notation).
    - [Linked list](https://en.wikipedia.org/wiki/Linked_list)
        - A [doubly linked list](https://en.wikipedia.org/wiki/Doubly_linked_list) has O(1) insertion and deletion at both ends, so it is a natural choice for queues.
        - A regular singly linked list only has efficient insertion and deletion at one end. However, a small modification—keeping a pointer to the *last* node in addition to the first one—will enable it to implement an efficient queue.
    - A [deque](https://en.wikipedia.org/wiki/Double-ended_queue) implemented using a modified dynamic array

## Queues and Programming Languages

- Queues may be implemented as a separate data type, or maybe considered a special case of a [double-ended queue](https://en.wikipedia.org/wiki/Double-ended_queue) (deque) and not implemented separately. For example, [Perl](https://en.wikipedia.org/wiki/Perl)
 and [Ruby](https://en.wikipedia.org/wiki/Ruby_(programming_language)) allow pushing and popping an array from both ends, so one can use *push*
 and *shift* functions to enqueue and dequeue a list (or, in reverse, one can use *unshift*
 and *pop*), although in some cases these operations are not efficient.
- C++'s [Standard Template Library](https://en.wikipedia.org/wiki/Standard_Template_Library) provides a "`queue`" templated class which is restricted to only push/pop operations. Since J2SE5.0, Java's library contains a `[Queue](https://docs.oracle.com/javase/10/docs/api/java/util/Queue.html)` interface that specifies queue operations; implementing classes include `[LinkedList](https://docs.oracle.com/javase/10/docs/api/java/util/LinkedList.html)` and (since J2SE 1.6) `[ArrayDeque](https://docs.oracle.com/javase/10/docs/api/java/util/ArrayDeque.html)`  PHP has an [SplQueue](http://www.php.net/manual/en/class.splqueue.php) class and third party libraries like [beanstalk'd](https://en.wikipedia.org/w/index.php?title=Beanstalk%27d&action=edit&redlink=1) and [Gearman](https://en.wikipedia.org/wiki/Gearman).

```javascript
// A simple queue implemented in JavaScript
class Queue {
    constructor() {
        this.items = [];
    }

    enqueue(element) {
        this.items.push(element);
    }

    dequeue() {
        return this.items.shift();
    }
}
```

[Source Documentation](https://en.wikipedia.org/iki/queue_(abstract_data_type))