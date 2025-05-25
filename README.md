import java.util.Scanner;

// Abstract class – Abstraction
abstract class Currency {
    private double rate;
    private String symbol;

    public Currency(double rate, String symbol) {
        this.rate = rate;
        this.symbol = symbol;
    }

    public double getRate() {
        return rate;
    }

    public String getSymbol() {
        return symbol;
    }

    // Method to be overridden – Polymorphism (Overriding)
    public abstract double convert(double amountInUSD);
}

// Subclasses – Inheritance and Method Overriding
class INR extends Currency {
    public INR() {
        super(83.20, "INR");
    }

    @Override
    public double convert(double amountInUSD) {
        return amountInUSD * getRate();
    }
}

class EUR extends Currency {
    public EUR() {
        super(0.92, "EUR");
    }

    @Override
    public double convert(double amountInUSD) {
        return amountInUSD * getRate();
    }
}

class GBP extends Currency {
    public GBP() {
        super(0.79, "GBP");
    }

    @Override
    public double convert(double amountInUSD) {
        return amountInUSD * getRate();
    }
}

// CurrencyConverter – Encapsulation + Overloading
class CurrencyConverter {
    private Currency currency;

    public void setCurrency(Currency currency) {
        this.currency = currency;
    }

    // Method Overloading – version 1
    public void convertAmount(double amount) {
        double result = currency.convert(amount);
        System.out.printf("%.2f USD = %.2f %s\n", amount, result, currency.getSymbol());
    }

    // Method Overloading – version 2 (with different parameter list)
    public void convertAmount(double amount, Currency otherCurrency) {
        double result = otherCurrency.convert(amount);
        System.out.printf("(Overloaded) %.2f USD = %.2f %s\n", amount, result, otherCurrency.getSymbol());
    }
}

// Main class
public class MainApp {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        CurrencyConverter converter = new CurrencyConverter();

        System.out.println("=== OOP Currency Converter ===");
        System.out.println("Convert from USD to:");
        System.out.println("1. INR");
        System.out.println("2. EUR");
        System.out.println("3. GBP");
        System.out.print("Choose an option (1-3): ");
        int choice = scanner.nextInt();

        System.out.print("Enter amount in USD: ");
        double amount = scanner.nextDouble();

        switch (choice) {
            case 1:
                converter.setCurrency(new INR());
                break;
            case 2:
                converter.setCurrency(new EUR());
                break;
            case 3:
                converter.setCurrency(new GBP());
                break;
            default:
                System.out.println("Invalid choice.");
                scanner.close();
                return;
        }

        // Method Overriding in action
        converter.convertAmount(amount);

        // Method Overloading in action – reuse for demo
        System.out.println("Demonstrating overloaded method:");
        converter.convertAmount(amount, new EUR());

        scanner.close();
    }
}
