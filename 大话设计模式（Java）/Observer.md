```java
/**
 * 抽象观察者
 */
public abstract class Observer {

    public abstract void update();
}





import java.util.ArrayList;
import java.util.List;

/**
 * 主题或抽象通知者
 */
public abstract class Subject {
    private List<Observer> observers = new ArrayList<Observer>();

    public void attach(Observer observer) {
	observers.add(observer);
    }

    public void detach(Observer observer) {
	observers.remove(observer);
    }

    public void notifyObserver() {
	for (Observer observer : observers) {
	    observer.update();
	}
    }
}



/**
 * 具体主题或通知者
 */
public class ConcreteSubject extends Subject {
    private String subjectState;

    public String getSubjectState() {
	return subjectState;
    }

    public void setSubjectState(String subjectState) {
	this.subjectState = subjectState;
    }
}


/**
 * 具体观察者
 */
public class ConcreteObserver extends Observer {

    private String name;
    private String observerState;
    private ConcreteSubject concreteSubject;

    public ConcreteObserver(ConcreteSubject concreteSubject, String name) {
	this.setName(name);
	this.setConcreteSubject(concreteSubject);
    }

    @Override
    public void update() {
	this.setObserverState(concreteSubject.getSubjectState());
	System.out.println("观察者" + this.getName() + "的新状态是"
		+ this.getObserverState());
    }

    public String getName() {
	return name;
    }

    public void setName(String name) {
	this.name = name;
    }

    public String getObserverState() {
	return observerState;
    }

    public void setObserverState(String observerState) {
	this.observerState = observerState;
    }

    public ConcreteSubject getConcreteSubject() {
	return concreteSubject;
    }

    public void setConcreteSubject(ConcreteSubject concreteSubject) {
	this.concreteSubject = concreteSubject;
    }

}




/**
 * 观察者模式客户端代码
 */
public class ObserverClient {
    public static void main(String[] args) {
	ConcreteSubject concreteSubject = new ConcreteSubject();

	concreteSubject.attach(new ConcreteObserver(concreteSubject, "X"));
	concreteSubject.attach(new ConcreteObserver(concreteSubject, "Y"));
	concreteSubject.attach(new ConcreteObserver(concreteSubject, "Z"));

	concreteSubject.setSubjectState("ABC");
	concreteSubject.notifyObserver();

    }

}
```
