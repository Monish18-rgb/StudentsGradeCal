package codesoft;

import java.util.InputMismatchException;
import java.util.Scanner;

public class StudentsGradeCalculator {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        int numSubjects = 0;
        boolean validInput = false;

        // Input validation for number of subjects
        while (!validInput) {
            try {
                System.out.print("Enter the number of subjects: ");
                numSubjects = scanner.nextInt();

                if (numSubjects <= 0) {
                    System.out.println("Number of subjects must be positive.");
                } else {
                    validInput = true;
                }

            } catch (InputMismatchException e) {
                System.out.println("Invalid input. Please enter a positive integer.");
                scanner.next(); // Clear the invalid input
            }
        }

        int[] marks = new int[numSubjects];
        int totalMarks = 0;

        for (int i = 0; i < numSubjects; i++) {
            validInput = false;

            // Input validation for marks
            while (!validInput) {
                try {
                    System.out.print("Enter marks for subject " + (i + 1) + ": ");
                    marks[i] = scanner.nextInt();

                    if (marks[i] < 0) {
                        System.out.println("Marks cannot be negative. Please enter again.");
                    } else {
                        totalMarks += marks[i];
                        validInput = true;
                    }

                } catch (InputMismatchException e) {
                    System.out.println("Invalid input. Please enter a non-negative integer for marks.");
                    scanner.next(); // Clear the invalid input
                }
            }
        }

        double averagePercentage = numSubjects > 0 ? (double) totalMarks / numSubjects : 0.0;
        char grade = calculateGrade(averagePercentage);

        System.out.printf("\nTotal Marks: %d\n", totalMarks);
        System.out.printf("Average Percentage: %.2f\n", averagePercentage);
        System.out.println("Grade: " + grade);

        scanner.close();
    }

    private static char calculateGrade(double averagePercentage) {
        if (averagePercentage >= 90) {
            return 'A';
        } else if (averagePercentage >= 80) {
            return 'B';
        } else if (averagePercentage >= 70) {
            return 'C';
        } else if (averagePercentage >= 60) {
            return 'D';
        } else {
            return 'F';
        }
    }
}
