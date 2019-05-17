运算类（抽象类）
public abstract class Operation {
    public double numberA;
    public double numberB;
    public abstract double result();
}

public class OperationAdd extends Operation {

    @Override
    public double result() {
	    return numberA + numberB;
    }
}

public class OperationDiv extends Operation {

    @Override
    public double result() {
	  if (numberB == 0) {
	    throw new RuntimeException("divided by 0");
	  }
	  return numberA / numberB;
    }
}

public class OperationMul extends Operation {

    @Override
    public double result() {
	    return numberA * numberB;
    }
}

public class OperationSub extends Operation {

    @Override
    public double result() {
	return numberA - numberB;
    }
}



/**
 * 操作类工厂类
 *
 */
public class OperationFactory {
    public static Operation createOperation(char operator) {
	Operation operation = null;

	switch (operator) {
	case '+':
	    operation = new OperationAdd();
	    break;
	case '-':
	    operation = new OperationSub();
	    break;
	case '*':
	    operation = new OperationMul();
	    break;
	case '/':
	    operation = new OperationDiv ();
	    break;
	default:
	    throw new RuntimeException ("unsupported operation");
	}

	return operation;
    }
}


/**
 * 使用工厂方法生成实例完成运算操作
*/
public class Calculator {
    public static void main (String[] args) {
	Operation operation ;
	char operator;

	operator = '+';
	operation = OperationFactory.createOperation (operator);
	operation.numberA = 1.2;
	operation.numberB = 2.3;

	System.out.println( operation.result() );
    }
}
