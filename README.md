# CFAproject
Java project for Chick-Fil-A

import java.util.*;

// MenuItem class to represent each item in the menu

class MenuItem {
    
    private final String name;
    private final double price;

    public MenuItem(String name, double price) {
        this.name = name;
        this.price = price;
    }

    public String getName() {
        return name;
    }

    public double getPrice() {
        return price;
    }

    @Override
    public String toString() {
        return name + " - $" + price;
    }
}

// Menu class to hold the menu items

class Menu {
   
    private final HashMap<Integer, MenuItem> items;

    public Menu() {
        items = new HashMap<>();
        items.put(1, new MenuItem("Chicken Sandwich", 5.50));
        items.put(2, new MenuItem("Fries", 2.00));
        items.put(3, new MenuItem("Nuggets", 4.00));
        items.put(4, new MenuItem("Drink", 1.50));
    }

    public void displayMenu() {
        System.out.println("---- Chick-fil-A Menu ----");
        for (Map.Entry<Integer, MenuItem> entry : items.entrySet()) {
            System.out.println(entry.getKey() + ". " + entry.getValue());
        }
    }

    public MenuItem getMenuItem(int id) {
        return items.get(id);
    }
}

// Base Order class

class Order {
   
    private final ArrayList<MenuItem> items;
    private double totalPrice;

    public Order() {
        items = new ArrayList<>();
        totalPrice = 0.0;
    }

    public void addItem(MenuItem item) {
        items.add(item);
        totalPrice += item.getPrice();
    }

    public ArrayList<MenuItem> getItems() {
        return items;
    }

    public double getTotalPrice() {
        return totalPrice;
    }

    public void printOrderDetails() {
        for (MenuItem item : items) {
            System.out.println(item);
        }
        System.out.printf("Total Price: $%.2f%n", totalPrice);
    }
}

// DineInOrder subclass with a table number

class DineInOrder extends Order {
    
    private final int tableNumber;

    public DineInOrder(int tableNumber) {
        super();
        this.tableNumber = tableNumber;
    }

    public int getTableNumber() {
        return tableNumber;
    }

    @Override
    public void printOrderDetails() {
        System.out.println("Dine-In Order (Table #" + tableNumber + "):");
        super.printOrderDetails();
    }
}

// DriveThruOrder subclass with a processing fee

class DriveThruOrder extends Order {
    
    private static final double PROCESSING_FEE = 1.00;

    public DriveThruOrder() {
        super();
    }

    @Override
    public double getTotalPrice() {
        return super.getTotalPrice() + PROCESSING_FEE;
    }

    @Override
    public void printOrderDetails() {
        System.out.println("Drive-Thru Order:");
        super.printOrderDetails();
        System.out.printf("Processing Fee: $%.2f%n", PROCESSING_FEE);
        System.out.printf("Total with Fee: $%.2f%n", getTotalPrice());
    }
}

// Receipt class for printing the receipt

class Receipt {
   
    public void printReceipt(Order order) {
        System.out.println("\n---- Receipt ----");
        order.printOrderDetails();
        System.out.println("Thank you for choosing Chick-fil-A!");
    }
}

// OrderProcessor class to handle different types of orders

class OrderProcessor {
    
    public void processOrder(Order order, Menu menu, Scanner scanner) {
        System.out.println("Please choose items for your order.");
        menu.displayMenu();

        while (true) {
            System.out.print("Enter item number to add to order (0 to finish): ");
            int choice = scanner.nextInt();
            if (choice == 0) {
                break;
            }
            MenuItem item = menu.getMenuItem(choice);
            if (item != null) {
                order.addItem(item);
                System.out.println(item.getName() + " added to your order.");
            } else {
                System.out.println("Invalid selection, please try again.");
            }
        }
        
        Receipt receipt = new Receipt();
        receipt.printReceipt(order);
    }
}

// Main class to demonstrate scenarios

public class ChickFilAOrderSimulation {
   
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        Menu menu = new Menu();
        OrderProcessor orderProcessor = new OrderProcessor();

        // Scenario 1: Dine-In Order
        System.out.println("\n--- Scenario 1: Dine-In Order ---");
        System.out.print("Enter table number for dine-in: ");
        int tableNumber = scanner.nextInt();
        Order dineInOrder = new DineInOrder(tableNumber);
        orderProcessor.processOrder(dineInOrder, menu, scanner);

        // Scenario 2: Drive-Thru Order
        System.out.println("\n--- Scenario 2: Drive-Thru Order ---");
        Order driveThruOrder = new DriveThruOrder();
        orderProcessor.processOrder(driveThruOrder, menu, scanner);

    
    }
}


