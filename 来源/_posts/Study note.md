---
title: Java多线程
---

## JAVA多线程

## 1.继承Thread类

***

* 1.需要继承Thread类重写run方法

* 2.在Main方法中需要调用start();方法才能与main方法同时进行

***

## 2.实现Rannable接口

***

### 大抵与Thread相同

* 既也是重写run方法  

* 不同之处是实现接口与继承的区别  

* 一个类可以implement多个接口  

* 但是不能extents多个继承

***

## 静态代理模式(Static Proxy)

***

### 创建一个代理方法来增强真实方法

* 1.真实对象和代理对象都要实现同一个接口  

* 2.代理对象要代理真实角色  

* 3.对原有方法进行增强  

* 4.真实对象可以专注做自己的事情  

***

## Lmabda表达式

***

* lambda表达式只能有一行代码的情况才能简化成为一行,如果存在多行,就需要代码块包括  

* 前提是接口为函数式接口  

* 多个参数也可以去掉参数类型,如果要去掉就要全部去掉,必须加括号

```java
        public static void main(String[] args) {
        Ilove love =null;
                //表示简化
                Ilove love = (int a) -> {
                    System.out.println("I love you" + a);
                };
                //简化参数类型
                love = (a)-> {
                    System.out.println("I love you" + a);
                };

            //简化括号
                love = a -> {
                    System.out.println("I love you" + a);
                };

            //简化大括号
            love =(a,b) -> System.out.println("I love you"+a + b)   ;
            love.love(520, 12);
    
            }
        }   

        interface Ilove{
        void love(int a ,int b);
        }
```

## 线程五大状态

***

* 创建状态  

1. 线程对象一旦创建就进入到了新生状态  

    Thread t = new Thread();

2. 当调用start()方法,线程立即进入就绪状态,但不意味着立即调度执行

* 就绪状态

    调度之后进入运行状态

* 阻塞状态
  
1. 当调用sleep,wait或同步锁定时,线程进入阻塞状态,就是代码不会继续向下执行,阻塞事件结束后,重新进入就绪状态,等待cpu调度执行

* 运行状态

1. 进入运行状态,线程才是真正执行线程体的代码块

* 死亡状态

1. 线程中断或者结束,一旦进入死亡状态,就不能再次启动

***

## 线程停止

1. 建议线程正常停止,--->利用次数,不建议死循环
2. 不要使用stop等被过时或jdk不建议使用的方法

```java
        public class TestStop implements Runnable{
       //设置一个标志位
       private  boolean flag = true;

       @Override
       public void run() {
           int i = 0;
           while (flag){
               System.out.println("run"+i++);
           }
       }

       //设置一个公开的方法停止线程,转换标志位
       public  void  stop(){
           this.flag = false;
       }

       public static void main(String[] args) {
        TestStop t = new TestStop();
        new Thread(t).start();
           for (int i = 0; i < 1000; i++) {
               System.out.println("main"+i);
               if (i == 900) {
                   //调用stop方法切换标志位,让线程停止
                   t.stop();
                   System.out.println("线程该停止了");
                }
            }
          }
        }
```

***

## 线程休眠(sleep)

### sleep的主要作用是模拟延时或作倒计时

* sleep(时间)指定当前线程阻塞的毫秒数

* sleep存在一场InterrupatedException;
  
* sleep时间达到后线程进入就绪状态

* sleep可以模拟网络延时,倒计时等

* 每个对象都有一个锁,sleep不会释放锁

***

## 线程礼让(Yidle)

* 礼让线程,让当前正在执行的线程暂停,但不阻塞

* 将线程从与运行状态转为就绪状态
  
* 让CPU重新调度,礼让不一定成功 看CPU的心情

```java
      public class StudyYield{

       public static void main(String[] args) {
           MyYield m = new MyYield();
           new Thread(m,"a").start();
           new Thread(m,"b").start();
            }   
        }

        lass  MyYield implements Runnable{

       @Override
       public void run() {
           System.out.println(Thread.currentThread().getName()+"-->是笨蛋");
           Thread.yield();
           System.out.println(Thread.currentThread().getName()+"线程停止执行");
            }
        }
```

***

## Join

* Join合并线程,待此线程执行完毕后,再执行其他线程,其他线程阻塞

* 可以想象为插队

```java
        public class TestJoin implements Runnable{
            @Override
            public void run() {
                for (int i = 0; i < 500; i++) {
                    System.out.println("vip来了"+i);
                }
            }

            public static void main(String[] args) throws       Exception{
                TestJoin t = new TestJoin();
                Thread t1 = new Thread(t);
                t1.start();
                //主线程
                for (int i = 0; i < 500; i++) {
                    if (i == 200) {
                        t1.join(); //插队
                    }
                    System.out.println("main"+i);
                }
            }
        }
```

***

## 线程状态观测(Thread.State)

* NEW  

    尚未启动的线程处于此状态。

* RUNNABLE  
  
    在Java虚拟机中执行的线程处于此状态。

* BLOCKED  
  
   被阻塞等待监视器锁定的线程处于此状态。

* WAITING  
  
    正在等待另一个线程执行特定动作的线程处于此状态。

* TIMED_WAITING  

   正在等待另一个线程执行动作达到指定等待时间的线程处于此状态。

* TERMINATED  
  
   已退出的线程处于此状态。

```java
public class TestState {

    public static void main(String[] args) {
        Thread t = new Thread(()->{
            for (int i = 0; i < 50; i++) {
                try {
                    Thread.sleep(200);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
            System.out.println("/////");
        });


        //观察状态
        Thread.State state = t.getState();
        System.out.println(state);

        //观察启动后
        t.start();
        state = t.getState();
        System.out.println(state);

        while (state != Thread.State.TERMINATED){//只要线程不停止,就一直输出状态
            try {
                Thread.sleep(100);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            state = t.getState();//更新线程状态
            System.out.println(state);
        }
        
    }

}

```

***

## 线程优先级

* java提供一个线程调度器来监控程序中启动后进入就绪状态的所有线程,线程调度器按照优先级决定应该调度哪个线程来执行.
* 线程的优先级用数字表示,范围从1 ~ 10
  
    Thread.MIN_PRIORITY = 1;

    Thread.MAX_PRIORITY = 10;

    Thread.NORM_PRIORITY = 5;

* 使用以下方法改变或获取优先级
  
  getPriority().setPriority(int xxx)

* 优先级低只是意味着获得调度的概率低,并不是优先级低就一定会被晚调用,全看CPU调度执行

```java
//测试线程的优先级
public class TestPriority {
    public static void main(String[] args) {
        //主线程默认优先级
        System.out.println(Thread.currentThread().getName()+"==>"+Thread.currentThread().getPriority());
        MyPriority m = new MyPriority();
        Thread t1 = new Thread(m);
        Thread t2 = new Thread(m);
        Thread t3 = new Thread(m);
        Thread t4 = new Thread(m);
        Thread t5 = new Thread(m);
        Thread t6 = new Thread(m);

        //先设置优先级再启动
        t1.start();

        t2.setPriority(1);
        t2.start();

        t3.setPriority(4);
        t3.start();

        t4.setPriority(Thread.MAX_PRIORITY);
        t4.start();

        t5.setPriority(8);
        t5.start();

        t6.setPriority(7);
        t6.start();
    }
}

class MyPriority implements Runnable{
    @Override
    public void run() {
        System.out.println(Thread.currentThread().getName()+"==>"+Thread.currentThread().getPriority());
    }
}
```

***

## 守护(daemon)线程

* 线程分为用户线程和守护线程

* 虚拟机必须确保用户线程执行完毕

* 虚拟机不用等守护线程执行完毕 (后台操作日志,监控内存,垃圾回收诸如此类)

```java
//上帝守护你
public class TestDaemon {
    public static void main(String[] args) {
        God god = new God();
        You you = new You();

        Thread thread = new Thread(god);
        thread.setDaemon(true);     //默认是false表示是用户线程,正常的线程都是用户线程
        thread.start();

        new Thread(you).start();   //你(用户线程)启动
    }
}


//上帝
class God implements Runnable{
    @Override
    public void run() {
        while (true){
            System.out.println("上帝保佑你");
        }
    }
}


//你
class You implements Runnable{

    @Override
    public void run() {
        for (int i = 0; i < 36500; i++) {
            System.out.println("你一生都开始新的活着");
        }
        System.out.println("======goodbye!world");
    }
}

```

***

## 线程同步

* 由于同一进程的多个线程共享一块存储空间,在带来方便的同时,也带来了访问冲突问题,为了保证数据在方法中被访问时的正确性,在访问时加入锁机制synchronized,当一个线程获得对象的排它锁,独占资源,其他线程必须等待,使用后释放锁即,存在以下问题
  
  * 一个线程持有锁会导致其他所有需要此锁的线程挂起;
  
  * 在多线程竞争下,加锁,释放锁会导致比较多的 上下文切换 和 调度延时 引起性能问题

  * 如果一个优先级高的线程等待一个优先级低的线程释放锁,会导致优先级倒置,引起性能问题.

  1. 不安全的线程1

```java
 //不安全的买票
//线程不安全 有负数
public class UnsafeBuytickets {
    public static void main(String[] args) {
        Buytickets b = new Buytickets();

        new Thread(b,"小明").start();
        new Thread(b,"张三").start();
        new Thread(b,"憨憨").start();
    }
}

class Buytickets implements Runnable{
    boolean flag = true;   //外部停止方式
    @Override
    public void run() {
        //买票
        while (flag){
            Buy();
        }
    }    private int ticketsnum = 10;


    private void Buy(){
        //判断是否有票
        if (ticketsnum <= 0) {
            flag = false;
            return;
        }
        //模拟延时
        try {
            Thread.sleep(100);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        //买票
        System.out.println(Thread.currentThread().getName()+"拿到了===>"+ticketsnum--);
    }
}
```

1. 不安全的线程2

```java
//不安全的取钱
//两个人去银行取钱,账户
public class UnsafeBank {
    public static void main(String[] args) {
        Account account = new Account(100,"结婚基金");
        Drawing you = new Drawing(account,20,"你");
        Drawing girlfriend = new Drawing(account,100,"你老婆");
        you.start();
        girlfriend.start();

    }
}

//账户
class Account{
    int money;//余额
    String name;//卡名

    public Account(int money, String name) {
        this.money = money;
        this.name = name;
    }



}

//银行
class Drawing extends Thread{
    Account account;//账户
    //取了多少钱
    int drawingMoney;
    //现在手里有多少钱
    int nowMoney;

    public Drawing(Account account,int drawingMoney,String name){
        super(name);
        this.account  = account;
        this.drawingMoney = drawingMoney;
    }

    //取钱

    @Override
    public void run() {
        //判断有没有钱
        if (account.money - drawingMoney < 0) {
            System.out.println(Thread.currentThread().getName()+"钱不够取不了");
            return;
        }
        //sleep可以放大问题的安全性
        try {
            Thread.sleep(100);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        //卡内余额 = 余额 - 你取的钱
        account.money = account.money - drawingMoney;
        //你手里的钱
        nowMoney = nowMoney + drawingMoney;
        System.out.println(account.name+"余额为"+account.money);
        //Thread.currentThread().getName() = this.getName()
        System.out.println(this.getName()+"手里的钱"+nowMoney);
    }
}
```

1. 不安全的线程3

```java

//线程不安全的集合
public class UnsafeList {
    public static void main(String[] args) {
        List<String> list = new ArrayList<String>();
        for (int i = 0; i < 10000; i++) {
            new Thread(()->{
                list.add(Thread.currentThread().getName());
            }).start();
        }
        try {
            Thread.sleep(3000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        System.out.println(list.size());
    }
}
```

### 同步方法

* 由于我们可以通过private关键字来保证数据对象只能被方法访问,所以我们只需要针对发给发提出一套机制,这套机制就是synchroizd关键字,它包括两种用法,synchroizd方法和synchroizd块.

* synchroizd方法控制"对象"的访问,每个对象对应一把锁,每个synchroizd方法都必须获得调用该方法的对象的锁才能执行,否则线程会阻塞,方法一旦执行,就独占该锁,知道方法返回才释放锁,后面阻塞的线程才能或者这个锁,继续执行
  **缺陷:若将一个大的方法申明为synchroizd将会影响效率**

 1. 修改后的代码

* 修改后的代码

```java
 public class UnsafeBuytickets {
    public static void main(String[] args) {
        Buytickets b = new Buytickets();

        new Thread(b,"小明").start();
        new Thread(b,"张三").start();
        new Thread(b,"憨憨").start();
    }
}

class Buytickets implements Runnable{
    boolean flag = true;   //外部停止方式
    @Override
    public void run() {
        //买票
        while (flag){
            Buy();
            //模拟延时
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }    private int ticketsnum = 10;


    //synchronized 同步方法,锁的是this
    private synchronized void Buy(){
        //判断是否有票
        if (ticketsnum <= 0) {
            flag = false;
            return;
        }
        //买票
        System.out.println(Thread.currentThread().getName()+"拿到了===>"+ticketsnum--);
    }
}
```

* 修改后的代码2

```java
public class UnsafeBank {
    public static void main(String[] args) {
        Account account = new Account(1000,"结婚基金");
        Drawing you = new Drawing(account,20,"你");
        Drawing girlfriend = new Drawing(account,100,"你老婆");
        you.start();
        girlfriend.start();

    }
}

//账户
class Account{
    int money;//余额
    String name;//卡名

    public Account(int money, String name) {
        this.money = money;
        this.name = name;
    }



}

//银行
class Drawing extends Thread{
    Account account;//账户
    //取了多少钱
    int drawingMoney;
    //现在手里有多少钱
    int nowMoney;

    public Drawing(Account account,int drawingMoney,String name){
        super(name);
        this.account  = account;
        this.drawingMoney = drawingMoney;
    }

    //取钱
//synchronized默认锁的是它本身
    @Override
    public  void run() {
        //锁的对象指需要变化的量,需要增删改的
        synchronized (account){
        //判断有没有钱
        if (account.money - drawingMoney < 0) {
            System.out.println(Thread.currentThread().getName()+"钱不够取不了");
            return;
        }
        //sleep可以放大问题的安全性
        try {
            Thread.sleep(100);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        //卡内余额 = 余额 - 你取的钱
        account.money = account.money - drawingMoney;
        //你手里的钱
        nowMoney = nowMoney + drawingMoney;
        System.out.println(account.name+"余额为"+account.money);
        //Thread.currentThread().getName() = this.getName()
        System.out.println(this.getName()+"手里的钱"+nowMoney);
    }
}
}
```

* 修改后的代码3

```java
public class UnsafeList {
    public static void main(String[] args) {
        List<String> list = new ArrayList<String>();
        for (int i = 0; i < 10000; i++) {
            new Thread(()->{
                synchronized (list){
                    list.add(Thread.currentThread().getName());}
            }).start();
        }
        try {
            Thread.sleep(3000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        System.out.println(list.size());
    }
}
```

***

## 死锁

### 多个线程各自占有一些共享资源,并且互相等待其他线程占有的资源才能运行,而导致两个或者多个线程都在等待对方释放资源,都停止执行的情形,某一个同步块同时拥有"**两个以上对象的锁**"时,就可能发生死锁问题

1. 产生死锁的四个必要条件:

* 互斥条件:一个资源每次只能被一个进程使用
* 请求与保持条件:一个进程因请求资源而阻塞时,对已获得的资源保持不放
* 不剥夺条件:进程已获得的资源,在未使用完之前,不能强行剥夺
* 循环等待条件:若干进程之间形成一种头尾相接的循环等待资源关系

   **只要避免产生死锁中的一个或多个条件就可以避免死锁发生**

```java
//多个线程互相抱着对方需要的资源,然后形成僵持
public class TestLock {
    public static void main(String[] args) {
        MakeUp g1 = new MakeUp(0,"灰姑娘");
        MakeUp g2 = new MakeUp(0,"白雪公主");

        g1.start();
        g2.start();
    }
}
//口红
class Lipstick{

}

//镜子
class Mirror{

}

//化妆
class MakeUp extends Thread{

    //需要资源只有一份,所以用static来保证只有一份资源
    static Lipstick lipstick= new Lipstick();
    static Mirror mirror= new Mirror();

    int choose;//选择
    String girlName;//人

    public MakeUp(int choose, String girlName) {
        this.choose = choose;
        this.girlName = girlName;
    }

    @Override
    public void run() {
        try {
            makeup();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    private void makeup() throws Exception{
        if (choose == 0) {
            synchronized (lipstick){//获得口红的锁
                System.out.println(this.girlName+("获得口红的锁"));
                Thread.sleep(1000);
                }
                synchronized (mirror){//一秒钟后想要获得镜子的锁
                    System.out.println(this.girlName+"获得镜子的锁");
                }
            }else{
            synchronized (mirror){//获得镜子的锁
                System.out.println(this.girlName+("获得口红的锁"));
                Thread.sleep(1000);
            }
            synchronized (lipstick){//一秒钟后想要获得口红的锁
                System.out.println(this.girlName+"获得镜子的锁");
            }
        }
    }

}
```

***

## Lock锁

* java提供了更强大的线程同步机制--通过显示定义同步锁对象来实现同步,同步锁用Lock对象来充当.
* **java.util.concurrent.locks.Lock**接口是控制多个线程对共享资源进行访问的工具.锁提供了对共享资源的独占访问,每次只能有一个线程对Lock对象加锁,线程开始访问共享资源之前应先获得Lock对象
* **`ReentrantLock (可重入锁)`** 类实现了Lock,它拥有与 **`synchronized`** 相同的并发性和内存语义,在实现线程安全的控制中,比较常用的是 ReentrantLock ,可以显示加锁,释放锁

```java
//测试Lock锁
public class TestLock {
    public static void main(String[] args) {
        LockTwo l = new LockTwo();
        new Thread(l).start();
        new Thread(l).start();
        new Thread(l).start();
    }

}

class LockTwo implements Runnable{

    int ticketNums = 10;

    //定义Lock锁
    private final ReentrantLock lock = new ReentrantLock();

    @Override
    public void run() {
        while (true){
            try {
                //加锁
                lock.lock();
                if (ticketNums > 0) {
                    try {
                        Thread.sleep(100);
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                    System.out.println(ticketNums--);
                }else {
                    break;
                }
            }finally {
                //解锁
                lock.unlock();
                //如果代码同步有异常,要将unlock()写入finally语句块
                }

        }
    }
}
```

***

`synchronized` 与 `Lock`的对比

* Lock 是显示锁(手动开启和关闭锁,**别忘记关闭锁**), synchronized 是隐式锁,出了作用域自动释放.
* Lock只有代码块锁, synchronized 有代码块锁和方法锁.
* 使用Lock锁,JVM将花费较少的时间来调度线程,性能更好,并且具有更好的扩展性(提供更多的子类)
* 优先使用顺序:  
  **Lock > 同步代码块(已经进入方法体,分配了相应资源) > 同步方法(在方法体之外)**

***  

### 生产者与消费者问题笔记

#### 管程法

```java
//测试:生产者消费者模型-->利用缓冲区解决:管程法

//生产者,消费者,产品, 缓冲区
public class TestPC {
    public static void main(String[] args) {
        SynContainer container = new SynContainer();

        new Productor(container).start();
        new Consumer(container).start();
    }

}

//生产者
class Productor extends Thread{
    SynContainer container;

    public Productor(SynContainer container) {
        this.container = container;
    }
    //生产

    @Override
    public void run() {
        for (int i = 0; i < 100; i++) {
            container.push(new Chicken(i));
            System.out.println("生产了"+i+"只鸡");
        }
    }
}
//消费者
class Consumer extends Thread{
    SynContainer container;

    public Consumer(SynContainer container) {
        this.container = container;
    }

    @Override
    public void run() {
        for (int i = 0; i < 100; i++) {
            System.out.println("消费了===>"+container.pop().id+"只鸡");
        }
    }
}

//产品
class Chicken{
    int id; //产品编号

    public Chicken(int id) {
        this.id = id;
    }
}

//缓冲区
class SynContainer{

    Chicken[] chickens = new Chicken[10];
    //容器计数器
    int count = 0;
    //需要一个容器大小

    //生产者放入产品
    public synchronized void push(Chicken chicken){
        //如果容器满了就需要等待消费者消费
        if (count == chickens.length) {
            //通知消费者消费,生产等待
            try {
                this.wait();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }

        //如果没有满就需要丢入产品
        chickens[count] = chicken;
        count++;

        //可以通知消费者消费了
        this.notifyAll();
    }
    //消费者消费产品
    public synchronized Chicken pop(){
        //判断能否消费
        if (count == 0) {
            //等待生产者生产,消费者等待
            try {
                this.wait();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
        //如果可以消费
        count--;
        Chicken chicken = chickens[count];

        //吃完了 通知生产者生产
        this.notifyAll();
        return chicken;
    }
}
```

#### 信号灯法

```java
//测试生产者消费者问题2:信号灯法,标志位解决
public class TestPcTwo {

    public static void main(String[] args) {
        TV tv = new TV();
        new Player(tv).start();
        new Watcher(tv).start();
    }
}


//生产者--演员
class Player extends Thread{
    TV tv;
    public Player(TV tv){
        this.tv = tv;
    }

    @Override
    public void run() {
        for (int i = 0; i < 20; i++) {
            if (i % 2 == 0) {
                this.tv.player("快乐大本营播放着");
            }else {
                this.tv.player("抖音记录美好生活");
            }
        }
    }
}

//消费者--观众
class Watcher extends Thread{
    TV tv;
    public Watcher(TV tv){
        this.tv = tv;
    }

    @Override
    public void run() {
        for (int i = 0; i < 20; i++) {
            tv.watch();
        }
    }
}

//产品--节目
class TV{

    //演员表演,观众等待   t
    //观众观看,演员等待   f
    String voice;//表演的节目
    boolean flag = true;
    //演员表演
    public synchronized void player(String voice){
        if (!flag){
            try {
                this.wait();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
        System.out.println("演员表演了"+voice);
        //通知观众观看
        this.notifyAll();//通知唤醒
        this.voice = voice;
        this.flag = !this.flag;
    }
    //观众观看
    public synchronized void watch(){
        if (flag) {
            try {
                this.wait();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
        System.out.println("观看了"+voice);
        //通知演员表演
        this.notifyAll();
        this.flag = !this.flag;
    }
}
```

***
