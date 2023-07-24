
## java基础

### 数据类型
- 1.int Integer的区别，为什么有了int还要Integer
```
`int` 是 Java 的基本数据类型之一，用于表示整数。它在内存中占据固定的大小（通常是32位），并且直接存储数据值。

`Integer` 是 `int` 的包装类（Wrapper Class），它提供了一些额外的功能和操作，使得 `int` 类型具有对象特性。`Integer` 类封装了一个原始的 `int` 值，并提供了一系列方法来处理 `int` 类型的数据。

下面是 `int` 和 `Integer` 之间的一些区别：

1. 对象与基本类型：`int` 是基本数据类型，而 `Integer` 是一个对象。这意味着 `int` 不具备对象的性质，而 `Integer` 可以作为对象进行操作。

2. 自动装箱和拆箱：Java 提供了自动装箱和拆箱的机制，可以在 `int` 和 `Integer` 之间进行自动转换。装箱是指将 `int` 转换为相应的 `Integer` 对象，而拆箱则是将 `Integer` 对象转换为 `int`。例如，可以直接将 `int` 赋值给 `Integer`，或者将 `Integer` 直接传递给期望 `int` 参数的方法。

3. Null 值：`int` 是基本数据类型，不能为 `null`；而 `Integer` 可以为 `null`，因为它是一个对象。

4. 泛型支持：由于 `Integer` 是一个类，它可以作为泛型类型的参数，而 `int` 不能。这样可以在需要使用泛型的场景下，使用 `Integer` 进行操作。

为什么有了 `int` 还要有 `Integer` 呢？有几个原因：

1. Java 的集合类（例如 `List`、`Set`、`Map`）只能存储对象，不能直接存储基本数据类型。所以需要通过 `Integer` 这样的包装类来将 `int` 转换为对象，以便在集合中进行操作。

2. `Integer` 类提供了一些实用的方法，例如将 `String` 转换为 `int`、将 `int` 转换为 `String`、比较大小等等。

3. 在某些情况下，需要把 `int` 当作对象来使用，例如在使用泛型、反射等特定的场景下。

总之，`int` 是基本数据类型，而 `Integer` 是对 `int` 的封装，提供了更多的功能和灵活性。根据具体的需求，选择合适的类型进行使用。
```

### ArrayList & LinkedList
- 1.ArrayList  LinkedList 扩容机制有什么不同
```
`ArrayList` 和 `LinkedList` 是 Java 中常用的两种集合类，它们在扩容机制上有一些不同之处。

`ArrayList` 的底层实现是动态数组，它通过一个连续的内存块来存储元素。当 `ArrayList` 需要扩容时，会创建一个更大的数组，并将原来的元素复制到新数组中。默认情况下，`ArrayList` 的初始容量为10，扩容时会按照当前容量的1.5倍进行扩容。

例如，如果 `ArrayList` 的当前容量为10，当添加第11个元素时，会触发扩容操作，将容量扩展为15。这样可以避免频繁的扩容操作，在一定程度上提高性能。但是，如果事先知道要存储的元素数量较多，可以使用带有初始容量参数的构造函数来减少扩容次数。

相比之下，`LinkedList` 的底层实现是双向链表，每个节点包含了元素本身和对前后节点的引用。当 `LinkedList` 需要扩容时，不需要像 `ArrayList` 那样创建新的数组，而是直接在链表的尾部添加新的节点。

由于 `LinkedList` 的扩容操作只需要创建一个新的节点并链接到链表尾部，因此相对于 `ArrayList`，`LinkedList` 的扩容过程通常更高效。然而，`LinkedList` 在访问和搜索元素时的性能相对较低，因为需要遍历链表来查找指定位置的元素。

总结起来，`ArrayList` 的扩容机制是创建一个更大的数组并复制元素，而 `LinkedList` 的扩容机制是在链表尾部添加新的节点。`ArrayList` 的扩容操作可能会涉及数据的复制，而 `LinkedList` 的扩容操作则只需创建新的节点。
选择使用哪种集合类，取决于具体的场景和需求。如果需要频繁地进行随机访问和搜索操作，可以选择 `ArrayList`；如果需要频繁地进行插入和删除操作，可以选择 `LinkedList`。
```

### TreeMap & HashMap & ConcurrentHashMap
- 1.HashMap的底层数据结构，什么时候扩容？怎么扩容？为什么扩容为两倍
```
`HashMap` 是 Java 中常用的哈希表（Hash Table）实现，它使用数组和链表（或红黑树）来存储键值对。具体来说，`HashMap` 的底层数据结构是一个数组，每个数组元素都是一个链表（或红黑树）的头节点。当链表的长度达到一定的阈值（默认为8），会转换为红黑树，以提高查找效率。

`HashMap` 在什么时候扩容呢？当哈希表中存储的元素数量超过了当前容量与负载因子的乘积时，就会触发扩容操作。负载因子（load factor）是指哈希表中已存储元素数量与当前容量的比值。默认情况下，负载因子为0.75，即当元素数量超过容量的 75% 时，会触发扩容。
默认大小为16，在容量到达12时会触发扩容

在进行扩容时，`HashMap` 会创建一个新的更大的数组，通常将容量扩大为原来的两倍。然后遍历旧数组中的每个元素，并重新计算它们在新数组中的位置，并将其放入新数组中。这样可以保证元素在新数组中的散列分布更加均匀，减少冲突的概率。

为什么扩容的容量一般为原来的两倍呢？这是因为在哈希表中，元素的散列位置由键的 `hashCode()` 方法返回的散列值决定。当容量扩大一倍时，数组的长度也会变为原来的两倍，这意味着原来的散列值的低位部分将保持不变，这样可以确保元素在新的数组中的散列位置与原来相同或者更靠近。

选择扩容为两倍是为了平衡空间利用率和性能。扩容为两倍可以减少扩容操作的频率，使得哈希表在存储足够多的元素时，仍然保持较好的性能。同时，扩容为两倍也有助于减少哈希碰撞（hash collisions）的概率，提高查找效率。

综上所述，`HashMap` 的底层数据结构是一个数组和链表（或红黑树）组成的哈希表。它在元素数量超过容量与负载因子的乘积时进行扩容操作，将容量扩大为原来的两倍，以实现更好的空间利用率和性能。
```
- 2.有没有map的key是按顺序排序的，具体是怎么实现的

```
在 Java 中，`HashMap` 是无序的，它不会保持键的任何特定顺序。如果你需要有序的键值对集合，可以使用 `TreeMap` 或 `LinkedHashMap`。

TreeMap遍历结果是有序的
LinkedHashMap保持了元素插入的顺序

`TreeMap` 是基于红黑树实现的有序映射。它根据键的自然顺序或指定的比较器对键进行排序，并且在遍历时按照键的顺序返回结果。这使得 `TreeMap` 的键是有序的。

以下是一个使用 `TreeMap` 的示例：

TreeMap<Integer, String> treeMap = new TreeMap<>();
treeMap.put(3, "Apple");
treeMap.put(1, "Banana");
treeMap.put(2, "Orange");

for (Integer key : treeMap.keySet()) {
    System.out.println(key + ": " + treeMap.get(key));
}

输出结果将按照键的顺序进行排序：

1: Banana
2: Orange
3: Apple

另外，`LinkedHashMap` 是基于哈希表和双向链表实现的，它保持了元素插入的顺序。在遍历时，`LinkedHashMap` 会按照插入的顺序返回结果。虽然 `LinkedHashMap` 不会根据键进行排序，但它会保持元素的插入顺序。

以下是一个使用 `LinkedHashMap` 的示例：
LinkedHashMap<Integer, String> linkedHashMap = new LinkedHashMap<>();
linkedHashMap.put(3, "Apple");
linkedHashMap.put(1, "Banana");
linkedHashMap.put(2, "Orange");

for (Integer key : linkedHashMap.keySet()) {
    System.out.println(key + ": " + linkedHashMap.get(key));
}

输出结果将按照元素插入的顺序进行返回：

3: Apple
1: Banana
2: Orange

总结起来，`HashMap` 是无序的，不保证键的任何特定顺序。如果需要有序的键值对集合，可以使用 `TreeMap`（基于红黑树）或 `LinkedHashMap`（保持插入顺序）。
```

- 3.ConcurrentHashMap是怎么实现线程安全的
```
`ConcurrentHashMap` 的线程安全是通过以下几个关键点来实现的：

1. 分段锁（Segment）：`ConcurrentHashMap` 内部被分成多个段，每个段维护了一个独立的小型哈希表。不同的线程可以同时访问和修改不同的段，以提高并发性能。每个段都有自己的锁，因此线程在访问时只需要获取对应段的锁而不需要锁住整个 `ConcurrentHashMap`，从而减小了锁的粒度。

2. CAS（Compare and Swap）操作：`ConcurrentHashMap` 使用 CAS 操作来实现无阻塞的并发控制。CAS 是一种乐观锁机制，它比较当前值与期望值是否相等，如果相等则更新为新值，如果不相等则重新尝试。这样可以避免传统的互斥锁带来的线程阻塞和上下文切换开销。

3. 线程安全的操作：在 `ConcurrentHashMap` 中，读取操作（如 get）可以无锁地进行，并且不会引入并发问题。对于写入操作（如 put、remove）以及更新操作（如 putIfAbsent、replace、compute），需要获取对应段的锁来保证线程安全性。

4. 安全迭代器：`ConcurrentHashMap` 的迭代器（Iterator）是弱一致性的。这意味着迭代器在迭代开始时反映了初始状态，并且可能会看到其他线程进行的更新操作，但不保证能获取到最新的写入结果。这样可以避免在迭代过程中抛出 `ConcurrentModificationException` 异常。

通过上述机制，`ConcurrentHashMap` 实现了高效的并发访问和修改操作。它允许多个线程同时读取数据，并且在保证线程安全的前提下进行并行的写入和更新操作。分段锁减小了锁的粒度，CAS 操作避免了阻塞和上下文切换开销，以及对读取操作的无锁优化，使得 `ConcurrentHashMap` 能够在多线程环境下提供高性能的并发操作。
```
- 4.ConcurrentHashMap一共分了多少Segment，并发线程数超过Segment会发生什么
```
`ConcurrentHashMap` 的初始时会根据指定的并发级别（concurrency level）或默认值创建多个初始段（segments）。每个段相当于一个独立的小型哈希表，用于存储键值对。

默认情况下，`ConcurrentHashMap` 使用16个段来实现并发性。可以通过在构造函数中指定不同的并发级别来调整初始段的数量。例如，使用 `ConcurrentHashMap(int initialCapacity, float loadFactor, int concurrencyLevel)` 构造函数来创建一个新的 `ConcurrentHashMap` 实例，并指定并发级别。

如果并发线程数超过了 `ConcurrentHashMap` 的段数，仍然可以继续正常工作，因为不同线程可以同时访问和修改不同的段。只要锁争用不过于激烈，分段锁机制就能提供较好的并发性能。

然而，当并发线程数远远超过段数时，锁争用可能会变得非常激烈，导致性能下降。这是因为线程将频繁地等待获取段级别的锁，从而引入了大量的线程竞争和上下文切换开销。

为了避免这种情况，可以考虑增加 `ConcurrentHashMap` 的初始段数，以适应更高的并发线程数。另外，也可以使用其他并发数据结构如 `ConcurrentSkipListMap` 或者使用分布式缓存系统来满足更高的并发需求。

总结起来，`ConcurrentHashMap` 的初始段数默认为16，它可以支持多线程并发访问和修改。如果并发线程数超过了段数，仍然可以正常工作，但可能会出现锁争用导致性能下降的情况。在高并发环境中，可以通过调整并发级别或考虑其他并发数据结构来提高性能和并发能力。
```
