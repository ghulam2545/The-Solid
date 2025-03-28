### Single Responsibility Principle (SRP)
- **A class should have only one responsibility, or reason to change.**

<br/>
This principle states that a class should have only and only one responsibility to work. It cannot do multiple things in the same class. As below, I have considered a banking system service that is trying to process multiple tasks in the same class, and it violates SRP.
This class is doing too many things, which makes it harder to maintain.

```java
// ************************** BAD CODE ************************** //
class CoreBankingService {
    private String accountNumber;

    public CoreBankingService(String accountNumber) {
        this.accountNumber = accountNumber;
    }

    public void issueLoan() {
        System.out.println("Issuing Loan to: " + accountNumber);
    }

    public void generateReport() {
        System.out.println("Generating report for: " + accountNumber);
    }

    public void sendNotification() {
        System.out.println("Sending notification to: " + accountNumber);
    }
}

public class Main {
    public static void main(String[] args) {
        String accountNumber = "3020034109034";
        CoreBankingService bankingService = new CoreBankingService(accountNumber);

        bankingService.issueLoan();
        bankingService.generateReport();
        bankingService.sendNotification();
    }
}
```

As the principle states that there should be only responsibility, so now we can separate each task in separate class and good code will look like this.
Now each class has a single responsibility and adding new features won’t break existing code.

```java
// ************************** GOOD CODE ************************** //
class LoanService {
    private String accountNumber;

    public LoanService(String accountNumber) {
        this.accountNumber = accountNumber;
    }

    public void issueLoan() {
        System.out.println("Issuing Loan to: " + accountNumber);
    }
}

class ReportService {
    private String accountNumber;

    public ReportService(String accountNumber) {
        this.accountNumber = accountNumber;
    }

    public void generateReport() {
        System.out.println("Generating report for: " + accountNumber);
    }
}

class NotificationService {
    private String accountNumber;

    public NotificationService(String accountNumber) {
        this.accountNumber = accountNumber;
    }

    public void sendNotification() {
        System.out.println("Sending notification to: " + accountNumber);
    }
}

public class Main {
    public static void main(String[] args) {
        String accountNumber = "3020034109034";

        LoanService loanService = new LoanService(accountNumber);
        ReportService reportService = new ReportService(accountNumber);
        NotificationService notificationService = new NotificationService(accountNumber);

        loanService.issueLoan();
        reportService.generateReport();
        notificationService.sendNotification();
    }
}
```
