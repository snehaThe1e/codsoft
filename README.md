# codsoft
#ATMinterface

package atminterface;

import java.util.ArrayList;
  import java.util.Scanner;

class Transaction {
	 private String type;
    private double amount;
    

    public Transaction(String type,double amount) {
    	this.type = type;
        this.amount = amount;
    }

    public String getType() {
        return type;
    }

    public double getAmount() {
        return amount;
    }
}

class Bankaccount {
    private String accountNumber;
    private double balance;
    private ArrayList<Transaction> transactionHistory;

    public Bankaccount(String accountNumber) {
        this.accountNumber = accountNumber;
        this.balance = 0.0;
        this.transactionHistory = new ArrayList<>();
    }

    public double getBalance() {
        return balance;
    }

    public void deposit(double amount) {
        if (amount > 0) {
            balance += amount;
            transactionHistory.add(new Transaction("Deposit", amount));
            System.out.println("Deposit successful. New balance: " + balance);
        } 
        else 
        {
            System.out.println("Invalid deposit amount.");
        }
    }

    public void withdraw(double amount) {
        if (amount > 0 && amount <= balance) {
            balance -= amount;
            transactionHistory.add(new Transaction("Withdrawal", amount));
            System.out.println("Withdrawal successful. New balance: " + balance);
        } else {
            System.out.println("Invalid withdrawal amount or insufficient balance.");
        }
    }

    public void transfer(Bankaccount receiver, double amount) {
        if (amount > 0 && amount <= balance) {
            balance -= amount;
            receiver.deposit(amount);
            transactionHistory.add(new Transaction("Transfer to " + receiver.getAccountNumber(), amount));
            System.out.println("Transfer successful. New balance: " + balance);
        } else {
            System.out.println("Invalid transfer amount or insufficient balance.");
        }
    }

    public void printTransactionHistory() {
        System.out.println("Transaction History for Account: " + accountNumber);
        for (Transaction transaction : transactionHistory) {
            System.out.println(transaction.getType() + ": " + transaction.getAmount());
        }
    }

    public String getAccountNumber() {
        return accountNumber;
    }
}

public class Atminterface {
    public static void main(String[] args) 
    {
    	
        Scanner scanner = new Scanner(System.in);
        Bankaccount account1 = new Bankaccount("12345");

        while (true) {
            System.out.println("\nAtm Menu:");
            System.out.println("1] Transaction history.\n2] Withdraw.\n3] Deposit .\n4] Transfer.\n6] Quit");
            System.out.print("Enter your choice: ");

            int choice = scanner.nextInt();

            switch (choice) {    
            case 1:
                account1.printTransactionHistory();
                break;
            case 2:
                System.out.print("Enter withdrawal amount: ");
                double withdrawAmount = scanner.nextDouble();
                account1.withdraw(withdrawAmount);
                break;
             case 3:
                 System.out.print("Enter deposit amount: ");
                 double depositAmount = scanner.nextDouble();
                 account1.deposit(depositAmount);
                 break;
             case 4:
                 System.out.print("Enter recipient's account number: ");
                 String recipientAccountNumber = scanner.next();
                 Bankaccount recipientAccount = new Bankaccount(recipientAccountNumber);
                 System.out.print("Enter transfer amount: ");
                 double transferAmount = scanner.nextDouble();
                 account1.transfer(recipientAccount, transferAmount);
                 break;
             
                case 5:
                    System.out.println("Thank you . have a Goodday!");
                    System.exit(0);
                    break;
                  default:
                  System.out.println("invaild choice .please select void choice.");
            }
        }
    }
}
