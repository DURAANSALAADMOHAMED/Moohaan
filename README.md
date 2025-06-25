import java.util.Scanner;

public class EvcPlusApp {
    static int correctPIN = 5858;
    static int balance = 100;
    static String[] transactions = new String[5]; // Array lagu keydiyo 5 transaction
    static int transactionCount = 0;

    public static void main(String[] args) {
        Scanner input = new Scanner(System.in);

        displayUserInfo(); // Method lagu soo bandhigayo user info

        System.out.print("Fadlan gali PIN kaaga: ");
        int enteredPIN = input.nextInt();

        if (enteredPIN != correctPIN) {
            System.out.println("PIN kaaga waa qalad.");
            return;
        }

        boolean running = true;
        while (running) {
            displayMenu();
            int choice = input.nextInt();
            switch (choice) {
                case 1 -> showBalance();
                case 2 -> airtimeMenu(input);
                case 3 -> billPayment(input);
                case 4 -> transferMoney(input);
                case 5 -> showShortReport();
                case 6 -> salaamBank(input);
                case 7 -> settings(input);
                case 8 -> taajService(input);
                case 9 -> {
                    System.out.println("You have exited. Thank you.");
                    running = false;
                }
                default -> System.out.println("Invalid option.");
            }
        }

        input.close();
    }

    static void displayUserInfo() {
        System.out.println("Magaca: Mohamed Nor Mohamed");
        System.out.println("Class: CNS231");
        System.out.println("ID: C6230202");
    }

    static void displayMenu() {
        System.out.println("\n--- EVC Plus ---");
        System.out.println("1 = Itus haraagaaga");
        System.out.println("2 = Kaarka hadalka");
        System.out.println("3 = Bixi biil");
        System.out.println("4 = U wareeji EVC PLUS");
        System.out.println("5 = War bixin kooban");
        System.out.println("6 = Salaam Bank");
        System.out.println("7 = Maareynta");
        System.out.println("8 = Bill Payment (TAAJ)");
        System.out.println("9 = Exit");
        System.out.print("Choose: ");
    }

    static void showBalance() {
        System.out.println("Haraagaaga waa: $" + balance);
    }

    static void recordTransaction(String info) {
        if (transactionCount < transactions.length) {
            transactions[transactionCount++] = info;
        } else {
            // Wareeji transactions haddii ay buuxaan
            for (int i = 1; i < transactions.length; i++) {
                transactions[i - 1] = transactions[i];
            }
            transactions[transactions.length - 1] = info;
        }
    }

    static void airtimeMenu(Scanner input) {
        System.out.println("\n-- Kaarka hadalka --");
        System.out.println("1. Self Airtime");
        System.out.println("2. Friend Airtime");
        System.out.print("Choose: ");
        int option = input.nextInt();
        System.out.print("Fadlan gali lacagta: ");
        int amount = input.nextInt();
        System.out.println("1. Yes\n2. No");
        int confirm = input.nextInt();
        if (confirm == 1) {
            if (amount > balance) {
                System.out.println("Insufficient balance.");
            } else {
                balance -= amount;
                if (option == 1) {
                    System.out.println("You recharged yourself with $" + amount);
                    recordTransaction("Airtime self: $" + amount);
                } else if (option == 2) {
                    System.out.print("Enter friend's number: ");
                    int number = input.nextInt();
                    System.out.println("You sent $" + amount + " to " + number);
                    recordTransaction("Airtime to " + number + ": $" + amount);
                }
                System.out.println("Haraagaaga cusub waa: $" + balance);
            }
        } else {
            System.out.println("Lacag lama dirin.");
        }
    }

    static void billPayment(Scanner input) {
        System.out.println("\n-- Bixi biil --");
        System.out.print("Gali qadarka biilka: ");
        int bill = input.nextInt();
        if (bill > balance) {
            System.out.println("Haraagaaga kuguma filna.");
        } else {
            balance -= bill;
            System.out.println("Waxaad bixisay biil dhan $" + bill);
            recordTransaction("Biil la bixiyay: $" + bill);
        }
    }

    static void transferMoney(Scanner input) {
        System.out.print("Enter receiver number: ");
        int number = input.nextInt();
        System.out.print("Enter amount: ");
        int amount = input.nextInt();
        System.out.println("1. Yes\n2. No");
        int confirm = input.nextInt();
        if (confirm == 1) {
            if (amount > balance) {
                System.out.println("Haraagaaga kuguma filna.");
            } else {
                balance -= amount;
                System.out.println("Waxaad u dirtay $" + amount + " to " + number);
                recordTransaction("Transfer to " + number + ": $" + amount);
                System.out.println("New balance: $" + balance);
            }
        } else {
            System.out.println("Lacag lama dirin.");
        }
    }

    static void showShortReport() {
        System.out.println("\n-- Warbixin kooban --");
        if (transactionCount == 0) {
            System.out.println("Wax kala iibsasho ma jirto.");
        } else {
            for (int i = 0; i < transactionCount; i++) {
                System.out.println((i + 1) + ". " + transactions[i]);
            }
        }
    }

    static void salaamBank(Scanner input) {
        System.out.println("** Salaam Bank options ** (placeholder)");
        // Waxa la dhammaystiri karaa sida ku jirta code-kaaga hore.
    }

    static void settings(Scanner input) {
        System.out.println("\n-- Maareynta --");
        System.out.println("1. Badal PIN");
        int opt = input.nextInt();
        if (opt == 1) {
            System.out.print("Gali PIN cusub: ");
            int pin1 = input.nextInt();
            System.out.print("Confirm PIN: ");
            int pin2 = input.nextInt();
            if (pin1 == pin2 && pin1 >= 1000 && pin1 <= 9999) {
                correctPIN = pin1;
                System.out.println("Waad guulaysatay inaad badasho PIN kaaga.");
            } else {
                System.out.println("PIN lama badalin, isku day mar kale.");
            }
        }
    }

    static void taajService(Scanner input) {
        System.out.println("** TAAJ options ** (placeholder)");
        // Waxa la dhammaystiri karaa sida ku jirta code-kaaga hore.
    }
}
