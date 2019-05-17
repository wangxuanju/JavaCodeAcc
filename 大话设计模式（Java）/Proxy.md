```java
/** 定义真实实体类与代理类共用的接口*/
public interface Subject {
    public void request();
}

/** 真实实体类*/
public class RealSubject implements Subject {

    @Override
    public void request() {
	System.out.println("真实对象的请求");
    }

}

/** 代理类*/
public class Proxy implements Subject {

    // 保存一个引用，使得代理可以访问真实实体
    Subject subject;

    public Proxy() {
	subject = new RealSubject();
    }

    @Override
    public void request() {
	subject.request();
    }

}

/**代理客户端*/
public class ProxyClient {
    public static void main(String[] args) {
	Proxy proxy = new Proxy();
	proxy.request();
    }
}
```
