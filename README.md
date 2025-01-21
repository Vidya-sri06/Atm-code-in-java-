import java.util.Scanner;

public class ATM {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        double balance = 1000.00; // Initial balance
        int pin = 1234; // Example PIN
        int attempts = 0;
        final int MAX_ATTEMPTS = 3;

        System.out.println("Welcome to the ATM!");

        // PIN authentication
        while (attempts < MAX_ATTEMPTS) {
            System.out.print("Enter your PIN: ");
            int inputPin = scanner.nextInt();

            if (inputPin == pin) {
                System.out.println("Authentication successful!");
                break;
            } else {
                attempts++;
                System.out.println("Invalid PIN. Attempts remaining: " + (MAX_ATTEMPTS - attempts));
            }

            if (attempts == MAX_ATTEMPTS) {
                System.out.println("Too many failed attempts. Exiting...");
                scanner.close();
                return;
            }
        }

        // Main menu
        while (true) {
            System.out.println("\nATM Menu:");
            System.out.println("1. Check Balance");
            System.out.println("2. Deposit");
            System.out.println("3. Withdraw");
            System.out.println("4. Exit");
            System.out.print("Choose an option: ");
            int choice = scanner.nextInt();

            switch (choice) {
                case 1:
                    System.out.println("Your current balance is: $" + balance);
                    break;

                case 2:
                    System.out.print("Enter amount to deposit: ");
                    double depositAmount = scanner.nextDouble();
                    if (depositAmount > 0) {
                        balance += depositAmount;
                        System.out.println("Successfully deposited $" + depositAmount);
                        System.out.println("Your new balance is: $" + balance);
                    } else {
                        System.out.println("Invalid deposit amount.");
                    }
                    break;

                case 3:
                    System.out.print("Enter amount to withdraw: ");
                    double withdrawAmount = scanner.nextDouble();
                    if (withdrawAmount > 0 && withdrawAmount <= balance) {
                        balance -= withdrawAmount;
                        System.out.println("Successfully withdrew $" + withdrawAmount);
                        System.out.println("Your new balance is: $" + balance);
                    } else if (withdrawAmount > balance) {
                        System.out.println("Insufficient funds.");
                    } else {
                        System.out.println("Invalid withdrawal amount.");
                    }
                    break;

                case 4:
                    System.out.println("Thank you for using the ATM. Goodbye!");
                    scanner.close();
                    return;

                default:
                    System.out.println("Invalid choice. Please try again.");
            }
        }
    }
}
