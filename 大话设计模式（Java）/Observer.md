```java
/**
 * 抽象观察者
 * 
 * @author liu yuning
 *
 */
public abstract class Observer {

    public abstract void update();
}





import java.util.ArrayList;
import java.util.List;

/**
 * 主题或抽象通知者
 * 
 * @author liu yuning
 *
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
 * 
 * @author liu yuning
 *
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
