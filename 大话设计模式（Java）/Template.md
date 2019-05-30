模板方法模式
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
