

Créer une interface de paiement.


```java
public interface Payment {
    void pay(double amount);
}
```

Implémentation

```java
public class CreditCardPayment implements Payment {
    private String cardNumber;

    public CreditCardPayment(String cardNumber) {
        this.cardNumber = cardNumber;
    }

    @Override
    public void pay(double amount) {
        System.out.println("Paiement de " + amount + "€ par Carte de Crédit. Numéro: " + cardNumber);
    }
}

public class PayPalPayment implements Payment {
    private String email;

    public PayPalPayment(String email) {
        this.email = email;
    }

    @Override
    public void pay(double amount) {
        System.out.println("Paiement de " + amount + "€ via PayPal. Compte: " + email);
    }
}

public class BankTransferPayment implements Payment {
    private String iban;

    public BankTransferPayment(String iban) {
        this.iban = iban;
    }

    @Override
    public void pay(double amount) {
        System.out.println("Paiement de " + amount + "€ par Virement Bancaire. IBAN: " + iban);
    }
}
```


PaymentProcess

```java
public class PaymentProcessor {

    public void processPayment(Payment payment, double amount) {
        payment.pay(amount);
    }
}
```

Main 

```java
public class Main {
    public static void main(String[] args) {
        Payment creditCardPayment = new CreditCardPayment("1234-5678-9012-3456");
        Payment payPalPayment = new PayPalPayment("user@example.com");
        Payment bankTransferPayment = new BankTransferPayment("FR76 1234 5678 9012 3456 7890");

        PaymentProcessor paymentProcessor = new PaymentProcessor();

        paymentProcessor.processPayment(creditCardPayment, 100.0);
        paymentProcessor.processPayment(payPalPayment, 200.0);
        paymentProcessor.processPayment(bankTransferPayment, 300.0);
    }
}
```


