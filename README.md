# 23BCS10234_Vijay-Bhaskar-ex-2.3

import java.util.*;
import java.util.stream.*;

class Employee {
    int id;
    String name;
    double salary;

    Employee(int id, String name, double salary) {
        this.id = id;
        this.name = name;
        this.salary = salary;
    }

    public String toString() {
        return id + " - " + name + " - $" + salary;
    }
}

class Student {
    int id;
    String name;
    int marks;

    Student(int id, String name, int marks) {
        this.id = id;
        this.name = name;
        this.marks = marks;
    }

    public String toString() {
        return id + " - " + name + " - Marks: " + marks;
    }
}

class Product {
    int id;
    String name;
    double price;

    Product(int id, String name, double price) {
        this.id = id;
        this.name = name;
        this.price = price;
    }

    public String toString() {
        return id + " - " + name + " - ₹" + price;
    }
}

public class Experiment2_3 {

    public static void main(String[] args) {
        System.out.println("===== Part A: Sorting Employee Objects =====");
        sortEmployees();

        System.out.println("\n===== Part B: Filtering and Sorting Students =====");
        filterAndSortStudents();

        System.out.println("\n===== Part C: Stream Operations on Product Dataset =====");
        streamOperationsOnProducts();
    }

    // Part A: Sorting Employee Objects Using Lambda Expressions
    static void sortEmployees() {
        List<Employee> employees = new ArrayList<>();
        employees.add(new Employee(1, "Alice", 70000));
        employees.add(new Employee(2, "Bob", 50000));
        employees.add(new Employee(3, "Charlie", 60000));

        System.out.println("Original List:");
        employees.forEach(System.out::println);

        // Sort by name
        employees.sort((e1, e2) -> e1.name.compareTo(e2.name));
        System.out.println("\nSorted by Name:");
        employees.forEach(System.out::println);

        // Sort by salary
        employees.sort(Comparator.comparingDouble(e -> e.salary));
        System.out.println("\nSorted by Salary:");
        employees.forEach(System.out::println);
    }

    // Part B: Filtering and Sorting Students Using Streams
    static void filterAndSortStudents() {
        List<Student> students = Arrays.asList(
            new Student(1, "Ravi", 75),
            new Student(2, "Anu", 90),
            new Student(3, "John", 60),
            new Student(4, "Meena", 85)
        );

        System.out.println("Students with marks > 70, sorted by name:");

        students.stream()
                .filter(s -> s.marks > 70)
                .sorted(Comparator.comparing(s -> s.name))
                .forEach(System.out::println);
    }

    // Part C: Stream Operations on Product Dataset
    static void streamOperationsOnProducts() {
        List<Product> products = Arrays.asList(
            new Product(1, "Laptop", 75000),
            new Product(2, "Mouse", 500),
            new Product(3, "Keyboard", 1000),
            new Product(4, "Monitor", 15000)
        );

        System.out.println("Filtered Products (price > 1000):");
        products.stream()
                .filter(p -> p.price > 1000)
                .forEach(System.out::println);

        System.out.println("\nList of Product Names:");
        List<String> productNames = products.stream()
                                            .map(p -> p.name)
                                            .collect(Collectors.toList());
        productNames.forEach(System.out::println);

        System.out.println("\nTotal Price of All Products:");
        double totalPrice = products.stream()
                                    .mapToDouble(p -> p.price)
                                    .sum();
        System.out.println("₹" + totalPrice);
    }
}
