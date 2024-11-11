# CFAproject
Java project for Chick-Fil-A

import java.util.*;
public class Menu {

	
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
