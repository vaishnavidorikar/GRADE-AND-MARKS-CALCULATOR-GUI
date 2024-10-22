# GRADE-AND-MARKS-CALCULATOR-GUI

package markscalculator;
import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

public class MarksCalculator extends JFrame {
    
    private JTextField[] subjectFields;
    private JLabel totalMarksLabel, averageLabel, gradeLabel;
    private JButton calculateButton;
    private final int NUM_SUBJECTS = 5; // Adjust the number of subjects here

    public MarksCalculator() {
        setTitle("Marks Calculator");
        setSize(800, 800);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLayout(new GridLayout(NUM_SUBJECTS + 4, 2));

        // Set the background color of the entire frame
        getContentPane().setBackground(new Color(230, 230, 250)); // Light lavender color

        subjectFields = new JTextField[NUM_SUBJECTS];

        // Add input fields for each subject with custom colors
        for (int i = 0; i < NUM_SUBJECTS; i++) {
            JLabel label = new JLabel("Subject " + (i + 1) + " Marks:");
            label.setForeground(new Color(0, 128, 128)); // Dark cyan color
            add(label);

            subjectFields[i] = new JTextField();
            subjectFields[i].setBackground(new Color(255, 255, 204)); // Light yellow background
            subjectFields[i].setForeground(new Color(75, 0, 130)); // Indigo text color
            add(subjectFields[i]);
        }

        calculateButton = new JButton("Calculate");
        calculateButton.setBackground(new Color(0, 128, 128)); // Dark cyan background
        calculateButton.setForeground(Color.WHITE); // White text color

        totalMarksLabel = new JLabel("Total Marks: ");
        totalMarksLabel.setForeground(new Color(0, 0, 139)); // Dark blue color

        averageLabel = new JLabel("Average Percentage: ");
        averageLabel.setForeground(new Color(0, 0, 139)); // Dark blue color

        gradeLabel = new JLabel("Grade: ");
        gradeLabel.setForeground(new Color(0, 0, 139)); // Dark blue color

        add(calculateButton);
        add(new JLabel(""));  // Empty label for spacing
        add(totalMarksLabel);
        add(averageLabel);
        add(gradeLabel);

        // ActionListener for the Calculate button
        calculateButton.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                calculateResults();
            }
        });
    }

    // Method to calculate total marks, average, and grade
    private void calculateResults() {
        try {
            int totalMarks = 0;

            // Get marks from input fields and calculate total
            for (int i = 0; i < NUM_SUBJECTS; i++) {
                int marks = Integer.parseInt(subjectFields[i].getText());
                totalMarks += marks;
            }

            // Calculate average percentage
            double averagePercentage = (double) totalMarks / NUM_SUBJECTS;

            // Determine grade based on average percentage
            String grade;
            if (averagePercentage >= 90) {
                grade = "A";
            } else if (averagePercentage >= 80) {
                grade = "B";
            } else if (averagePercentage >= 70) {
                grade = "C";
            } else if (averagePercentage >= 60) {
                grade = "D";
            } else {
                grade = "F";
            }

            // Display results
            totalMarksLabel.setText("Total Marks: " + totalMarks);
            averageLabel.setText("Average Percentage: " + String.format("%.2f", averagePercentage) + "%");
            gradeLabel.setText("Grade: " + grade);

        } catch (NumberFormatException ex) {
            JOptionPane.showMessageDialog(this, "Please enter valid numeric values for marks.");
        }
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(new Runnable() {
            @Override
            public void run() {
                new MarksCalculator().setVisible(true);
            }
        });
    }
}
