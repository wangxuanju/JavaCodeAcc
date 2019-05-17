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
