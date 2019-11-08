title: Java类加载
comments: true
date: 2019-03-22 10:30:12
updated: 2019-03-22 10:30:12
tags:
  - java_base
  - knowledge
  - skills
categories:
  - java
---

### 一、类内部加载顺序
- 1.父类static{} 只加载一次
- 2.本身static{} 只加载一次
- 3.父类{}块 每次
- 4.父类构造器 每次
- 5.本身{}块 每次
- 6.本身构造器 每次

<details>
  <summary>类内部加载顺序实例</summary>
  <a href='https://github.com/xuegangliu/javaBasic/tree/master/jbs-problem/src/main/java/com/lxg/problem/clazz/v1' target="_blank">代码链接</a>
  <br/>
  <code>
    package com.lxg.problem.clazz.v1;
    
    /**************************
     *  Aa
     * @author xuegangliu
     *  2019/3/22 14:06
     ***************************/
    public interface Aa {
    
        String VERSION="v1.0.0";
    
        /**
         * say
         */
        void say();
    
        /**
         * main
         * @param args
         */
        static void main(String[] args) {
            System.out.println("interface Aa main()");
        }
    }
    
    package com.lxg.problem.clazz.v1;

    /**************************
     *  Bb
     * @author xuegangliu
     *  2019/3/22 14:06
     ***************************/
    public class Bb {
        private static String name="Bb static prop name";
        private String name1;
    
        static {
            System.out.println("Bb static{}");
        }
    
        {
            System.out.println("Bb {}");
        }
    
        public Bb(){
            System.out.println("Bb()");
        }
    
        public Bb(String name1){
            this.name1=name1;
            System.out.println("Bb(String name1)");
        }
    
        public void talk(){
            System.out.println("b.talk(){}");
        }
    
        public static void main(String[] args) {
            System.out.println("----------Bb main()");
            Bb t=new Bb();
            System.out.println(t.name1);
            t.talk();
        }
    }

    package com.lxg.problem.clazz.v1;
    
    
    /**************************
     *  Cc
     * @author xuegangliu
     *  2019/3/22 14:06
     ***************************/
    public  class Cc extends Bb implements Aa {
    
        private static String name = "Cc";
    
        private String name1="c";
    
        static {
            System.out.println("Cc static{}"+VERSION);
        }
    
        {
            System.out.println("Cc {}");
        }
    
        public Cc(){
            System.out.println("Cc()");
        }
    
        public Cc(String name1){
            this.name1=name1;
            System.out.println("Cc(String name1)");
        }
    
        public static void ok(){
            System.out.println("Cc static Cc.ok()");
        }
    
        @Override
        public void say() {
            System.out.println("c.say()");
        }
    
        @Override
        public void talk(){
            super.talk();
            System.out.println("c.talk(){}");
        }
    
        public static void main(String[] args) {
            // 1.父类的static{}只加载一次     Bb static{}
            // 2.当前类的static{}只加载一次   Cc static{}v1.0.0
            // 3.当前方法           -----Cc main()
            System.out.println("===============Cc main()");
    
            // 4.父类 {}块          Bb {}
            // 5.父类 构造器         Bb()
            // 6.当前类 {}块         Cc {}
            // 7.当前类 构造器       Cc()
            Cc c=new Cc();
            System.out.println(c.name1);
            c.say();
            c.talk();
            System.out.println("===============");
            Cc c1=new Cc();
        }
    }


  </code>
</details>

### 二、Java 基本数据类型
- 内置数据类型
    - (byte(8位有符号,java.lang.Byte)
    - short(16位有符号,java.lang.Short)
    - int(32位有符号,java.lang.Integer)
    - long(64位有符号,java.lang.Long)
    - float(32位,java.lang.Float)
    - double(64位,java.lang.Double)
    - boolean(1位)
    - char(单一的 16 位 Unicode 字符,java.lang.Character)
    - void(java.lang.Void)

### 三、Java数据结构（集合框架）
- 接口:
    - java.lang.Iterable、java.util.Collection|java.util.concurrent.Callable、java.util.concurrent.Executor
    - java.util.List
    - java.util.Queue（单向队列）、java.util.Deque(双向队列)|java.util.concurrent.BlockingQueue,java.util.concurrent.BlockingDeque、java.util.concurrent.TransferQueue(1.7)
    - Set、SortedSet、NavigableSet
    - java.util.Map、java.util.SortedMap、java.util.NavigableMap|java.util.concurrent.ConcurrentMap、java.util.concurrent.ConcurrentNavigableMap
- 数组：java.util.Vector[同步]、java.util.ArrayList、java.util.LinkedList|java.util.concurrent.CopyOnWriteArrayList
- 栈：java.util.Stack 数据入栈和出栈的时间复杂度都为O(1)[Deque接口方法可以实现stack的方法，可以代替stack]
- 队列：java.util.PriorityQueue、java.util.ArrayDeque
    - 不阻塞队列 ：java.util.PriorityQueue、java.util.concurrent.ConcurrentLinkedQueue
    - 阻塞队列：java.util.concurrent.ArrayBlockingQueue、java.util.concurrent.DelayQueue、java.util.concurrent.LinkedBlockingDeque、java.util.concurrent.LinkedBlockingQueue、java.util.concurrent.PriorityBlockingQueue、java.util.concurrent.SynchronousQueue
- Set：java.util.HashSet、java.util.LinkedHashSet、java.util.TreeSet|java.util.concurrent.ConcurrentSkipListSet、java.util.concurrent.CopyOnWriteArraySet
- Map：java.util.HashMap、java.util.LinkedHashMap、java.util.IdentityHashMap、java.util.TreeMap、java.util.WeakHashMap、java.util.Hashtable[同步]、java.util.Properties[同步]|java.util.concurrent.ConcurrentHashMap、java.util.concurrent.ConcurrentSkipListMap
- 工具类：java.util.Arrays、java.util.Collections|java.util.concurrent.Executors