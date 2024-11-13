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

import java.util.*;

public class Menu {
    private HashMap<Integer, MenuItem> items;

    public Menu() {
    	items = new HashMap<>();
        items.put(1, new MenuItem("Chicken Sandwich", 5.99, "Entree"));
        items.put(2, new MenuItem("Spicy Chicken Sandwich", 5.99, "Entree"));
        items.put(3, new MenuItem("Grilled Cool Wrap", 6.99, "Entree"));
        items.put(4, new MenuItem("Chicken Nuggets", 4.99, "Entree"));
        items.put(5, new MenuItem("Waffle Fries", 2.99, "Side"));
        items.put(6, new MenuItem("Mac and Cheese", 3.99, "Side"));
        items.put(7, new MenuItem("Sweet Tea", 1.99, "Drink"));
        items.put(8, new MenuItem("Lemonade", 1.99, "Drink"));
        items.put(9, new MenuItem("Milkshake", 3.99, "Dessert"));
        items.put(10, new MenuItem("Chocolate Chip Cookie", 2.99, "Dessert"));
    }

    public MenuItem getItem(int id) {
        return items.get(id);
    }

    public HashMap<Integer, MenuItem> getItems() {
        return items;
    }
    
    public void printInfo() {
    	System.out.println("Welcome to ChickFilA");
    	System.out.println("See the Menu below: ");
    	System.out.println();
    	
    	System.out.println("Entrees: ");
    	System.out.println("  1: Chicken Sandwich: $5.99");
    	System.out.println("  2: Spicy Chicken Sandwich: $5.99");
    	System.out.println("  3: Grilled Cool Wrap: $6.99");
    	System.out.println("  4: Chicken Nuggets: $4.99");
    	
    	
    	System.out.println("Sides:");
    	System.out.println("  5: Waffle Fries: $2.99");
    	System.out.println("  6: Mac and Cheese: $3.99");
    	
    	
    	System.out.println("Drinks:");
    	System.out.println("  7: Sweet Tea: $1.99");
    	System.out.println("  8: Lemonade: $1.99");
    	
    	
    	System.out.println("Desserts: ");
    	System.out.println("  9:  Milkshake: $3.99");
    	System.out.println("  10: Chocolate Chip Cookie: $2.99");
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

        scanner.close();
    }
}


11/13/24 code--> 
import java.util.*;

public class ChickFilAOrderSimulation {

public static void main(String[] args) {
    Scanner input = new Scanner(System.in);
    Menu menu = new Menu();
    OrderProcessor orderProcessor = new OrderProcessor();
int option;
    System.out.println("Welcome to Chick-Fil-A! Enter (1) for Dine in or (2) for drive thru."); 
    
option = input.nextInt(); 

    switch (option) {
    case 1: System.out.println("--- Scenario 1: Dine-In Order ---");
    System.out.print("Enter table number for dine-in: ");
    int tableNumber = input.nextInt();
    Order dineInOrder = new DineInOrder(tableNumber);
    orderProcessor.processOrder(dineInOrder, menu, input);
 break; 
    
   
    
    case 2:
    System.out.println("--- Scenario 2: Drive-Thru Order ---");
    Order driveThruOrder = new DriveThruOrder();
    orderProcessor.processOrder(driveThruOrder, menu, input);
break;
    }
}
}
--------------
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
---------------
import java.util.*;

class DriveThruOrder extends Order {
String make; 
String model; 

Scanner input = new Scanner(System.in);
//private static final double PROCESSING_FEE = 1.00;

public DriveThruOrder() {
    super();
}

@Override
public double getTotalPrice() {
    return super.getTotalPrice(); //+ PROCESSING_FEE;
}


@Override
public void printOrderDetails() {
	System.out.println("Please enter you car make/model: "); 
    String make = input.nextLine(); 
    String model =input.nextLine(); 
    
    System.out.println("Drive-Thru Order:");
    
    
    
    super.printOrderDetails();
   // System.out.printf("Processing Fee: $%.2f%n");//, PROCESSING_FEE);
   
   // System.out.printf("Total with Fee: $%.2f%n", getTotalPrice());
    System.out.println("Car details: " + make + " "  + model); 
    
}
}
------------------------
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
----------------
import java.util.*;

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
-----------------
import java.util.*;

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
    double tax; 
    tax = ((totalPrice * 1.08) - totalPrice);
    System.out.println("Tax: $" + String.format("%.2f", tax));
    System.out.printf("Total Price: $%.2f%n", totalPrice * 1.08 );
}
}
-----------------------
import java.util.*;

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
--------------------
class Receipt extends Order {
double tax;
public void printReceipt(Order order) {
    System.out.println("\n---- Receipt ----");
    order.printOrderDetails();
    
   
    System.out.println("Thank you for choosing Chick-fil-A!");
   
    
}
}

