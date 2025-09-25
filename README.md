package com.mycompany.ammar;
import java.util.Scanner;

public class ATM_project  {

    int balance = 0; // initial balance

    // Deposit method
    void deposit(int amount) {
        if (amount > 0) {
            balance += amount;
            System.out.println("Deposited: " + amount);
        } else {
            System.out.println("Invalid deposit amount!");
        }
    }

    // Withdraw method
    void withdraw(int amount) {
        if (amount > 0 && amount <= balance) {
            balance -= amount;
            System.out.println("Withdrawn: " + amount);
        } else if (amount > balance) {
            System.out.println("Insufficient funds!");
        } else {
            System.out.println("Invalid withdraw amount!");
        }
    }

    // Check balance method
    void checkBalance() {
        System.out.println("Your Balance = " + balance);
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        ATM_project atm = new ATM_project();
        int pin = 1234;
        boolean loggedIn = false;

        // 3 attempts for PIN
        for (int i = 1; i <= 3; i++) {
            System.out.print("Enter PIN: ");
            int enteredPin = sc.nextInt();
            if (enteredPin == pin) {
                loggedIn = true;
                break;
            } else {
                System.out.println("Wrong PIN! Attempts left: " + (3 - i));
            }
        }

        if (!loggedIn) {
            System.out.println("Account locked due to 3 wrong attempts.");
            return;
        }

        // Menu after login
        while (true) {
            System.out.println("\nATM Menu:");
            System.out.println("1. Deposit");
            System.out.println("2. Withdraw");
            System.out.println("3. Check Balance");
            System.out.println("4. Exit");
            System.out.print("Choose option: ");
            int choice = sc.nextInt();

            switch (choice) {
                case 1:
                    System.out.print("Enter amount to deposit: ");
                    int dep = sc.nextInt();
                    atm.deposit(dep);
                    break;
                case 2:
                    System.out.print("Enter amount to withdraw: ");
                    int wd = sc.nextInt();
                    atm.withdraw(wd);
                    break;
                case 3:
                    atm.checkBalance();
                    break;
                case 4:
                    System.out.println("Thank you for using ATM. Goodbye!");
                    sc.close();
                    return;
                default:
                    System.out.println("Invalid choice!");
            }
        }
    }
}
