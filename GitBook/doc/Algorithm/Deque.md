[toc]

# Deque

`Deque`表示双端队列。双端队列是在两端都可以进行插入和删除的队列。

现在`Stack`和`Queue`都可以直接用`Deque`. 其常用方法有：

> Set a new Deque

```java
Deque<Integer> deque = new LinkedList<>();
```

> Judge if the deque is empty

```java
deque.isEmpty()
```

> Add the element from the front or the end

```java
offerFirst()
offerLast()
```

> Get and delete the element from the front or the end

```java
pollFirst()
pollLast()
```

> search the first or the last element

```java
peekFirst()
peekLast()
```

 Others:

> delete the first or the last element which needs to be searched

```java
removeFirstOccurrence(ele)
removeLastOccurrence(ele)
```

