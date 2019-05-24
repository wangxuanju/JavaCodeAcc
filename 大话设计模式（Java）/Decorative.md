# 装饰模式
装饰模式：动态地给一个对象添加一些额外的职责，就增加功能来说，装饰模式比生成子类更加灵活。<br>
装饰模式是为已有功能动态地添加更多功能的一种方式。当系统需要新功能的时候，是向旧有的类添加新的代码。这些新加的代码通常装饰了原有类的核心职责或主要行为。在主类中加入了新的字段，新的方法和新的逻辑，从而增加了主类的复杂度，而这些新加入的东西仅仅是为了满足一些只在某种特定的情况下才会执行的特殊行为的需要。而装饰模式却提供了一个非常好的解决方案，它把每个要装饰的功能放在单独的类中，并让这个类包装它所要装饰的对象，因此，当需要执行特殊行为时，客户代码就可以在运行时根据需要有选择地、按顺序地使用装饰功能包装对象了。
装饰模式的优点，是把类中的装饰功能从类中搬移去除，这样可以简化原有的类。这样做最大的好处就是有效的把类的职责和装饰功能区分开了。而且可以去除相关中重复的装饰逻辑。
```java
/**
 * Component是定义一个对象接口，可以给这些对象动态地添加职责
*/
public abstract class Component {
    public abstract void operation();
}


/**
 * ConcreteComponent是定义一个具体的对象，也可以给这个对象添加一些职责
*/
public class ConcreteComponent extends Component {

    @Override
    public void operation() {
	System.out.println("具体对象的操作");
    }

}


/**Decorator，装饰抽象类，继承了Component，从外类来扩展Component类的功能，但对于Component来说，是无需知道Decorator的存在的*/
public abstract class Decorator extends Component {
    protected Component component;

    public Component getComponent() {
	return component;
    }

    public void setComponent(Component component) {
	this.component = component;
    }

    @Override
    public void operation() {
	if (component != null) {
	    component.operation();
	}
    }

}
/*至于ConcreteDecorator就是具体的装饰对象，起到给Component添加职责的功能*/
class ConcreteDecoratorA extends Decorator {
    private String addedState;

    @Override
    public void operation() {
	// 首先运行原Component的operation()，再执行本类的功能，如addedState，相当于对原Component进行了装饰
	super.operation();
	addedState = "A中的new state ";
	System.out.println(addedState + "具体装饰对象A的操作");
    }
}

class ConcreteDecoratorB extends Decorator {
    @Override
    public void operation() {
	super.operation();
	addedBehavior();
	System.out.println("具体装饰对象B的操作");
    }

    public void addedBehavior() {
	System.out.print("B中的新增行为 ");
    }
}

class ConcreteDecoratorC extends Decorator {
    @Override
    public void operation() {
	super.operation();
	System.out.println("C没有特殊行为 " + "具体装饰对象C的操作");
    }

}


/**装饰模式客户端调用代码，装饰的过程更像是层层包装，用前面的对象装饰后面的对象
 */
public class DecoratorClient {
    public static void main(String[] args) {
	ConcreteComponent concreteComponent = new ConcreteComponent();
	ConcreteDecoratorA concreteDecoratorA = new ConcreteDecoratorA();//深入理解（引用了抽象父类的方法）
	ConcreteDecoratorB concreteDecoratorB = new ConcreteDecoratorB();
	ConcreteDecoratorC concreteDecoratorC = new ConcreteDecoratorC();

	concreteDecoratorA.setComponent(concreteComponent);
	concreteDecoratorB.setComponent(concreteDecoratorA);
	concreteDecoratorC.setComponent(concreteDecoratorB);
	concreteDecoratorC.operation();

    }
}
```
