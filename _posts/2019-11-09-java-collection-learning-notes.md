---
layout: post
title: "Java Collection learning notes"
category: 
catalog: true
tags: 
date: 2019-11-09
header-img: 
post_copyright: true
author: Jerry
---

容器类的对象实例成为容器，用于保存对象。

# 容器

按照存储的元素形式，按照接口划分为两类：

## Collection
<div class="tip inlineBlock important">包括List，Set，Queue。</div>
1. List：按照元素被插入时的顺序保存的元素
   - ArrayList：性能
   - LinkedList
2. Set：不能有重复元素
   - TreeSet：按照比较结果升序保存对象
   - HashSet：以最快的速度访问目标存储的元素，不考虑顺序
     - LinkedHashSet：按照元素被添加的顺序保存对象
3. Queue：按照排队规则确定的元素顺序
   - PriorityQueue

## Map
<div class="tip inlineBlock important">一系列由键值对组成的序列，允许通过键查找值</div>
- HashMap：最快速度不考虑键值对顺序
   - LinkedHashMap：按照键值对插入顺序保存键值对，并将保持接近HashMap的访问速度。
- TreeMap：按照键的比较结果升序保存键值对

# 容器具体代码实现

```java
public class TestCollection {
    /**
     *
     * @param col
     * 用fill方法接受所有collection类型的容器，
     * 这些容器都实现了用于添加元素的add方法
     * @return col
     */
    Collection<String> fill(Collection<String> col) {
        col.add("java");
        col.add("c");
        col.add("py");
        return col;
    }

    /**
     *
     * @param map
     * 用fill方法接受所有collection类型的容器，
     * 这些类型都能够通过put(key,value)添加键值对
     * 通过get(key)查找键随对应的值
     * @return map
     */
    Map<String, Integer> fill(Map<String, Integer> map) {
        map.put("java", 19);
        map.put("c", 22);
        map.put("py", 1);
        return map;
    }

    public static void main(String[] args) {
        TestCollection tc = new TestCollection();
        System.out.println("ArrayList:"+tc.fill(new ArrayList<String>()));
        System.out.println("LinkList:"+tc.fill(new LinkedList<String>()));
        System.out.println("HashSet:"+tc.fill(new HashSet<String>()));
        System.out.println("LinkedHashSet:"+tc.fill(new LinkedHashSet<String>()));
        System.out.println("HashMap:"+tc.fill(new HashMap<String, Integer>()));
        System.out.println("TreeMap:"+tc.fill(new TreeMap<String, Integer>()));
    }
}
//输出结果
ArrayList:[java, c, py]
LinkList:[java, c, py]
HashSet:[java, c, py]
LinkedHashSet:[java, c, py]
HashMap:{java=19, c=22, py=1}
TreeMap:{c=22, java=19, py=1}

```

## Set接口

| 接口方法                            | 含义                                                         |
| ----------------------------------- | ------------------------------------------------------------ |
| boolean addAll(Collection<> c)      | 对于容器c的所有元素，如果有不存在于当前Set的元素，就加入，然后返回true |
| void clear()                        | 移除当前Set的所有元素                                        |
| boolean contains(Object c)          | 若指定元素存在当前Set，则返回true                            |
| boolean containsAll(Collection<> c) | 类似于上                                                     |
| boolean isEmpty()                   | 不包含元素返回true                                           |
| boolean remove(Object c)            | 若包含，则移除                                               |
| boolean retainAll(Collection<> c)   | 只保留当前Set中同时也包含在指定容器中的元素，集合发生改变返回true |
| int size()                          | 返回当前Set中元素                                            |
| Object[] toArray()                  | 返回一个数组，该数组由当前Set中所有元素组成                  |
| boolean add(E e)                    | 若元素不在当前Set中，则加入                                  |



```java
public class TestSet {
    public static void main(String[] args) {
        Random rand = new Random(47);
        Set<Integer> s = new HashSet<Integer>();
        for(int i = 0; i<5000; i++){
            s.add(rand.nextInt(40));
        }
        System.out.println(s);
        s = new TreeSet<Integer>();
        for(int i = 0; i<5000; i++){
            s.add(rand.nextInt(40));
        }
        System.out.println(s);
        s = new LinkedHashSet<Integer>();
        for(int i = 0; i<5000; i++){
            s.add(rand.nextInt(40));
        }
        System.out.println(s);
    }
}
```

输出结果：

```java
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33, 34, 35, 36, 37, 38, 39]
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33, 34, 35, 36, 37, 38, 39]
[28, 15, 39, 14, 16, 29, 24, 37, 6, 25, 2, 1, 32, 3, 36, 38, 5, 22, 23, 7, 8, 21, 33, 17, 18, 30, 31, 0, 27, 4, 19, 9, 12, 35, 34, 10, 26, 20, 13, 11]
```

当我们想将任意类型的T实例放入Set容器中，需要额外定义。

若要改变TreeSet中的元素排列方式，需要更改元素类型对于Comparable接口的实现。

先留下一个坑，具体怎么更改以后再说。

## List接口

| 接口方法                                   | 含义                                                         |
| ------------------------------------------ | ------------------------------------------------------------ |
| void add(int index,E element)              | 向指定位置插入特定元素                                       |
| boolean addAll(int index, Collection<> c)  | 指定位置插入容器c的所有元素                                  |
| E get(int index)                           | 返回指定位置的元素                                           |
| int indexOf(Object c)                      | 返回指定元素在List中第一次出现的索引值，若没出现则返回-1     |
| int lastIndexOf(Object c)                  | 类似                                                         |
| E remove(int index)                        | 移除指定位置元素                                             |
| E set(int index,E element)                 | 用特定元素E替换指定位置的元素                                |
| List<E> subList(int fromIndex,int toIndex) | 返回一个从fromIndex到toIndex的子List，对于此子List的修改和删除能反映到原List |



```java
public class TestList {
    public void draw(Shape s){
        s.draw();
    }
    public void draw(List<Shape> ss){
        for(int i = 0; i<ss.size(); i++){
            draw(ss.get(i));
        }
    }
    public static void main(String[] args) {
        List<Shape> ss = new ArrayList<Shape>();
        Random rand = new Random(3);
        for(int i = 0; i<5; i++)
        {
            switch (rand.nextInt(3)){
                case 0: ss.add(i,new Circle());break;//在指定位置插入特定元素
                case 1: ss.add(new Rectangle());break;//在末尾插入Rectangle
                case 2: ss.add(0,new Triangle());break;//在List头部插入特定元素
                default:
            }
        }
        TestList ts = new TestList();
        ts.draw(ss);
        ss.set(ss.size()-2,new Triangle());//set方法将容器倒数第二个元素替换为Triangle元素
        Shape s = ss.get(ss.size()-2);//get方法获取指定index的元素并返回
        ss.remove(ss.indexOf(s));//当不知道索引值时可循环调用根据元素获取索引然后用这个索引remove
        System.out.println("------------");
        ts.draw(ss);
    }
}
class Shape{
    void draw(){};
}
class Circle extends Shape{
    @Override
    void draw(){System.out.println("draw Circle");}
}
class Rectangle extends Shape{
    @Override
    void draw() {
        System.out.println("draw rectangle");
    }
}
class Triangle extends Shape{
    @Override
    void draw() {
        System.out.println("draw Triangle");
    }
}
```

输出结果：

```java
draw Triangle
draw Triangle
draw Circle
draw rectangle
draw Circle
------------
draw Triangle
draw Triangle
draw Circle
draw Circle
```

