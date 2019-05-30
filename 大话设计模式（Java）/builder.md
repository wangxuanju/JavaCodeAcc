```java
public abstract class Builder {
    public abstract void buildPartA();

    public abstract void buildPartB();

    public abstract Product getBuildResult();
}


public class Product {
    List<String> parts = new ArrayList<String>();

    // 添加产品部件
    public void add(String part) {
	parts.add(part);
    }

    // 列举所有的产品部件
    public void show() {
	System.out.println("---产品 创建---");

	for (String part : parts) {
	    System.out.println(part);
	}
    }
}


/**
 * 具体建造者类
 *
 */
public class ConcreteBuilder1 extends Builder {

    private Product product = new Product();

    @Override
    public void buildPartA() {
	product.add("部件A");
    }

    @Override
    public void buildPartB() {
	product.add("部件B");
    }

    @Override
    public Product getBuildResult() {
	return product;
    }

}



/**
 * 具体建造者类，建造的对象时Product，通过build使Product完善
 *
 */
public class ConcreteBuilder2 extends Builder {

    private Product product = new Product();

    @Override
    public void buildPartA() {
	product.add("部件X");
    }

    @Override
    public void buildPartB() {
	product.add("部件Y");
    }

    @Override
    public Product getBuildResult() {
	return product;
    }

}


/**
 * 指挥者类，用来指挥建造过程
 */
public class Director {

    public void construct(Builder builder) {
	builder.buildPartA();
	builder.buildPartB();
    }
}


/**
 * 建造客户端
 *
 */
public class BuilderClient {

    public static void main(String[] args) {
	Director director = new Director();
	Builder builder1 = new ConcreteBuilder1();
	Builder builder2 = new ConcreteBuilder2();

	director.construct(builder1);
	Product product1 = builder1.getBuildResult();
	product1.show();

	director.construct(builder2);
	Product product2 = builder2.getBuildResult();
	product2.show();

    }

}
```
