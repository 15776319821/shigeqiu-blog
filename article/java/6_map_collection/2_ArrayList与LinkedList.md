# ArrayList与LinkedList

<!-- TOC -->

- [ArrayList与LinkedList](#arraylist%e4%b8%8elinkedlist)
  - [ArrayList](#arraylist)
    - [扩容](#%e6%89%a9%e5%ae%b9)
    - [数组最大容量](#%e6%95%b0%e7%bb%84%e6%9c%80%e5%a4%a7%e5%ae%b9%e9%87%8f)
    - [默认的初始容量](#%e9%bb%98%e8%ae%a4%e7%9a%84%e5%88%9d%e5%a7%8b%e5%ae%b9%e9%87%8f)
  - [LinkedList](#linkedlist)

<!-- /TOC -->

## ArrayList

### 扩容

新容量=旧容量*1.5

``` java
/**
     * Increases the capacity to ensure that it can hold at least the
     * number of elements specified by the minimum capacity argument.
     *
     * @param minCapacity the desired minimum capacity
     */
    private void grow(int minCapacity) {
        // overflow-conscious code
        int oldCapacity = elementData.length;
        //新容量扩大到原来的1.5倍，右移一位相当于原来的值除以2
        int newCapacity = oldCapacity + (oldCapacity >> 1);
        if (newCapacity - minCapacity < 0)
            newCapacity = minCapacity;
        if (newCapacity - MAX_ARRAY_SIZE > 0)
            newCapacity = hugeCapacity(minCapacity);
        // minCapacity is usually close to size, so this is a win:
        elementData = Arrays.copyOf(elementData, newCapacity);
    }
```

### 数组最大容量

> 注释翻译过来的意思：要分配的数组的最大大小。一些vm在数组中保留一些头信息。尝试分配较大的数组可能会导致OutOfMemory错误：请求的数组大小超过了VM限制

``` java
/**
* The maximum size of array to allocate.
* Some VMs reserve some header words in an array.
* Attempts to allocate larger arrays may result in
* OutOfMemoryError: Requested array size exceeds VM limit
*/
private static final int MAX_ARRAY_SIZE = Integer.MAX_VALUE - 8;
```

### 默认的初始容量

```
/**
* Default initial capacity.
*/
private static final int DEFAULT_CAPACITY = 10;
```

## LinkedList

内部结点如下：

``` java
private static class Node<E> {
    E item;
    Node<E> next;
    Node<E> prev;

    Node(Node<E> prev, E element, Node<E> next) {
        this.item = element;
        this.next = next;
        this.prev = prev;
    }
}
```

LinkedList 是一个双向链表，没有初始化大小，也没有扩容的机制，就是一直在前面或者后面新增就好。