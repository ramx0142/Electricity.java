# Electricity.java
import java.util.Scanner;

class ElectricityBill {
    int consumerNo;
    String consumerName;
    int prevReading;
    int currReading;
    String ebConnectionType; // "domestic" or "commercial"

    void getDetails() {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter Consumer Number: ");
        consumerNo = sc.nextInt();
        sc.nextLine(); // consume newline
        System.out.print("Enter Consumer Name: ");
        consumerName = sc.nextLine();
        System.out.print("Enter Previous Month Reading: ");
        prevReading = sc.nextInt();
        System.out.print("Enter Current Month Reading: ");
        currReading = sc.nextInt();
        sc.nextLine(); // consume newline
        System.out.print("Enter EB Connection Type (domestic/commercial): ");
        ebConnectionType = sc.nextLine().toLowerCase();
    }

    int calculateUnits() {
        return currReading - prevReading;
    }

    double calculateBill() {
        int units = calculateUnits();
        double amount = 0;

        if (ebConnectionType.equals("domestic")) {
            if (units <= 100) {
                amount = units * 1;
            } else if (units <= 200) {
                amount = (100 * 1) + (units - 100) * 2.5;
            } else if (units <= 500) {
                amount = (100 * 1) + (100 * 2.5) + (units - 200) * 4;
            } else {
                amount = (100 * 1) + (100 * 2.5) + (300 * 4) + (units - 500) * 6;
            }
        } else if (ebConnectionType.equals("commercial")) {
            if (units <= 100) {
                amount = units * 2;
            } else if (units <= 200) {
                amount = (100 * 2) + (units - 100) * 4.5;
            } else if (units <= 500) {
                amount = (100 * 2) + (100 * 4.5) + (units - 200) * 6;
            } else {
                amount = (100 * 2) + (100 * 4.5) + (300 * 6) + (units - 500) * 7;
            }
        }

        return amount;
    }

    void displayBill() {
        int units = calculateUnits();
        double billAmount = calculateBill();
        System.out.println("\n----- Electricity Bill -----");
        System.out.println("Consumer No   : " + consumerNo);
        System.out.println("Consumer Name : " + consumerName);
        System.out.println("Connection Type : " + ebConnectionType);
        System.out.println("Units Consumed  : " + units);
        System.out.println("Total Bill Amount: Rs. " + billAmount);
    }
}

public class ElectricityBillMain {
    public static void main(String[] args) {
        ElectricityBill bill = new ElectricityBill();
        bill.getDetails();
        bill.displayBill();
    }
}
