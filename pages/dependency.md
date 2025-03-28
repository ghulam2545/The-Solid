### Dependency Inversion Principle (DIP)
- **High-level components should rely on abstractions, or interfaces, instead of low-level components.**

_This principle helps us to write loosely coupled code, and it states that we should prefer abstraction and interface instead directly injecting dependency at low level._

```java
// ************************** BAD CODE ************************** //
class SendSMSService {
    public void sendSMS(String customerID) {
        System.out.println("Sending alert to: " + customerID);
    }
}

class CustomerService {
    private String customerID;
    private SendSMSService sendSMSService;

    public CustomerService(String customerID) {
        this.customerID = customerID;
        this.sendSMSService = new SendSMSService(); // BAD: Tight coupling
    }

    public void sendAlert() {
        sendSMSService.sendSMS(customerID);
    }
}

public class Main {
    public static void main(String[] args) {
        CustomerService customerService = new CustomerService("1234567890");
        customerService.sendAlert();
    }
}
```

_Below code rely on abstraction, so let suppose if bank decided to send notification via emails, then don't need to change implementation logic of customer service just provide our new notifier._

```java
class App {}
```

[Home](../README.md)