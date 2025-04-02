# JAVA-EXCEPTIONS-ASSISGNEMENT
### 1.` Difference between Checked and Unchecked Exceptions in Java:`
- Checked Exceptions: These are exceptions that are checked at compile time. The programmer must handle these 
 exceptions using a `try-catch` block or by declaring them with the `throws` keyword. Examples include:

  - `IOException:` Occurs when there is an issue with input/output operations (e.g., reading a file that doesn't exist).

  - `SQLException:` Occurs during database access errors.
    
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
