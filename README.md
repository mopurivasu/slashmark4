public class Employee {
    private int id;
    private String name;
    private String department;
    private double salary;

    public Employee(int id, String name, String department, double salary) {
        this.id = id;
        this.name = name;
        this.department = department;
        this.salary = salary;
    }

    public int getId() {
        return id;
    }

    public String getName() {
        return name;
    }

    public String getDepartment() {
        return department;
    }

    public double getSalary() {
        return salary;
    }

    @Override
    public String toString() {
        return "Employee{" +
                "id=" + id +
                ", name='" + name + '\'' +
                ", department='" + department + '\'' +
                ", salary=" + salary +
                '}';
    }
}
import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;

public class EmployeeManagement {

    private List<Employee> employees;
    private int nextId;

    public EmployeeManagement() {
        employees = new ArrayList<>();
        nextId = 1;
    }

    public void addEmployee(String name, String department, double salary) {
        Employee employee = new Employee(nextId++, name, department, salary);
        employees.add(employee);
        System.out.println("Employee added: " + employee);
    }

    public void listEmployees() {
        if (employees.isEmpty()) {
            System.out.println("No employees found.");
        } else {
            System.out.println("Employee List:");
            for (Employee employee : employees) {
                System.out.println(employee);
            }
        }
    }

    public void removeEmployee(int id) {
        Employee toRemove = null;
        for (Employee employee : employees) {
            if (employee.getId() == id) {
                toRemove = employee;
                break;
            }
        }

        if (toRemove != null) {
            employees.remove(toRemove);
            System.out.println("Employee removed: " + toRemove);
        } else {
            System.out.println("Employee with id " + id + " not found.");
        }
    }

    public static void main(String[] args) {
        EmployeeManagement management = new EmployeeManagement();
        Scanner scanner = new Scanner(System.in);

        while (true) {
            System.out.println("\nEmployee Management System");
            System.out.println("1. Add Employee");
            System.out.println("2. List Employees");
            System.out.println("3. Remove Employee");
            System.out.println("4. Exit");
            System.out.print("Enter your choice: ");

            int choice = scanner.nextInt();
            scanner.nextLine();  // consume the newline

            switch (choice) {
                case 1:
                    System.out.print("Enter name: ");
                    String name = scanner.nextLine();
                    System.out.print("Enter department: ");
                    String department = scanner.nextLine();
                    System.out.print("Enter salary: ");
                    double salary = scanner.nextDouble();
                    management.addEmployee(name, department, salary);
                    break;
                case 2:
                    management.listEmployees();
                    break;
                case 3:
                    System.out.print("Enter employee ID to remove: ");
                    int id = scanner.nextInt();
                    management.removeEmployee(id);
                    break;
                case 4:
                    System.out.println("Exiting...");
                    scanner.close();
                    System.exit(0);
                default:
                    System.out.println("Invalid choice. Please try again.");
            }
        }
    }
}
