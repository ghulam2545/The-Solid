### Open/Closed Principle (OCP)
- **Software entities (classes, modules, functions, etc.) should be open for extension but closed for modification.** OR
- **You should be able to extend a class's behavior without modifying it.**

_todo_

```java
class CardIssuer {
    public void issueCard(String cardKind) {
        if ("CREDIT_CARD".equals(cardKind)) {
            System.out.println("Issuing card: " + cardKind);
        } else if ("DEBIT_CARD".equals(cardKind)) {
            System.out.println("Issuing card: " + cardKind);
        } else {
            System.out.println("Invalid card: " + cardKind);
        }
    }
}

public class Main {
    public static void main(String[] args) {
        CardIssuer issuer = new CardIssuer();
        issuer.issueCard("CREDIT_CARD");
        issuer.issueCard("DEBIT_CARD");
        issuer.issueCard("XYZ");
    }
}
```

_todo_

```java
interface CardKind {
    void issueCard();
}

class CreditCard implements CardKind {
    @Override
    public void issueCard() {
        System.out.println("Issuing Credit Card");
    }
}

class DebitCard implements CardKind {
    @Override
    public void issueCard() {
        System.out.println("Issuing Debit Card");
    }
}

// PrepaidCard (New addition)
class PrepaidCard implements CardKind {
    @Override
    public void issueCard() {
        System.out.println("Issuing Prepaid Card");
    }
}

class CardIssuer {
    public void issue(CardKind card) {
        card.issueCard();
    }
}

public class Main {
    public static void main(String[] args) {
        CardIssuer issuer = new CardIssuer();

        issuer.issue(new CreditCard());
        issuer.issue(new DebitCard());
        issuer.issue(new PrepaidCard()); // New card type added without modifying existing code
    }
}
```

[Home](../README.md)