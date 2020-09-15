#### java序列化机制

---

在Java的世界里，创建好对象之后，只要需要，对象是可以长驻内存，但是在程序终止时，所有对象还是会被销毁。这其实很合理，但是即使合理也不一定能满足所有场景，仍然存在着一些情况，需要能够在程序不运行的情况下保持对象，所以序列化机制应运而生。

- RPC框架的数据传输；
- 对象状态的持久化保存；

也许你会觉得，要达到这种持久化的效果，我们直接将信息写入文件或数据库也可以实现啊，为什么还要序列化？这是一个好问题，试想如果我们采用前面所述的方法，在序列化对象和反序列化恢复对象时，我们必须考虑如何完整的保存和恢复对象的信息，这里面会涉及到很多繁琐的细节，稍加不注意就可能导致信息的丢失。如果能够有一种机制，只要将一个对象声明为是“持久性”的，就能够为我们处理掉所有细节，这样岂不是很方便，这就是序列化要做的事情。Java已经将序列化的概念加入到语言中，本文的关于序列化的所有例子都是基于Java的。

Java提供的原生序列化机制功能强大，有其自己的一些特点：



- 序列化处理非常简单，只需将对象实现Serializable接口即可；

- 能够自动弥补不同操作系统之间的差异，即可以在运行Windows系统的计算机上创建一个对象，将其序列化，然后通过网络将它发送给一台运行Unix系统的计算机，然后在那里准确地重新组装，不必担心数据在新的机器上表示会不同；

- 对象序列化不仅会保存对象的“全景图”，而且能够追踪对象内所包含的所有引用，并保存那些对象；接着又能对对象内包含的每个这样的引用进行追踪，依此类推；

- 对象序列化保存的是对象的”状态”，即它的成员变量，所以对象序列化并不会处理类中的静态变量；

## 2. 序列化机制的使用

　　Java的对象序列化机制是将那些实现了Serializable接口的对象转换成一个字节序列，并能够在以后将这个字节序列完全恢复为原来的对象。

　　要序列化一个对象，首先要创建一个OutputStream对象，然后将其封装在一个ObjectOutputStream对象内，接着只需调用writeObject()方法即可将对象序列化，并将序列化后的字节序列发送给OutputStream。要将一个序列还原为一个对象，则需要将一个InputStream封装在ObjectInputStream内，然后调用readObject()，该方法会返回一个引用，它指向一个向上转型的Object，必须向下转型才能直接使用。

　　我们来看一个例子，如何序列化和反序列化对象。

```java
public class Worm implements Serializable{
    private static Random rand = new Random(47);
    private Data[] d = {
        new Data(rand.nextInt(10)),
        new Data(rand.nextInt(10)),
        new Data(rand.nextInt(10))
    };
    private Worm next;
    private char c;
    public Worm(int i, char x){
        System.out.println("Worm constructor: " + i);
        c = x;
        if(--i > 0){
            next = new Worm(i,(char)(x + 1));
        }
    }
    public Worm(){
        System.out.println("Default constructor");
    }
    public String toString(){
        StringBuilder result = new StringBuilder(":");
        result.append(c);
        result.append("(");
        for(Data dat : d){
            result.append(dat);
        }
        result.append(")");
        if(next != null){
            result.append(next);
        }
        return result.toString();
    }
    public static void main(String[] args) throws ClassNotFoundException, IOException{
        Worm w = new Worm(6,'a');
        System.out.println("w = " + w);
        ObjectOutputStream out = new ObjectOutputStream(new FileOutputStream("worm.out"));
        out.writeObject("Worm storage\n");
        out.writeObject(w);
        out.close();
        ObjectInputStream in = new ObjectInputStream(new FileInputStream("worm.out"));
        String s = (String)in.readObject();
        Worm w2 = (Worm)in.readObject();
        System.out.println(s + "w2 = " + w2);
        ByteArrayOutputStream bout = new ByteArrayOutputStream();
        ObjectOutputStream out2 = new ObjectOutputStream(bout);
        out2.writeObject("Worm storage\n");
        out2.writeObject(w);
        out2.flush();
        ObjectInputStream in2 = new ObjectInputStream(new ByteArrayInputStream(bout.toByteArray()));
        s = (String)in2.readObject();
        Worm w3 = (Worm)in2.readObject();
        System.out.println(s + "w3 = " + w3);
    }
}

class Data implements Serializable{
    private int n;
    public Data(int n){this.n = n;}
    public String toString(){return Integer.toString(n);}
}
```

输出结果如下：

```
Worm constructor: 6
Worm constructor: 5
Worm constructor: 4
Worm constructor: 3
Worm constructor: 2
Worm constructor: 1
w = :a(853):b(119):c(802):d(788):e(199):f(881)
Worm storage
w2 = :a(853):b(119):c(802):d(788):e(199):f(881)
Worm storage
w3 = :a(853):b(119):c(802):d(788):e(199):f(881)
```

　　这段代码通过对链接的对象生成一个worm(蠕虫)对序列化机制进行测试，每个对象都与worm中的下一段链接，同时又与属于不同类(Data)的对象引用数组链接。

　　对象序列化不仅保存了对象的“全景图”，而且能追踪对象内所包含的所有引用，并保存那些对象；还能对对象内包含的每个这样的引用进行追踪；依此类推。

　　而且从上面的输出结果还可以看出一个Serializable对象进行还原的过程中，没有调用任何构造器，包括默认的构造器。整个对象都是通过从InputStream中取得数据恢复而来的。

## 3. 序列化需要什么

　　前面我们有说到序列化的目的之一是支持rpc框架的数据传输，比如我们将一个对象序列化，并通过网络将其传给另一台计算机，另一台计算机通过反序列化来还原这个对象，那是否只需要该序列化文件就能还原对象呢？我们用下面的代码来测试一下。

```java
public class Serialize implements Serializable{}
}

public class FreezeSerialize {
    public static void main(String[] args) throws Exception{
        ObjectOutputStream os = new ObjectOutputStream(new FileOutputStream("X.file"));
        Serialize serialize = new Serialize();
        os.writeObject(alien);
    }
}

public class ThawSerialize {
    public static void main(String[] args) throws Exception{
        ObjectInputStream in = new ObjectInputStream(new FileInputStream("X.file"));
        Object mystery = in.readObject();
        System.out.println(mystery.getClass());
    }
}
```

　　FreezeSerialize类用来把对象序列化到文件中，ThawSerialize类用来反序列化对象，在测试电脑上如果同时执行这两个类是没有问题的，但如果我们将Serialize类的位置更改一下(或者直接将FreezeSerialize和Serialize删掉)，则执行ThawSerialize反序列化时会报错误--ClassNotFoundException，所以可以知道，反序列化时是需要原对象的Class对象的。

　　既然反序列化时需要对应的Class对象，那如果序列化时和反序列化时对应的Class版本不一样会怎么样呢(这种情况是存在的)？为了模拟这种情况，我们先执行FreezeSerialize类的main方法，再给Serialize类添加一个属性，这时再跑一下ThawSerialize类的main方法，可以发现报java.io.InvalidClassException异常，明明是能通过编译的但是却报错了，这种情况有没有什么办法解决呢？有的，我们可以给实现了Serializable接口的类添加一个long类型的成员：serialVersionUID，修饰符为private static final，并且指定一个随机数即可。

　　这个serialVersionUID其实叫序列化版本号，如果不指定的话，编译器会在编译后的class文件中默认添加一个，其值是根据当前类结构生成。但是这样会带来一个问题，如果类的结构发生了改变，那编译之后对应的版本号也会发生改变，**而虚拟机是否允许反序列化，不仅取决于类路径和功能代码是否一致，还有一个非常重要的一点是两个类的序列化ID是否一致**，如果不一致则不允许序列化并且会抛出InvalidClassException异常，这就是前面不添加序列号时更改类结构再反序列化时会报错的原因。所以建议给实现了Serializable接口的类添加一个序列化版本号serialVersionUID，并指定值。

　　关于序列化版本号还有一个点需要主意，版本号一致的情况下，若待反序列化的对象与当前类现有结构不一致时，则采用兼容模式，即：该对象的属性现有类有的则还原，没有的则忽略。

## 4. 序列化控制

　　上面我们我们使用的是Java提供的默认序列化机制，即将对象成员全部序列化。但是，如果有特殊的需要呢？比如，只希望对象的某一部分被序列化。在这种特殊情况下，可以通过若干种方法来实现想要的效果，下面一一介绍。

### 4.1 实现Externalizable接口

　　通过实现Externalizable接口(代替实现Serializable)，可以对序列化过程进行控制。这个Externalizable接口继承了Serializable接口，同时增加了两个方法：writeExternal()和readExternal()。这两个方法会分别在序列化和反序列化还原的过程中被自动调用，这样就可以在这两个方法种指定执行一些特殊操作。下面来看一个简单例子：

```java
public class Blip implements Externalizable{
    private int i;
    private String s;
    public Blip(){
        System.out.println("Blip Constructor");
    }
    public Blip(String x, int a){
        System.out.println("Blip(String x, int a)");
        s = x;
        i = a;
    }
    public String toString(){
        return s + i;
    }
    public void writeExternal(ObjectOutput out) throws IOException{
        System.out.println("Blip.writeExternal");
        out.writeObject(s);
        out.writeInt(i);
    }
    public void readExternal(ObjectInput in) throws IOException, ClassNotFoundException{
        System.out.println("Blip.readExternal");
        s = (String)in.readObject();
        i = in.readInt();
    }
    public static void main(String[] args) throws IOException, ClassNotFoundException{
        System.out.println("Constructing objects:");
        Blip b = new Blip("A String ",47);
        System.out.println(b);
        // 序列化对象
        ObjectOutputStream o = new ObjectOutputStream(new FileOutputStream("Blip.out"));
        System.out.println("Saving object:");
        o.writeObject(b);
        o.close();
        // 还原对象
        ObjectInputStream in = new ObjectInputStream(new FileInputStream("Blip.out"));
        System.out.println("Recovering b:");
        b = (Blip)in.readObject();
        System.out.println(b);
    } 
}
```

　　在这个例子中，对象继承了Externalizable接口，成员s和i只在第二个构造器中初始化(而不是默认构造器)，我们在writeExternal()方法中对要序列化保存的成员执行写入操作，在readExternal()方法中将其恢复。输出结果如下：

```
Blip(String x, int a)
A String 47
Saving object:
Blip.writeExternal
Recovering b:
Blip Constructor
Blip.readExternal
A String 47
```

这里需要注意的几个点：

1. 对象实现了Externalizable之后，没有任何成员可以自动序列化，需要在writeExternal()内部只对所需部分进行显式的序列化，并且在readExternal()方法中将其恢复。
2. 在将实现了Externalizable接口的对象进行反序列化操作时，会调用其默认构造函数，如果没有，则会报错java.io.InvalidClassException。所以如果对象实现了Externalizable接口，则还需要检查其是否有默认构造函数。

### 4.2 transient(瞬时)关键字

　　在我们对序列化进行控制时，可能会碰到某个特定子对象不想让Java的序列化机制自动保存与恢复。比如一些敏感信息(密码)，即使对象中的这些成员是由private修饰，一经序列化处理，通过读取文件或者网络抓包的方式还是能访问到它。

　　前面说的通过实现Externalizable接口可以解决这个问题，但是假如对象有很多的成员，而我们只希望其中少量成员不被序列化，那通过实现Externalizable接口的方式就不合适了(因为需要在writeExternal()方法中做大量工作)，这种情况下，transient关键就可以大显身手了。在实现了Serializable接口的类中，被transient关键字修饰的成员是不会被序列化的。而且，由于Externalizable对象在默认情况下不会序列化对象的任何字段，transient关键字只能和Serializable对象一起使用。

##  总结

　　序列化的出现给保存程序运行状态提供了一种新的途径，实际主要使用在RPC框架的数据传输以及对象状态的持久化保存等场景。

- 要将对象进行序列化处理，只需要实现Serializable接口，然后通过ObjectOutputStream的writeObject()方法即可完成对象的序列化；

- 在某个类实现了Serializable接口之后，为了保证能够成功反序列化，通常建议再添加一个序列化版本号serialVersionUID，并指定值；

- 实现Serializable接口只能使用Java提供的默认序列化机制(即将对象所有部分序列化)，若想自定义序列化过程，有如下三种方式： 

1. 实现Externalizable接口，并实现writeExternal()和readExternal()方法； 
2. 用transient修饰不希望被序列化的成员； 
3. 在类中添加名为writeObject()和readObject()的方法，在其中指定自己的逻辑；

- 实现Externalizable接口之后，没有任何成员可以自动序列化，需要在writeExternal()内部只对所需部分进行显式的序列化，并且在readExternal()方法中将其恢复；

- 在对实现了Serializable接口的类进行反序列化的过程中不会调用任何构造函数，而对实现了Externalizable接口的类进行反序列化时会调用其默认构造函数，如果没有默认构造函数，则会报java.io.InvalidClassException错误；