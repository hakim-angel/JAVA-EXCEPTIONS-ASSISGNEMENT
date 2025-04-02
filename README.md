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
### 6. Explanation of the Given Code

```
public class Test { 
    public static void main(String[] args) { 
        try { 
            System.out.println(10 / 0); 
        } finally { 
            System.out.println("Inside finally block"); 
        } 
    } 
}
```

#### Explanation:

  - The line `System.out.println(10 / 0);` attempts to divide `10 `by` 0`, which causes an `ArithmeticException` (i.e., "Division by zero").

  - In spite of the absence of a `catch` block to trap the exception, the `finally` block will be executed since it gets executed regardless of exceptions occurring.

  - After the execution of the `finally` block, the program will terminate running due to the uncaught exception.
#### Output:
```
Inside finally block
Exception in thread "main" java.lang.ArithmeticException: / by zero
```
The program prints "Inside finally block" from the `finally` block, followed by the exception details from the unhandled `ArithmeticException`.
### 7. Java Program: Convert a String to an Integer:
```
public class StringToIntegerConverter {
    public static int convertToInt(String str) {
        try {
            return Integer.parseInt(str);
        } catch (NumberFormatException e) {
            System.out.println("Invalid number: " + str);
            return -1;
        }
    }

    public static void main(String[] args) {
        String validInput = "123";
        String invalidInput = "abc";

        System.out.println("Valid Input: " + convertToInt(validInput)); // Output: 123
        System.out.println("Invalid Input: " + convertToInt(invalidInput)); // Output: -1
    }
}
```
### 8. Java Program: Student Class with Custom Exception:
#### Custom Exception Class:
```
public class InvalidAgeException extends Exception {
    public InvalidAgeException(String message) {
        super(message);
    }
}
```
#### Student Class:
```
public class Student {
    private int age;

    public void setAge(int age) throws InvalidAgeException {
        if (age < 0) {
            throw new InvalidAgeException("Age cannot be negative!");
        }
        this.age = age;
        System.out.println("Age set to: " + age);
    }

    public int getAge() {
        return age;
    }
}
```
#### Testing the Code:

```
public class StudentTest {
    public static void main(String[] args) {
        Student student = new Student();

        try {
            student.setAge(20); // Valid age
            student.setAge(-5); // Invalid age
        } catch (InvalidAgeException e) {
            System.out.println("Exception caught: " + e.getMessage());
        }
    }
}
```
#### Output:
```
Age set to: 20
Exception caught: Age cannot be negative!
```
### 9. Java Program: Handle Division with `ArithmeticException`:
```
import java.util.Scanner;

public class DivisionHandler {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.print("Enter numerator: ");
        int numerator = scanner.nextInt();

        while (true) {
            System.out.print("Enter denominator: ");
            int denominator = scanner.nextInt();

            try {
                int result = numerator / denominator;
                System.out.println("Result: " + result);
                break; // Exit loop if division is successful
            } catch (ArithmeticException e) {
                System.out.println("Cannot divide by zero. Please enter a valid denominator.");
            }
        }

        scanner.close();
    }
}
```
### Sample Input/Output:
```
Enter numerator: 10
Enter denominator: 0
Cannot divide by zero. Please enter a valid denominator.
Enter denominator: 2
Result: 5
```
#### 10. Java Program to Retrieve an Array Element with Exception Handling:

This program retrieves an element from an array based on the index provided by the user and handles `ArrayIndexOutOfBoundsException`.

```
import java.util.Scanner;

public class ArrayElementRetriever {
    public static void main(String[] args) {
        int[] array = {10, 20, 30, 40, 50}; // Sample array
        Scanner scanner = new Scanner(System.in);

        System.out.print("Enter an index: ");
        try {
            int index = scanner.nextInt();
            System.out.println("Element at index " + index + ": " + array[index]);
        } catch (ArrayIndexOutOfBoundsException e) {
            System.out.println("Invalid index! Please enter an index between 0 and " + (array.length - 1));
        }
        scanner.close();
    }
}
```
### 11. Java Method to Validate Email with Exception Handling:
This method checks if the email contains `'@'` and `'.'`. If not, it throws an `IllegalArgumentException`.
```
public class EmailValidator {
    public static void validateEmail(String email) {
        if (email == null || !email.contains("@") || !email.contains(".")) {
            throw new IllegalArgumentException("Invalid email! Email must contain '@' and '.'");
        }
        System.out.println("Valid email: " + email);
    }

    public static void main(String[] args) {
        try {
            validateEmail("example@gmail.com"); // Valid email
            validateEmail("invalidEmail"); // Invalid email
        } catch (IllegalArgumentException e) {
            System.out.println("Exception caught: " + e.getMessage());
        }
    }
}
```
### 12. Java Program to Prompt User for Integer Input and Handle `InputMismatchException`:
This program repeatedly asks the user for an integer input until a valid integer is provided.
```
import java.util.Scanner;

public class IntegerInputHandler {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        while (true) {
            try {
                System.out.print("Enter an integer: ");
                int number = scanner.nextInt();
                System.out.println("You entered: " + number);
                break; // Exit loop if input is valid
            } catch (java.util.InputMismatchException e) {
                System.out.println("Invalid input! Please enter a valid integer.");
                scanner.next(); // Clear the invalid input
            }
        }
        scanner.close();
    }
}
```
### 13. Java Program to Handle Multiple Exceptions

This program demonstrates how to handle `NullPointerException`,` ArithmeticException`, and `ArrayIndexOutOfBoundsException` using multiple catch blocks.
```
public class MultipleCatchBlocks {
    public static void main(String[] args) {
        String str = null; // For NullPointerException
        int[] array = {1, 2, 3}; // For ArrayIndexOutOfBoundsException

        try {
            // Uncomment one line at a time to test each exception
            // int result = 10 / 0; // ArithmeticException
            // System.out.println(str.length()); // NullPointerException
            System.out.println(array[5]); // ArrayIndexOutOfBoundsException
        } catch (ArithmeticException e) {
            System.out.println("ArithmeticException caught: Division by zero is not allowed.");
        } catch (NullPointerException e) {
            System.out.println("NullPointerException caught: You tried to access a null object.");
        } catch (ArrayIndexOutOfBoundsException e) {
            System.out.println("ArrayIndexOutOfBoundsException caught: Invalid array index accessed.");
        }
    }
}
```










