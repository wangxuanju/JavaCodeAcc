# 模板方法模式
 定义一个操作中的算法的骨架，而将一些步骤延迟到子类中。模板方法使得子类可以不改变一个算法的结构即可重定义该算法的某些特定步骤。<br>
 特点：模板方法模式是通过把不变行为搬移到超类，去除子类中的重复代码来体现它的优势。模板方法就是提供了一个很好的代码复用平台。<br>
 当不变的和可变的行为在方法的子类实现中混合在一起的时候，不变的行为就会在子类中重复出现。通过模板方法把这些行为搬移到单一的地方，这样就帮助子类摆脱重复的不变行为的纠缠。
```java
/**
 * 模板方法抽象类：不变的部分给出具体实现，变化的部分封装为抽象方法延迟到子类实现
 */
public abstract class AbstractTemplate {
    public abstract void primitiveOperation1();

    public abstract void primitiveOperation2();

    public void templateMethod() {
	primitiveOperation1();
	primitiveOperation2();
	System.out.println("模板方法结束\n");
    }

}


/**
 * 具体类A
 *
 */
public class ConcreteClassA extends AbstractTemplate {

    @Override
    public void primitiveOperation1() {
	System.out.println("具体类A的方法1实现");
    }

    @Override
    public void primitiveOperation2() {
	System.out.println("具体类A的方法2实现");
    }

}

/**
 * 具体类B
 *
 */
public class ConcreteClassB extends AbstractTemplate {

    @Override
    public void primitiveOperation1() {
	System.out.println("具体类B的方法1实现");
    }

    @Override
    public void primitiveOperation2() {
	System.out.println("具体类B的方法2实现");
    }

}

/**
 * 模板方法客户端
 *
 */
public class TemplateClient {
    public static void main(String[] args) {
	AbstractTemplate abstractTemplate;

	abstractTemplate = new ConcreteClassA();
	abstractTemplate.templateMethod();

	abstractTemplate = new ConcreteClassB();
	abstractTemplate.templateMethod();

    }
}
```
