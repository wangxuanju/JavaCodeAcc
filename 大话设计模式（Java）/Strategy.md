```java

/**
 * 策略接口
 *
 */
public interface Strategy {
    public void algorithmInterface();
}

class ConcreteStrategyA implements Strategy {

    @Override
    public void algorithmInterface() {
	System.out.println("策略A的具体算法实现");
    }

}

class ConcreteStrategyB implements Strategy {

    @Override
    public void algorithmInterface() {
	System.out.println("策略B的具体算法实现");
    }

}

class ConcreteStrategyC implements Strategy {

    @Override
    public void algorithmInterface() {
	System.out.println("策略C的具体算法实现");
    }

}



public class Context {
    Strategy strategy;

    public Context(Strategy strategy) {
	this.strategy = strategy;
    }
    /* * 上下文接口 */
public void contextInterface() {
	strategy.algorithmInterface();
    }

}


客户端使用策略
public class StrategyClient {
    public static void main(String[] args) {
	Context context;

	context = new Context(new ConcreteStrategyA());
	context.contextInterface();

	context = new Context(new ConcreteStrategyB());
	context.contextInterface();

	context = new Context(new ConcreteStrategyC());
	context.contextInterface();

    }
}
```
