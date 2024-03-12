import java.util.ArrayList;
import java.util.List;

// Customer class representing bank customers
class Customer {
    private int customerId;
    private String name;
    private String address;
    private String phoneNumber;

    // Constructor
    public Customer(int customerId, String name, String address, String phoneNumber) {
        this.customerId = customerId;
        this.name = name;
        this.address = address;
        this.phoneNumber = phoneNumber;
    }

    // Getters and setters
    public int getCustomerId() {
        return customerId;
    }

    public void setCustomerId(int customerId) {
        this.customerId = customerId;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getAddress() {
        return address;
    }

    public void setAddress(String address) {
        this.address = address;
    }

    public String getPhoneNumber() {
        return phoneNumber;
    }

    public void setPhoneNumber(String phoneNumber) {
        this.phoneNumber = phoneNumber;
    }
}

// BankAccount class representing individual bank accounts
class BankAccount {
    private int accountId;
    private Customer customer;
    private double balance;

    // Constructor
    public BankAccount(int accountId, Customer customer, double balance) {
        this.accountId = accountId;
        this.customer = customer;
        this.balance = balance;
    }

    // Getters and setters
    public int getAccountId() {
        return accountId;
    }

    public void setAccountId(int accountId) {
        this.accountId = accountId;
    }

    public Customer getCustomer() {
        return customer;
    }

    public void setCustomer(Customer customer) {
        this.customer = customer;
    }

    public double getBalance() {
        return balance;
    }

    public void setBalance(double balance) {
        this.balance = balance;
    }

    // Deposit method
    public void deposit(double amount) {
        balance += amount;
    }

    // Withdraw method
    public boolean withdraw(double amount) {
        if (balance >= amount) {
            balance -= amount;
            return true;
        } else {
            System.out.println("Insufficient funds.");
            return false;
        }
    }
}

// Bank class representing the entire bank system
class Bank {
    private List<Customer> customers;
    private List<BankAccount> accounts;
    private int nextCustomerId = 1;
    private int nextAccountId = 1;

    // Constructor
    public Bank() {
        customers = new ArrayList<>();
        accounts = new ArrayList<>();
    }

    // Method to add a new customer
    public void addCustomer(String name, String address, String phoneNumber) {
        Customer customer = new Customer(nextCustomerId++, name, address, phoneNumber);
        customers.add(customer);
    }

    // Method to create a new account for a customer
    public void openAccount(int customerId, double initialBalance) {
        Customer customer = getCustomerById(customerId);
        if (customer != null) {
            BankAccount account = new BankAccount(nextAccountId++, customer, initialBalance);
            accounts.add(account);
            System.out.println("Account created successfully. Account ID: " + account.getAccountId());
        } else {
            System.out.println("Customer not found.");
        }
    }

    // Method to deposit into an account
    public void deposit(int accountId, double amount) {
        BankAccount account = getAccountById(accountId);
        if (account != null) {
            account.deposit(amount);
            System.out.println("Deposit successful. New balance: " + account.getBalance());
        } else {
            System.out.println("Account not found.");
        }
    }

    // Method to withdraw from an account
    public void withdraw(int accountId, double amount) {
        BankAccount account = getAccountById(accountId);
        if (account != null) {
            if (account.withdraw(amount)) {
                System.out.println("Withdrawal successful. New balance: " + account.getBalance());
            }
        } else {
            System.out.println("Account not found.");
        }
    }

    // Utility method to find a customer by ID
    private Customer getCustomerById(int customerId) {
        for (Customer customer : customers) {
            if (customer.getCustomerId() == customerId) {
                return customer;
            }
        }
        return null;
    }

    // Utility method to find an account by ID
    private BankAccount getAccountById(int accountId) {
        for (BankAccount account : accounts) {
            if (account.getAccountId() == accountId) {
                return account;
            }
        }
        return null;
    }
}

public class Main {
    public static void main(String[] args) {
        Bank bank = new Bank();

        // Adding customers
        bank.addCustomer("Akhila", "123 Main St", "123-456-7890");
        bank.addCustomer("Aswadhama", "456 Oak St", "987-654-3210");

        // Opening accounts
        bank.openAccount(1, 1000);
        bank.openAccount(2, 500);

        // Depositing and withdrawing
        bank.deposit(1, 500);
        bank.withdraw(2, 200);
    }
}
