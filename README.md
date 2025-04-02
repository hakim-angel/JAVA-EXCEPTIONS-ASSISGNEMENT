# JAVA-EXCEPTIONS-ASSISGNEMENT
### 1.` Difference between Checked and Unchecked Exceptions in Java:`
- Checked Exceptions:These are exceptions checked during the compilation of the program. The programmer must handle these exceptions using a `try-catch` block or by specifying the `throws` keyword. Examples include:

  - `IOException:` This occurs if there is a problem with input/output operations (e.g., when trying to read a file that is not available).

  - `SQLException:`  This occurs when there is a problem reading from the database.
    
 #### Example of a Checked Exception:
```
import java.io.File;
import java.io.FileReader;

public class CheckedExample {
    public static void main(String[] args) {
        try {
            File file = new File("nonexistent.txt");
            FileReader fr = new FileReader(file); // FileNotFoundException
        } catch (Exception e) {
            System.out.println("Checked Exception: " + e.getMessage());
        }
    }
}
```
- Unchecked Exceptions: These exceptions are not checked at compile time but occur at runtime. They include programming bugs like logical errors or improper use of an API. Examples include:

  - `ArithmeticException:` E.g., division by zero.

  - `NullPointerException:` Occurs when you try to access a method or field on a null object.

#### Example of an Unchecked Exception:

```
public class UncheckedExample {
    public static void main(String[] args) {
        int a = 10;
        int b = 0;
        int result = a / b; // ArithmeticException
        System.out.println("Result: " + result);
    }
}
```
### 2. `Output and Explanation of the Given Java Code:`

#### Code Review:
```
public class ExceptionTest { 
    public static void main(String[] args) { 
        try { 
            int result = divide(10, 0); 
            System.out.println("Result: " + result); 
        } catch (ArithmeticException e) { 
            System.out.println("Exception caught: " + e.getMessage()); 
        } 
    } 

    public static int divide(int a, int b) throws ArithmeticException { 
        return a / b; 
    } 
}
```
Explanation:

In the `divide` method, the code tries to divide 10 by 0. This throws an `ArithmeticException `("Division by zero").

The exception is thrown, and as there is a `try-catch` block in the `main` method, the exception is caught in the `catch` block.

The message of the exception is retrieved using `e.getMessage()` and printed.

#### Output:
```
Exception caught: / by zero
```
### 3. `Purpose of the finally Block in Java Exception Handling:`
Use of the `finally` Block in Java Exception Handling:

- Function: The `finally` block is utilized to create a portion of code that will invariably execute, no matter if there is an exception or it's being caught. It is normally used for cleaning up activities like closing resources like files or database connections.

- When Does It Run?: The `finally` block runs after the `try` block and any `catch` blocks, if they are present. It runs whether an exception is thrown or caught.

- Can It Be Skipped?: The finally block is very likely to run. It can be skipped in a few extremely unlikely situations:

  - If the program runs off into the weeds by calling `System.exit()`.

  - If the JVM crashes or the power goes out during execution.
 #### Example:
 ```
 public class FinallyExample {
    public static void main(String[] args) {
        try {
            int result = 10 / 0; // This will throw ArithmeticException
        } catch (ArithmeticException e) {
            System.out.println("Exception caught: " + e.getMessage());
        } finally {
            System.out.println("Finally block executed.");
        }
    }
}
```
#### Output:
```
Exception caught: / by zero
Finally block executed.
```
### 4. Role of the `throws` Keyword and Difference from `throw`:

- ### Role of `throws`:

  - It is used in method declarations to specify that a method can throw one or more exceptions.

  - It notifies the method caller about the exceptions that can be thrown.

  - Example: public void myMethod() throws IOException.

- `throw`:

  - It is used inside the method body to throw an exception explicitly.

  - Example: throw new IOException("File not found").

Difference:
| Aspect  | `throws`                                      |  `throw`                                          |
|---------|-----------------------------------------------|---------------------------------------------------|
|Usage    | Declares exception in method signature        | Used to throw an exception explicitly             |
|Location | Appears after method parameters               | Used inside a method or constructor               |
|Purpose  | Notifies the caller about potential exceptions| Creates and propagates the exception              |

#### Example:
```
import java.io.IOException;

public class ThrowsExample {
    public static void main(String[] args) {
        try {
            readFile();
        } catch (IOException e) {
            System.out.println("Exception caught: " + e.getMessage());
        }
    }

    public static void readFile() throws IOException {
        throw new IOException("File not found"); // Explicitly throwing an exception
    }
}
```
#### Output:
```
Exception caught: File not found
```
### 5. Custom Exception Class` InsufficientFundsException` and BankAccount Implementation:

Here is a sample implementation:

#### Custom Exception Class:
```
public class InsufficientFundsException extends Exception {
    public InsufficientFundsException(String message) {
        super(message); // Passes the exception message to the parent class
    }
}
```
#### BankAccount Class:
```
public class BankAccount {
    private double balance;

    public BankAccount(double initialBalance) {
        this.balance = initialBalance;
    }

    public void withdraw(double amount) throws InsufficientFundsException {
        if (amount > balance) {
            throw new InsufficientFundsException("Insufficient funds! Your balance is: " + balance);
        }
        balance -= amount;
        System.out.println("Withdrawal successful. New balance: " + balance);
    }

    public double getBalance() {
        return balance;
    }
}
```
#### Testing the Code:
```
public class BankApplication {
    public static void main(String[] args) {
        BankAccount account = new BankAccount(500.0);

        try {
            account.withdraw(600.0); // Attempting to withdraw more than the balance
        } catch (InsufficientFundsException e) {
            System.out.println("Exception caught: " + e.getMessage());
        }
    }
}
```
#### OUTPUT:
```
Exception caught: Insufficient funds! Your balance is: 500.0
```






