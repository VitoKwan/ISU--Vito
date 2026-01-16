import java.util.ArrayList;
import java.util.Scanner;

public class ISU {
    public static void main(String[] args) {

        Scanner input = new Scanner(System.in);
        boolean run = true;
        ArrayList<String> firstNames = new ArrayList<>();
        ArrayList<String> lastNames = new ArrayList<>();
        ArrayList<Integer> marks = new ArrayList<>();

        firstNames.add("Jay");
        lastNames.add("Kat");
        marks.add(67);
        firstNames.add("Dean");
        lastNames.add("Lo");
        marks.add(87);
        firstNames.add("Bosco");
        lastNames.add("King");
        marks.add(92);
        firstNames.add("Cloud");
        lastNames.add("Ware");
        marks.add(95);
        firstNames.add("Marco");
        lastNames.add("King");
        marks.add(72);

        System.out.println("Welcome to the Course Management System!");
        while (run) {
            double sum = 0;
            for (int i = 0; i < marks.size(); i++) {
                sum += marks.get(i);
            }
            double average = sum / marks.size();
            
            System.out.println("\n===== MAIN MENU =====");
            System.out.println("1. Add a student");
            System.out.println("2. Average of class marks");
            System.out.println("3. Minimum and Maximum mark");
            System.out.println("4. Display the list of students");
            System.out.println("5. Display the mark distribution");
            System.out.println("6. Search a student");
            System.out.println("7. Display top and bottom 20%");
            System.out.println("8. Exit");
            System.out.print("Choose an option: ");
            int choice = input.nextInt();
            switch (choice) {
                case 1:
                    for (int i = 0; i < 2; i++) {
                        System.out.print("Enter first name: ");
                        String firstName = input.next();
                        System.out.print("Enter last name: ");
                        String lastName = input.next();
                        System.out.print("Enter mark: ");
                        int mark = input.nextInt();
                        input.nextLine();
                        System.out.println("Student added: " + firstName + " " + lastName + " - " + mark);
                        if (i < 1) {
                            System.out.print("Add another student? (yes/no): ");
                            String add = input.nextLine().toLowerCase();
                            if (!add.equals("yes"))
                                break;
                        }
                    }
                    break;

                case 2:
                    System.out.println("Class average: " + average);
                    break;

                case 3:
                    int low = marks.get(0);
                    int high = marks.get(0);
                    int lowIndex = 100;
                    int highIndex = 0;
                    for (int i = 1; i < marks.size(); i++) {
                        if (marks.get(i) < low) {
                            low = marks.get(i);
                            lowIndex = i;
                        }
                        if (marks.get(i) > high) {
                            high = marks.get(i);
                            highIndex = i;
                        }
                    }
                    System.out.println("Lowest mark: " + low + " (" + firstNames.get(lowIndex) + " " + lastNames.get(lowIndex) + ")");
                    System.out.println("Highest mark: " + high + " (" + firstNames.get(highIndex) + " " + lastNames.get(highIndex) + ")");
                    break;

                case 4:
                    System.out.println("ID\tFirst Name\tLast Name\tMark");
                    for (int i = 0; i < marks.size(); i++) {
                        System.out.println(i + "\t" + firstNames.get(i) + "\t\t" + lastNames.get(i) + "\t\t" + marks.get(i));
                    }

                    System.out.println("\n1. Edit a Student");
                    System.out.println("2. Remove a Student");
                    System.out.println("3. Return to the main menu");
                    System.out.print("Choose an option: ");
                    int subChoice = input.nextInt();
                    if (subChoice == 1) {
                        System.out.print("Enter student ID to edit: ");
                        int id = input.nextInt();
                        if (id >= 0 && id < marks.size()) {
                            System.out.print("Enter new first name: ");
                            firstNames.set(id, input.next());
                            System.out.print("Enter new last name: ");
                            lastNames.set(id, input.next());
                            System.out.print("Enter new mark: ");
                            marks.set(id, input.nextInt());
                            System.out.println("Student information updated.");
                        } else
                            System.out.println("Invalid student ID.");
                    } else if (subChoice == 2) {
                        System.out.print("Enter student ID to remove: ");
                        int id = input.nextInt();
                        if (id >= 0 && id < marks.size()) {
                            firstNames.remove(id);
                            lastNames.remove(id);
                            marks.remove(id);
                            System.out.println("Student removed.");
                        } else
                            System.out.println("Invalid student ID.");
                    } else if (subChoice == 3)
                        System.out.println("Returning to main menu...");
                    else
                        System.out.println("Invalid option.");

                    break;

                case 5:
                    int countA = 0, countB = 0, countC = 0, countD = 0, countF = 0;

                    // count grades
                    for (int i = 0; i < marks.size(); i++) {
                        int m = marks.get(i);
                        if (m >= 80)
                            countA++;
                        else if (m >= 70)
                            countB++;
                        else if (m >= 60)
                            countC++;
                        else if (m >= 50)
                            countD++;
                        else
                            countF++;
                    }
                    int max = countA;
                    if (countB > max)
                        max = countB;
                    if (countC > max)
                        max = countC;
                    if (countD > max)
                        max = countD;
                    if (countF > max)
                        max = countF;

                    for (int level = max; level > 0; level--) {

                        if (countA >= level)
                            System.out.print(" * ");
                        else
                            System.out.print("   ");

                        if (countB >= level) System.out.print(" * ");
                        else System.out.print("   ");

                        if (countC >= level) System.out.print(" * ");
                        else System.out.print("   ");

                        if (countD >= level) System.out.print(" * ");
                        else System.out.print("   ");

                        if (countF >= level) System.out.print(" * ");
                        else System.out.print("   ");

                        System.out.println();
                    }

                    System.out.println("-------------------------");
                    System.out.println(" A   B   C   D   F");
                    break;

                case 6:
                    System.out.print("Enter a first name or last name to search: ");
                    String keyword = input.next().toLowerCase();
                    boolean found = false;
                    for (int i = 0; i < firstNames.size(); i++) {
                        String fName = firstNames.get(i).toLowerCase();
                        String lName = lastNames.get(i).toLowerCase();
                        if (fName.contains(keyword) || lName.contains(keyword)) {
                            found = true;
                            System.out.println("ID: " + i);
                            System.out.println("Name: " + firstNames.get(i) + " " + lastNames.get(i));
                            System.out.println("Mark: " + marks.get(i));
                            if (marks.get(i) > average)
                                System.out.println("This student is ABOVE the class average.");
                            else if (marks.get(i) == average)
                                System.out.println("This student is AT the class average.");
                            else
                                System.out.println("This student is BELOW the class average.");
                            System.out.println();
                        }
                    }
                    if (!found)
                        System.out.println("No student found.");
                    break;
                case 7:
                    int total = marks.size();
                    int[] temp = new int[total];
                    for (int i = 0; i < marks.size(); i++) {
                        temp[i] = marks.get(i);
                    }
                    for (int i = 0; i < total - 1; i++) {
                        for (int j = i + 1; j < marks.size(); j++) {
                            if (temp[i] > temp[j]) {
                                int t = temp[i];
                                temp[i] = temp[j];
                                temp[j] = t;
                            }
                        }
                    }
                    int lowIn = (int)(0.2 * total);
                    int highIn = (int)(0.8 * total);
                    int lowCutoff = temp[lowIn];
                    int highCutoff = temp[highIn];
                    System.out.println("Bottom 20%:");
                    for (int i = 0; i < total; i++) {
                        if (marks.get(i) <= lowCutoff)
                            System.out.println(firstNames.get(i) + " " + lastNames.get(i) + " - " + marks.get(i));
                    }

                    System.out.println("\nTop 20%:");
                    for (int i = 0; i < total; i++) {
                        if (marks.get(i) >= highCutoff)
                            System.out.println(firstNames.get(i) + " " + lastNames.get(i) + " - " + marks.get(i));
                    }
                    break;

                case 8:
                    System.out.println("Thank you for using the CMS!");
                    run = false;
                    break;

                default:
                    System.out.println("Invalid option. Please try again.");
            }
        }
        input.close();
    }
}
